---
hidden: true
noIndex: true
noRobotsIndex: true
---

# Create and deploy a custom application with REST

Create a custom application from an MSI, upload its installer, and deploy it using settings from a deployment template. Choose PowerShell or curl (Bash), then use that tab at every step in the same shell session. Both versions send HTTP requests directly; neither requires the Patch My PC PowerShell module.

You need a PAT with `appcatbroker:apps:write` and `appcatbroker:apps:deploy`, an Intune connection with granted admin consent, and an approved test group. Your account must have custom applications and deployment management enabled, with room for another application.

This example uses one Windows x64 MSI smaller than 32 MiB. Use the actual MSI product code, publisher, language, ARP display name and version for your installer; the values below describe the example file, not every MSI.

Use PowerShell 7.4 or later, or Bash with curl 7.76 or later, jq and OpenSSL. Run the curl examples in Bash, not in a PowerShell session.

### 1. Authenticate and choose a connection

Use your company's regional portal: `us.portal.patchmypc.com`, `eu.portal.patchmypc.com` or `uk.portal.patchmypc.com`. Read the PAT from a secret environment variable; do not put it in the script or print the exchange response.

{% tabs %}
{% tab title="PowerShell" %}
```powershell
$ErrorActionPreference = 'Stop'
$portal = 'https://us.portal.patchmypc.com'
$api = "$portal/v1/api"
if ([string]::IsNullOrWhiteSpace($env:PMPC_PAT)) {
    throw 'Set PMPC_PAT from your secret store before running this example.'
}
$session = Invoke-RestMethod -Method Post -Uri "$api/auth/token" `
    -Headers @{ Authorization = "Bearer $env:PMPC_PAT" }
$accessToken = $session.gatewayJwt
$headers = @{ Authorization = "Bearer $accessToken"; Accept = 'application/json' }

$connections = Invoke-RestMethod -Method Get -Uri "$api/connections" -Headers $headers
$connections | Select-Object connectionId, displayName, adminConsent
$connectionId = [guid](Read-Host 'Connection ID of the Intune connection to use')
$connection = @($connections | Where-Object { $_.connectionId -eq $connectionId })
if ($connection.Count -ne 1 -or $connection[0].adminConsent -ne 'Granted') {
    throw 'Choose a listed Intune connection with granted admin consent.'
}
```
{% endtab %}

{% tab title="curl (Bash)" %}
```bash
set -euo pipefail
portal='https://us.portal.patchmypc.com'
api="$portal/v1/api"
: "${PMPC_PAT:?Set PMPC_PAT from your secret store}"

session=$(curl --fail-with-body --silent --show-error --request POST "$api/auth/token" \
  --header "Authorization: Bearer $PMPC_PAT")
access_token=$(jq -er '.gatewayJwt | select(type == "string" and length > 0)' <<< "$session")
connections=$(curl --fail-with-body --silent --show-error "$api/connections" \
  --header "Authorization: Bearer $access_token")
jq -r '.[] | [.connectionId, .displayName, .adminConsent] | @tsv' <<< "$connections"
read -r -p 'Connection ID of the Intune connection to use: ' connection_id
jq -e --arg id "$connection_id" \
  '[.[] | select(.connectionId == $id)] | length == 1 and .[0].adminConsent == "Granted"' \
  <<< "$connections" > /dev/null
```
{% endtab %}
{% endtabs %}

Keep the access token for subsequent calls, including the upload. Exchange the PAT again when the token expires; `expiresIn` gives its lifetime in seconds.

### 2. Prepare the installer and create a draft

Set the metadata to match your installer. The unique display name identifies the application you create; `arpDisplayNameMatch` describes the installed application's Add or Remove Programs entry and need not match that unique name.

{% tabs %}
{% tab title="PowerShell" %}
```powershell
$installerPath = 'C:\Packages\7zip\7z2408-x64.msi'
$installer = Get-Item -LiteralPath $installerPath
if ($installer.PSIsContainer -or $installer.Extension -ine '.msi' -or
    $installer.Length -eq 0 -or $installer.Length -ge 32MB) {
    throw 'This example needs a nonempty MSI smaller than 32 MiB.'
}
$fileName = $installer.Name
$msiProductCode = [guid](Read-Host 'Product code from this MSI')
$displayName = "Archive Tool $([guid]::NewGuid().ToString('N'))"
$metadata = @{
    displayName = $displayName
    description = 'File archiver'
    publisher = 'Igor Pavlov'
    language = 'en-US'
    requirementArchitecture = 'X64'
    installContext = 'System'
    arpDisplayNameMatch = '7-Zip*'
    arpVersionMatch = '24.08'
    msiProductCode = $msiProductCode
    cmdArguments = '/qn'
}

$draft = Invoke-RestMethod -Method Post -Uri "$api/apps/custom/draft" -Headers $headers
$productId = $draft.productId
```
{% endtab %}

{% tab title="curl (Bash)" %}
In Git Bash, use a drive-letter path with forward slashes, such as `C:/Packages/7zip/7z2408-x64.msi`, so Windows curl can open the multipart file.

```bash
installer_path='/path/to/7z2408-x64.msi'
if [[ ! -f "$installer_path" || "$installer_path" != *.msi ]]; then
  echo 'Choose the MSI file for this example.' >&2
  exit 1
fi
file_size=$(wc -c < "$installer_path")
if (( file_size == 0 || file_size >= 32 * 1024 * 1024 )); then
  echo 'This example needs a nonempty MSI smaller than 32 MiB.' >&2
  exit 1
fi
file_name="${installer_path##*/}"
read -r -p 'Product code from this MSI (without braces): ' msi_product_code
display_name="Archive Tool $(openssl rand -hex 16)"
metadata=$(jq -n --arg name "$display_name" --arg msi "$msi_product_code" '{
  displayName: $name,
  description: "File archiver",
  publisher: "Igor Pavlov",
  language: "en-US",
  requirementArchitecture: "X64",
  installContext: "System",
  arpDisplayNameMatch: "7-Zip*",
  arpVersionMatch: "24.08",
  msiProductCode: $msi,
  cmdArguments: "/qn"
}')

draft=$(curl --fail-with-body --silent --show-error --request POST "$api/apps/custom/draft" \
  --header "Authorization: Bearer $access_token")
product_id=$(jq -er '.productId' <<< "$draft")
update_id=$(jq -er '.updateId' <<< "$draft")
revision_id=$(jq -er '.revisionId' <<< "$draft")
```
{% endtab %}
{% endtabs %}

### 3. Upload the installer to the draft

Upload the file before completing the application. Use the draft's `fileUploadPath` for a single-request upload and the same access token you use for application requests. Do not send the raw PAT with the upload. Each command below waits for the upload response. Continue to step 4 only after it succeeds with `201`; do not run completion in parallel with the upload.

The upload path is relative to your regional portal origin, not to `/v1/api`. For example, `api/storageupload/public/applications` becomes `https://us.portal.patchmypc.com/api/storageupload/public/applications`. Use the path returned by the draft rather than the older upload routes.

Send the MSI as `multipart/form-data`. Let the HTTP client set the multipart content type and boundary.

| Form field      | Value for this new-application example                                                                                                                       |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `file`          | The MSI's binary contents. Set its multipart filename to the path relative to the application folder, such as `7z2408-x64.msi`, not the local absolute path. |
| `updateId`      | `updateId` from the draft, not `productId`.                                                                                                                  |
| `revisionId`    | `revisionId` from the same draft; do not assume it is always `1`.                                                                                            |
| `fileType`      | `1`, meaning the main installation file (`Installation`).                                                                                                    |
| `operationType` | `1`, meaning creation of a new application (`Create`).                                                                                                       |
| `sha1Hash`      | SHA-1 of the entire file, encoded as lowercase hexadecimal.                                                                                                  |
| `sha256Hash`    | SHA-256 of the entire file, encoded as lowercase hexadecimal.                                                                                                |
| `scupDigest`    | The SHA-1 hash bytes encoded as Base64, not the hexadecimal text encoded as Base64.                                                                          |

Compute the hashes from the exact file you will send. Do not modify or replace it between hashing and uploading.

{% tabs %}
{% tab title="PowerShell" %}
```powershell
$sha1 = (Get-FileHash -LiteralPath $installerPath -Algorithm SHA1).Hash.ToLowerInvariant()
$sha256 = (Get-FileHash -LiteralPath $installerPath -Algorithm SHA256).Hash.ToLowerInvariant()
$scupDigest = [Convert]::ToBase64String([Convert]::FromHexString($sha1))
$uploadUrl = "$($portal.TrimEnd('/'))/$($draft.fileUploadPath.TrimStart('/'))"

$form = @{
    file = $installer
    updateId = [string]$draft.updateId
    revisionId = [string]$draft.revisionId
    fileType = '1'
    operationType = '1'
    sha1Hash = $sha1
    sha256Hash = $sha256
    scupDigest = $scupDigest
}
$upload = Invoke-WebRequest -Method Post -Uri $uploadUrl -Headers $headers -Form $form
if ($upload.StatusCode -ne 201) {
    throw "Unexpected upload status: $($upload.StatusCode). Do not complete the application."
}

$applicationFile = [ordered]@{
    fileName = $fileName
    fileSize = $installer.Length
    fileType = 'Installation'
    sha1Hash = $sha1
    sha256Hash = $sha256
}
```
{% endtab %}

{% tab title="curl (Bash)" %}
```bash
sha1=$(openssl dgst -sha1 "$installer_path")
sha1="${sha1##* }"
sha256=$(openssl dgst -sha256 "$installer_path")
sha256="${sha256##* }"
scup_digest=$(openssl dgst -sha1 -binary "$installer_path" | openssl base64 -A)
upload_path=$(jq -er '.fileUploadPath' <<< "$draft")
upload_url="${portal%/}/${upload_path#/}"

upload_status=$(curl --fail-with-body --silent --show-error --request POST "$upload_url" \
  --header "Authorization: Bearer $access_token" \
  --form-string "updateId=$update_id" \
  --form-string "revisionId=$revision_id" \
  --form-string 'fileType=1' \
  --form-string 'operationType=1' \
  --form-string "sha1Hash=$sha1" \
  --form-string "sha256Hash=$sha256" \
  --form-string "scupDigest=$scup_digest" \
  --form "file=@$installer_path;filename=$file_name;type=application/octet-stream" \
  --output /dev/null --write-out '%{http_code}')
if [[ "$upload_status" != 201 ]]; then
  echo "Unexpected upload status: $upload_status. Do not complete the application." >&2
  exit 1
fi
```
{% endtab %}
{% endtabs %}

A successful single-request upload returns `201 Created`. That acknowledges the upload; it does not complete the application or prove that processing has finished. Do not call the chunked upload completion path for this single-request upload.

### 4. Complete the application

After the upload succeeds, submit the metadata and the file you just uploaded, keeping all three IDs from the same draft. Completing the application submits its metadata; it does not mean that background processing has finished.

{% tabs %}
{% tab title="PowerShell" %}
```powershell
$completion = $metadata.Clone()
$completion.productId = $productId
$completion.updateId = $draft.updateId
$completion.revisionId = $draft.revisionId
$completion.primaryInstallerFile = $fileName
$completion.files = @($applicationFile)

$created = Invoke-RestMethod -Method Post -Uri "$api/apps/custom/complete" `
    -Headers $headers -ContentType 'application/json' `
    -Body ($completion | ConvertTo-Json -Depth 10)
if ($created.productId -ne $productId -or $created.updateId -ne $draft.updateId -or
    $created.revisionId -ne $draft.revisionId) {
    throw 'The completion response did not identify this draft.'
}
```
{% endtab %}

{% tab title="curl (Bash)" %}
```bash
completion=$(jq --arg product "$product_id" --arg update "$update_id" \
  --argjson revision "$revision_id" --arg file "$file_name" --argjson size "$file_size" \
  --arg sha1 "$sha1" --arg sha256 "$sha256" '. + {
    productId: $product, updateId: $update, revisionId: $revision,
    primaryInstallerFile: $file,
    files: [{fileName: $file, fileSize: $size, fileType: "Installation",
             sha1Hash: $sha1, sha256Hash: $sha256}]
  }' <<< "$metadata")
created=$(curl --fail-with-body --silent --show-error --request POST "$api/apps/custom/complete" \
  --header "Authorization: Bearer $access_token" --header 'Content-Type: application/json' \
  --data "$completion")
jq -e --arg product "$product_id" --arg update "$update_id" --argjson revision "$revision_id" \
  '.productId == $product and .updateId == $update and .revisionId == $revision' \
  <<< "$created" > /dev/null
```
{% endtab %}
{% endtabs %}

### 5. Get the application and its files

After completion, the application may briefly return `404` while background processing finishes and it becomes queryable. Poll for up to two minutes; other errors stop the example. Only continue to the template and deployment steps after the application and file checks pass.

{% tabs %}
{% tab title="PowerShell" %}
```powershell
$deadline = [DateTimeOffset]::UtcNow.AddMinutes(2)
do {
    $response = Invoke-WebRequest -Method Get -Uri "$api/apps/custom/$productId" `
        -Headers $headers -SkipHttpErrorCheck
    if ($response.StatusCode -eq 200) { break }
    if ($response.StatusCode -ne 404) {
        throw "Application read failed: HTTP $($response.StatusCode). $($response.Content)"
    }
    if ([DateTimeOffset]::UtcNow -ge $deadline) {
        throw 'The application is not queryable yet. Keep its product ID before retrying.'
    }
    Start-Sleep -Seconds 5
} while ($true)

$app = $response.Content | ConvertFrom-Json
$files = Invoke-RestMethod -Method Get -Uri "$api/apps/$productId/files" -Headers $headers
if ($app.productId -ne $productId -or $app.type -ne 'custom' -or
    $app.displayName -ne $displayName -or $app.mainFile -ne $fileName -or
    ($app.custom.updateId -and $app.custom.updateId -ne $draft.updateId)) {
    throw 'The application details do not match the application just created.'
}
if (@($files).Count -ne 1 -or $files[0].productId -ne $productId -or
    $files[0].fileName -ne $fileName -or $files[0].fileSize -ne $installer.Length -or
    $files[0].fileType -ne 'Installation' -or
    $files[0].sha1Hash -ne $sha1 -or $files[0].sha256Hash -ne $sha256) {
    throw 'The returned installer metadata does not match the uploaded file.'
}
$catalogEntryId = [guid]$app.custom.catalogEntryId
if ($catalogEntryId -eq [guid]::Empty) {
    throw 'The application details did not return a deployment catalog entry ID.'
}

$app | Select-Object productId, displayName, updateVersion, mainFile
$files | Select-Object fileName, fileSize, sha1Hash, sha256Hash
```
{% endtab %}

{% tab title="curl (Bash)" %}
```bash
deadline=$((SECONDS + 120))
while :; do
  response=$(curl --silent --show-error "$api/apps/custom/$product_id" \
    --header "Authorization: Bearer $access_token" --write-out $'\n%{http_code}')
  status="${response##*$'\n'}"
  app="${response%$'\n'*}"
  if [[ "$status" == 200 ]]; then break; fi
  if [[ "$status" != 404 ]]; then
    printf 'Application read failed: HTTP %s. %s\n' "$status" "$app" >&2
    exit 1
  fi
  if (( SECONDS >= deadline )); then
    echo "The application is not queryable yet. Keep product ID $product_id before retrying." >&2
    exit 1
  fi
  sleep 5
done

files=$(curl --fail-with-body --silent --show-error "$api/apps/$product_id/files" \
  --header "Authorization: Bearer $access_token")
jq -e --arg product "$product_id" --arg name "$display_name" --arg file "$file_name" \
  --arg update "$update_id" \
  '.productId == $product and .type == "custom" and .displayName == $name and
   .mainFile == $file and (.custom.updateId == null or .custom.updateId == $update)' \
  <<< "$app" > /dev/null
jq -e --arg product "$product_id" --arg file "$file_name" --argjson size "$file_size" \
  --arg sha1 "$sha1" --arg sha256 "$sha256" \
  'length == 1 and .[0].productId == $product and .[0].fileName == $file and
   .[0].fileSize == $size and .[0].fileType == "Installation" and
   (.[0].sha1Hash | ascii_downcase) == $sha1 and
   (.[0].sha256Hash | ascii_downcase) == $sha256' <<< "$files" > /dev/null
catalog_entry_id=$(jq -er '.custom.catalogEntryId |
  select(type == "string" and length > 0 and . != "00000000-0000-0000-0000-000000000000")' <<< "$app")

jq '{productId, displayName, updateVersion, mainFile}' <<< "$app"
jq '.[] | {fileName, fileSize, sha1Hash, sha256Hash}' <<< "$files"
```
{% endtab %}
{% endtabs %}

Keep the product ID, catalog entry ID and connection ID for deployment, along with the draft's update ID; application details can omit `custom.updateId`. These checks compare the returned file metadata with your local file, not downloaded stored bytes, and do not prove installation on a device.

### 6. Create a deployment template

Create a uniquely named Windows template on the connection you selected. This example enables Company Portal uninstall and retains two previous application versions in Intune. Keep `isDefault: false` so you do not change the connection's default template.

{% tabs %}
{% tab title="PowerShell" %}
```powershell
$templateName = "$displayName template"
$templateRequest = @{
    connectionId = $connectionId
    templateName = $templateName
    osType = 'Windows'
    isDefault = $false
    allowAvailableUninstall = $true
    appVersionsRetention = 2
}
$newTemplate = Invoke-RestMethod -Method Post -Uri "$api/deployments/templates" `
    -Headers $headers -ContentType 'application/json' `
    -Body ($templateRequest | ConvertTo-Json)
$templateId = $newTemplate.deploymentTemplateId
if ([string]::IsNullOrWhiteSpace($templateId)) {
    throw 'The template creation response did not return a template ID.'
}
```
{% endtab %}

{% tab title="curl (Bash)" %}
```bash
template_name="$display_name template"
template_request=$(jq -n --arg connection "$connection_id" --arg name "$template_name" '{
  connectionId: $connection, templateName: $name, osType: "Windows",
  isDefault: false, allowAvailableUninstall: true, appVersionsRetention: 2
}')
new_template=$(curl --fail-with-body --silent --show-error --request POST "$api/deployments/templates" \
  --header "Authorization: Bearer $access_token" --header 'Content-Type: application/json' \
  --data "$template_request")
template_id=$(jq -er '.deploymentTemplateId | select(type == "string" and length > 0)' <<< "$new_template")
```
{% endtab %}
{% endtabs %}

### 7. Get the template

Retrieve the exact template on the same connection. Use this read-back, rather than the original create request, as the source of settings for your deployment.

{% tabs %}
{% tab title="PowerShell" %}
```powershell
$template = Invoke-RestMethod -Method Get `
    -Uri "$api/deployments/templates/${templateId}?connectionId=$connectionId" -Headers $headers
if ($template.deploymentTemplateId -ne $templateId -or $template.templateName -ne $templateName -or
    $template.osType -ne 'Windows' -or $template.isDefault -ne $false -or
    $template.allowAvailableUninstall -ne $true -or $template.appVersionsRetention -ne 2) {
    throw 'The returned template does not match the template just created.'
}
```
{% endtab %}

{% tab title="curl (Bash)" %}
```bash
template=$(curl --fail-with-body --silent --show-error \
  "$api/deployments/templates/$template_id?connectionId=$connection_id" \
  --header "Authorization: Bearer $access_token")
jq -e --arg id "$template_id" --arg name "$template_name" \
  '.deploymentTemplateId == $id and .templateName == $name and .osType == "Windows" and
   .isDefault == false and .allowAvailableUninstall == true and .appVersionsRetention == 2' \
  <<< "$template" > /dev/null
```
{% endtab %}
{% endtabs %}

### 8. Deploy the application using the template's settings

Enter an approved test group's Microsoft Entra object ID. `Required` installs the application on devices targeted by that group; do not use All Users or All Devices for this walkthrough.

REST deployment creation does not take a template ID. Copy the settings you want from the retrieved template into the deployment request. This example copies only retention and Company Portal uninstall; it does not apply every template field. The `catalogEntryId` comes from the application details in step 5, not the draft's update ID.

{% tabs %}
{% tab title="PowerShell" %}
```powershell
$groupId = [guid](Read-Host 'Approved test group ID')
if ($groupId -eq [guid]::Empty -or $groupId -in @(
    'acacacac-9df4-4c7d-9d50-4ef0226f57a9', 'adadadad-808e-44e2-905a-0b7873a8a531')) {
    throw 'Use an approved test group, not All Users or All Devices.'
}
$deploymentRequest = @{
    connectionId = $connectionId
    catalogEntryId = $catalogEntryId
    osType = $template.osType
    assignments = @(@{ groupId = [string]$groupId; intent = 'Required'; targetType = 'Group' })
    configuration = @{
        appVersionsRetention = $template.appVersionsRetention
        allowAvailableUninstall = $template.allowAvailableUninstall
    }
}
$newDeployment = Invoke-RestMethod -Method Post -Uri "$api/apps/$productId/deployments" `
    -Headers $headers -ContentType 'application/json' `
    -Body ($deploymentRequest | ConvertTo-Json -Depth 10)
$deploymentId = $newDeployment.deploymentId
if ([string]::IsNullOrWhiteSpace($deploymentId) -or $newDeployment.productId -ne $productId -or
    $newDeployment.catalogEntryId -ne $catalogEntryId -or $newDeployment.osType -ne 'Windows') {
    throw 'The deployment creation response does not identify this application and catalog entry.'
}
```
{% endtab %}

{% tab title="curl (Bash)" %}
```bash
read -r -p 'Approved test group ID: ' group_id
case "${group_id,,}" in
  ''|00000000-0000-0000-0000-000000000000|acacacac-9df4-4c7d-9d50-4ef0226f57a9|adadadad-808e-44e2-905a-0b7873a8a531)
    echo 'Use an approved test group, not All Users or All Devices.' >&2
    exit 1
    ;;
esac
deployment_request=$(jq --arg connection "$connection_id" --arg catalog "$catalog_entry_id" \
  --arg group "$group_id" '{
    connectionId: $connection, catalogEntryId: $catalog, osType: .osType,
    assignments: [{groupId: $group, intent: "Required", targetType: "Group"}],
    configuration: {appVersionsRetention: .appVersionsRetention,
                    allowAvailableUninstall: .allowAvailableUninstall}
  }' <<< "$template")
new_deployment=$(curl --fail-with-body --silent --show-error --request POST \
  "$api/apps/$product_id/deployments" \
  --header "Authorization: Bearer $access_token" --header 'Content-Type: application/json' \
  --data "$deployment_request")
deployment_id=$(jq -er '.deploymentId | select(type == "string" and length > 0)' <<< "$new_deployment")
jq -e --arg product "$product_id" --arg catalog "$catalog_entry_id" \
  '.productId == $product and .catalogEntryId == $catalog and .osType == "Windows"' \
  <<< "$new_deployment" > /dev/null
```
{% endtab %}
{% endtabs %}

### 9. Get the deployment and wait for publication

Read the exact product/deployment pair with the selected `connectionId`. Creation starts asynchronously; poll for up to ten minutes, then inspect `status` and `errorMessages` before retrying with the same deployment ID.

{% tabs %}
{% tab title="PowerShell" %}
```powershell
$deadline = [DateTimeOffset]::UtcNow.AddMinutes(10)
$deploymentUri = "$api/apps/$productId/deployments/${deploymentId}?connectionId=$connectionId"
do {
    $deployment = Invoke-RestMethod -Method Get -Uri $deploymentUri -Headers $headers
    if ($deployment.status -eq 'Success') { break }
    if ($deployment.status -notin @('InProgress', 'Retrying') -or
        [DateTimeOffset]::UtcNow -ge $deadline) {
        throw "Deployment $deploymentId status: $($deployment.status). $($deployment.errorMessages -join '; ')"
    }
    Start-Sleep -Seconds 10
} while ($true)

if ($deployment.deploymentId -ne $deploymentId -or $deployment.productId -ne $productId -or
    $deployment.catalogEntryId -ne $catalogEntryId -or $deployment.osType -ne 'Windows' -or
    @($deployment.assignments).Count -ne 1 -or $deployment.assignments[0].groupId -ne $groupId -or
    $deployment.assignments[0].targetType -ne 'Group' -or $deployment.assignments[0].intent -ne 'Required' -or
    $deployment.configuration.appVersionsRetention -ne $template.appVersionsRetention -or
    $deployment.configuration.allowAvailableUninstall -ne $template.allowAvailableUninstall) {
    throw 'The deployment does not match the application, targeting or selected template settings.'
}
$deployment | Select-Object deploymentId, displayName, status, version, warningMessages
```
{% endtab %}

{% tab title="curl (Bash)" %}
```bash
deadline=$((SECONDS + 600))
deployment_url="$api/apps/$product_id/deployments/$deployment_id?connectionId=$connection_id"
while :; do
  deployment=$(curl --fail-with-body --silent --show-error "$deployment_url" \
    --header "Authorization: Bearer $access_token")
  status=$(jq -er '.status' <<< "$deployment")
  if [[ "$status" == Success ]]; then break; fi
  if [[ "$status" != InProgress && "$status" != Retrying ]] || (( SECONDS >= deadline )); then
    printf 'Deployment %s status: %s\n' "$deployment_id" "$status" >&2
    jq '.errorMessages' <<< "$deployment" >&2
    exit 1
  fi
  sleep 10
done

jq -e --arg id "$deployment_id" --arg product "$product_id" --arg catalog "$catalog_entry_id" \
  --arg group "$group_id" --argjson template "$template" \
  '.deploymentId == $id and .productId == $product and .catalogEntryId == $catalog and
   .osType == "Windows" and (.assignments | length) == 1 and
   .assignments[0].groupId == $group and .assignments[0].targetType == "Group" and
   .assignments[0].intent == "Required" and
   .configuration.appVersionsRetention == $template.appVersionsRetention and
   .configuration.allowAvailableUninstall == $template.allowAvailableUninstall' \
  <<< "$deployment" > /dev/null
jq '{deploymentId, displayName, status, version, warningMessages}' <<< "$deployment"
```
{% endtab %}
{% endtabs %}

`Success` confirms publication to Intune, not installation on a device. Review any `warningMessages`; keep the product, template and deployment IDs for later management.

### Upload troubleshooting

Upload filenames must be folder-relative paths using `/` between folders. Absolute paths, backslashes, empty path segments and `.` or `..` segments are not accepted. The upload only works for an eligible draft revision belonging to the access token's company.

| Status                    | Meaning for this upload                                                                                                                                |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `400 Bad Request`         | The request has invalid or missing upload metadata, a disallowed filename or an unsupported installation file. Check the response before trying again. |
| `401 Unauthorized`        | The access token is missing, invalid or expired. Use a valid token from the PAT exchange.                                                              |
| `403 Forbidden`           | The access token lacks permission to upload, including the required `appcatbroker:apps:write` scope.                                                   |
| `404 Not Found`           | No eligible draft revision is available for this token and update/revision pair. Check the draft IDs and company.                                      |
| `409 Conflict`            | The upload conflicts with stored file metadata or has already completed processing for this draft revision. Do not repeatedly overwrite it.            |
| `503 Service Unavailable` | Draft eligibility could not be checked. Do not assume the draft is invalid or complete the application without a successful upload.                    |

---
description: >-
  Upload an installer and its files to create a custom application with the
  Patch My PC Cloud Customer API.
noIndex: true
noRobotsIndex: true
---

# Create a custom application

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

A custom application is an application your company packages and uploads itself, rather than one Patch My PC maintains in its catalog. You create one by uploading a folder that contains the installer and any supporting files, and describing how the application installs and how it's detected.

The .NET SDK and the PowerShell module do the whole job in one call: they validate the folder, compute file hashes, upload the files in chunks, and complete the application. With REST you perform each of those steps yourself, so we recommend the SDK or the module for creating applications.

This guide covers the SDK, PowerShell module, and a direct REST example using PowerShell. For curl (Bash) or the complete deployment workflow, follow [Create and deploy a custom application with REST](https://docs.patchmypc.com/patch-my-pc-cloud-api/guides/create-a-custom-application-with-rest). See the [REST API reference](https://docs.patchmypc.com/patch-my-pc-cloud-api/rest-api) for individual operations.

## Before you begin

* Exchange a personal access token (PAT) for an access token. See [Authentication](https://docs.patchmypc.com/patch-my-pc-cloud-api/authentication).
* A PAT needs the `appcatbroker:apps:write` scope, plus `appcatbroker:apps:read` to verify the result.
* Check that your account has room for another custom application. Your account information lists your usage and limits—see [Getting started](https://docs.patchmypc.com/patch-my-pc-cloud-api/getting-started). When you're at your limit, creating the application fails with `400 Bad Request`.
* Choose a display name that does not conflict with an application already available to your company.

## Step 1: Prepare the application folder

1. Create a folder that contains the primary installer and every file the installation needs. Every file in the folder is uploaded.
2. Keep the folder within the upload limits: up to 1,000 files and 30 GB in total.
3. Decide how the application will be detected after installation:
   * For an MSI installer, use its MSI product code.
   * For other installers, use the Add or Remove Programs display name and version, or supply custom detection rules.
4. Optionally, prepare an icon file.

## Step 2: Create the application

{% tabs %}
{% tab title="C#" %}
`CreateApplicationAsync` validates the folder, uploads the files, and completes the application. Pass an `IProgress<UploadProgress>` to report progress.

{% code title="Program.cs" collapsedlinecount="10" %}
```csharp
using PatchMyPC.Cloud.Models;
using PatchMyPC.Cloud.Client;

var metadata = new ApplicationMetadata
{
    FolderPath = @"C:\Packages\7zip",
    PrimaryInstallerFile = "7z2408-x64.msi",
    DisplayName = $"Contoso Archive Tool {Guid.NewGuid():N}",
    Description = "Sample file archiver",
    Publisher = "Contoso",
    Architecture = RequirementArchitecture.X64,
    Language = "en-US",
    InstallContext = InstallationBehavior.System,
    ArpDisplayNameMatch = "7-Zip*",
    ArpVersionMatch = "24.08",
    MsiProductCode = Guid.Parse("{msi-product-code}"),
    CmdArguments = "/qn"
};

var progress = new Progress<UploadProgress>(p =>
    Console.WriteLine($"{p.Stage}: {p.FileName} {p.BytesUploadedOverall}/{p.TotalBytesOverall} bytes"));

var created = await client.CreateApplicationAsync(metadata, progress: progress);
if (created.IsFailure)
{
    Console.WriteLine($"{created.Error.Code}: {created.Error.Message}");
    return;
}

Console.WriteLine($"Created product {created.Value.ProductId}, version {created.Value.UpdateId}");
Console.WriteLine($"Uploaded {created.Value.FilesUploaded} file(s) in {created.Value.Duration}");
```
{% endcode %}

The example omits an icon. To include one, set `IconPath` to an image file; if that file can't be uploaded, the application is still created without an icon.

See [CreateApplicationAsync](../sdk/applications.md#createapplicationasync).
{% endtab %}

{% tab title="PowerShell" %}
{% code collapsedlinecount="10" %}
```powershell
$displayName = "Contoso Archive Tool $([guid]::NewGuid().ToString('N'))"
$app = New-PmpcCustomApplication `
    -FolderPath 'C:\Packages\7zip' `
    -PrimaryInstallerFile '7z2408-x64.msi' `
    -DisplayName $displayName `
    -Description 'Sample file archiver' `
    -Publisher 'Contoso' `
    -MsiProductCode '{msi-product-code}' `
    -CmdArguments '/qn' `
    -ArpDisplayNameMatch '7-Zip*' `
    -ArpVersionMatch '24.08'

[pscustomobject]@{
    ProductId = $app.ProductId
    UpdateId = $app.UpdateId
}
```
{% endcode %}

`-IconPath` is optional and omitted here; pass an image path to include an icon. `New-PmpcCustomApplication` supports `-WhatIf` and `-Confirm`.

See [New-PmpcCustomApplication](../powershell/new-pmpccustomapplication.md).
{% endtab %}

{% tab title="REST (PowerShell)" %}
This example sends HTTP requests directly from PowerShell 7.4 or later; it does not use the module. It uploads **one nonempty Windows x64 MSI smaller than 32 MiB**, without supporting files or an icon. The larger folder limits above apply to the SDK/module, not this single-request example.

Set `PMPC_PAT` from your secret store and select your regional portal. Replace the installer path and metadata with your MSI's actual values; the sample describes 7-Zip 24.08. Keep this shell session open for the REST verification in step 3.

{% code collapsedlinecount="10" %}
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
$sha1 = (Get-FileHash -LiteralPath $installerPath -Algorithm SHA1).Hash.ToLowerInvariant()
$sha256 = (Get-FileHash -LiteralPath $installerPath -Algorithm SHA256).Hash.ToLowerInvariant()
$scupDigest = [Convert]::ToBase64String([Convert]::FromHexString($sha1))

$draft = Invoke-RestMethod -Method Post -Uri "$api/apps/custom/draft" -Headers $headers
$productId = $draft.productId
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
$created | Select-Object productId, updateId, revisionId
```
{% endcode %}

Upload to the draft's returned `fileUploadPath`, relative to the portal origin, using the **access token**, not the PAT. Let `-Form` set the multipart content type and boundary. `fileType = '1'` identifies the main installer and `operationType = '1'` creates an application. `scupDigest` is the SHA-1 bytes encoded as Base64, not the hexadecimal text encoded as Base64. The upload must finish with `201` before completion; a completion response is not proof that background processing has finished. Do not retry creation blindly after a later error: retain the returned product ID and check its details first.
{% endtab %}
{% endtabs %}

## Step 3: Verify the application

1. Read the custom application's details with the product ID you received.
2. Check the display name, version, and primary installer. Retain `updateId` from the creation response; the details may also return it as `custom.updateId`. Use `custom.catalogEntryId` when creating a deployment.

{% tabs %}
{% tab title="C#" %}
{% code collapsedlinecount="10" %}
```csharp
var details = await client.GetCustomApplicationDetailsAsync(created.Value.ProductId);
if (details.IsSuccess)
{
    Console.WriteLine($"Version ID: {details.Value.Custom?.UpdateId}");
    Console.WriteLine($"Deployment entry ID: {details.Value.Custom?.CatalogEntryId}");
}
```
{% endcode %}

See [GetCustomApplicationDetailsAsync](../sdk/custom-applications.md#getcustomapplicationdetailsasync).
{% endtab %}

{% tab title="PowerShell" %}
{% code collapsedlinecount="10" %}
```powershell
$details = Get-PmpcCustomApplication -ProductId '{product-id}'
$details | Select-Object DisplayName, UpdateVersion, @{ Name = 'UpdateId'; Expression = { $_.Custom.UpdateId } }, @{ Name = 'CatalogEntryId'; Expression = { $_.Custom.CatalogEntryId } }
```
{% endcode %}

See [Get-PmpcCustomApplication](../powershell/get-pmpccustomapplication.md).
{% endtab %}

{% tab title="REST (PowerShell)" %}
Continue in the same shell session. A newly completed application may briefly return `404`; poll for up to two minutes, stopping on any other error. Check the returned installer metadata against the exact file uploaded in step 2.

{% code collapsedlinecount="10" %}
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
{% endcode %}

The checks compare the API's stored file metadata, not a downloaded copy of the binary. The application remains available in your company; this example does not create a deployment or install anything on a device. Exchange the PAT again when the access token expires.
{% endtab %}
{% endtabs %}

## Related pages

* [Update an application](update-an-application.md)
* [Deploy an application](deploy-an-application.md)
* [Search the catalog](search-the-catalog.md)
* [Errors](../errors.md)

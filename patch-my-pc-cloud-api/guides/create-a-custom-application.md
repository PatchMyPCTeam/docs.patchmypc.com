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

## Before you begin

* Exchange a personal access token (PAT) for an access token. See [Authentication](../authentication.md).
* The REST examples use the US host, `https://us.portal.patchmypc.com`. If your account is hosted in the EU, use `https://eu.portal.patchmypc.com` instead.
* A PAT needs the `appcatbroker:apps:write` scope.
* Check that your account has room for another custom application. Your account information lists your usage and limits—see [Getting started](../getting-started.md). When you're at your limit, creating the application fails with `400 Bad Request`.

## Step 1: Prepare the application folder

1. Create a folder that contains the primary installer and every file the installation needs. Every file in the folder is uploaded.
2. Keep the folder within the upload limits: up to 1,000 files and 30 GB in total.
3. Decide how the application will be detected after installation:
   * For an MSI installer, use its MSI product code.
   * For other installers, use the Add or Remove Programs display name and version, or supply custom detection rules.
4. Optionally, prepare an icon file.

## Step 2: Create the application

{% tabs %}
{% tab title="REST" %}
Creating an application over REST takes three stages.

1. Create a draft. The request has no body.

```http
POST https://us.portal.patchmypc.com/v1/api/apps/draft
Authorization: Bearer {access-token}
Accept: application/json
```

The response identifies the new application and returns the paths to upload its files to:

```json
{
  "productId": "{product-id}",
  "updateId": "{update-id}",
  "revisionId": 1,
  "displayName": "",
  "customerId": "{customer-id}",
  "fileUploadPath": "{file-upload-path}",
  "chunkedFileUploadPath": "{chunked-file-upload-path}",
  "fileCompleteUploadPath": "{file-complete-upload-path}"
}
```

2. Upload each file to the paths the draft returned. Small files can be sent in a single request; larger files are sent in chunks and then finalized with a separate request. Each file is verified against its SHA-1 and SHA-256 hashes. Because this involves chunking, hashing, and retries, we recommend the SDK or PowerShell module for uploads.
3. Complete the application. Send the IDs from the draft, the application's details, and the list of files you uploaded.

```http
POST https://us.portal.patchmypc.com/v1/api/apps/complete
Authorization: Bearer {access-token}
Content-Type: application/json

{
  "productId": "{product-id}",
  "updateId": "{update-id}",
  "revisionId": 1,
  "displayName": "Contoso Agent",
  "description": "Endpoint agent for Contoso services.",
  "publisher": "Contoso",
  "language": "en-US",
  "installContext": "System",
  "primaryInstallerFile": "ContosoAgent.msi",
  "msiProductCode": "{msi-product-code}",
  "files": [
    {
      "productId": "{product-id}",
      "fileName": "ContosoAgent.msi",
      "fileSize": 52428800,
      "fileType": "{file-type}",
      "sha1Hash": "{sha1-hash}",
      "sha256Hash": "{sha256-hash}"
    }
  ]
}
```

Completing an application can take up to a minute.

See [Create application draft](../rest-api/applications.md#create-application-draft) and [Complete application creation](../rest-api/applications.md#complete-application-creation) for every field.
{% endtab %}

{% tab title="C#" %}
`CreateApplicationAsync` validates the folder, uploads the files, and completes the application. Pass an `IProgress<UploadProgress>` to report progress.

{% code title="Program.cs" %}
```csharp
using pmpc.appcatbroker.sdk.Models;
using static pmpc.common.Enums;

var metadata = new ApplicationMetadata
{
    FolderPath = @"C:\Packages\ContosoAgent",
    PrimaryInstallerFile = "ContosoAgent.msi",
    DisplayName = "Contoso Agent",
    Description = "Endpoint agent for Contoso services.",
    Publisher = "Contoso",
    Architecture = RequirementArchitecture.X64,
    Language = "en-US",
    InstallContext = InstallationBehavior.System,
    MsiProductCode = Guid.Parse("{msi-product-code}"),
    IconPath = @"C:\Packages\ContosoAgent.png"
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

If the icon can't be uploaded, the application is still created, without an icon.

See [CreateApplicationAsync](../sdk/applications.md#createapplicationasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
$app = New-PmpcCustomApplication `
    -FolderPath 'C:\Packages\ContosoAgent' `
    -PrimaryInstallerFile 'ContosoAgent.msi' `
    -DisplayName 'Contoso Agent' `
    -Description 'Endpoint agent for Contoso services.' `
    -Publisher 'Contoso' `
    -MsiProductCode '{msi-product-code}' `
    -IconPath 'C:\Packages\ContosoAgent.png'

$app.ProductId
$app.UpdateId
```

`New-PmpcCustomApplication` supports `-WhatIf` and `-Confirm`. It uses an operation that must be enabled for your account; until it is, the cmdlet reports the error code `FEATURE_NOT_ENABLED`.

See [New-PmpcCustomApplication](../powershell/new-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Step 3: Verify the application

1. Read the new application's details with the product ID you received.
2. Check the display name, version, and primary installer.

{% tabs %}
{% tab title="REST" %}
```http
GET https://us.portal.patchmypc.com/v1/api/apps/{product-id}
Authorization: Bearer {access-token}
Accept: application/json
```

See [Get application details](../rest-api/applications.md#get-application-details).
{% endtab %}

{% tab title="C#" %}
```csharp
var details = await client.GetApplicationDetailsAsync(created.Value.ProductId);
```

See [GetApplicationDetailsAsync](../sdk/applications.md#getapplicationdetailsasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcCustomApplication -ProductId $app.ProductId
```

See [Get-PmpcCustomApplication](../powershell/get-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Related pages

* [Update an application](update-an-application.md)
* [Deploy an application](deploy-an-application.md)
* [Search the catalog](search-the-catalog.md)
* [Errors](../errors.md)

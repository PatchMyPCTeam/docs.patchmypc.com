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

This guide covers the SDK and PowerShell module. For direct HTTP requests, follow [Create and deploy a custom application with REST](https://docs.patchmypc.com/patch-my-pc-cloud-api/guides/create-a-custom-application-with-rest), which carries the returned IDs through upload, completion, and deployment. See the [REST API reference](https://docs.patchmypc.com/patch-my-pc-cloud-api/rest-api) for individual operations.

## Before you begin

* Exchange a personal access token (PAT) for an access token. See [Authentication](../authentication.md).
* A PAT needs the `appcatbroker:apps:write` scope.
* Check that your account has room for another custom application. Your account information lists your usage and limits—see [Getting started](../getting-started.md). When you're at your limit, creating the application fails with `400 Bad Request`.
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

`-IconPath` is optional and omitted here; pass an image path to include an icon. `New-PmpcCustomApplication` supports `-WhatIf` and `-Confirm`. It uses an operation that must be enabled for your account; until it is, the cmdlet reports the error code `FEATURE_NOT_ENABLED`.

See [New-PmpcCustomApplication](../powershell/new-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Step 3: Verify the application

1. Read the custom application's details with the product ID you received.
2. Check the display name, version, and primary installer. The detail response carries custom identity in `custom`: use `custom.updateId` as the canonical version ID, and use `custom.catalogEntryId` when creating a deployment.

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
{% endtabs %}

## Related pages

* [Update an application](update-an-application.md)
* [Deploy an application](deploy-an-application.md)
* [Search the catalog](search-the-catalog.md)
* [Errors](../errors.md)

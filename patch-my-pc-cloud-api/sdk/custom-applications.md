---
description: >-
  SDK methods that target your custom applications explicitly—search, details,
  create, update, edit, and delete.
noIndex: true
noRobotsIndex: true
---

# Custom applications

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

These methods work only with your custom applications—applications you package and upload yourself. They behave like the general methods on [Applications](applications.md), but always target your custom applications catalog, and they add the ability to delete an application.

All of these methods need an authenticated session. For details, see [SDK authentication methods](authentication.md). Search and read methods need the `appcatbroker:apps:read` scope, and create, update, edit, and delete methods need `appcatbroker:apps:write`.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

Every method on this page requires the feature described above.

## Models

These methods use the models described on [Applications](applications.md): the [search filter](applications.md#search-filter), [search results](applications.md#search-results), [application metadata](applications.md#application-metadata), [edit metadata](applications.md#edit-metadata), and [upload result and progress](applications.md#upload-result-and-progress).

### Custom application details

`CustomApplicationDto` (namespace `PatchMyPC.Cloud.Client`) describes one of your custom applications in full. It has the descriptive properties of a public catalog application—`ProductId`, `Type`, `DisplayName`, `Description`, `Language`, `VendorName`, `UpdateVersion`, the icon properties, `PrivacyUrl`, `InformationUrl`, `Developer`, `IntuneNotes`, `InstallerType`, `Architecture`, `InstallContext`, and `Actions`—plus these packaging details.

| Property                                             | Type                   | Description                                                                                                                                                                                                                                                                                                       |
| ---------------------------------------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `MainFile`                                           | `string?`              | The primary installer file.                                                                                                                                                                                                                                                                                       |
| `SilentInstallArguments`, `SilentUninstallArguments` | `string?`              | The silent install and uninstall arguments.                                                                                                                                                                                                                                                                       |
| `ConflictingProcessList`                             | collection of `string` | Processes that block installation while running.                                                                                                                                                                                                                                                                  |
| `DetectionRules`                                     | object                 | How Intune detects that the application is installed.                                                                                                                                                                                                                                                             |
| `CustomRequirements`                                 | object                 | The installation requirements.                                                                                                                                                                                                                                                                                    |
| `ArpDisplayNameMatch`, `ArpVersionMatch`             | `string?`              | The Add or Remove Programs display name and version to match. Both are required when you create an application, and `ArpVersionMatch` is required when you update one. `ArpVersionMatch` is a version number with two to four parts separated by dots, such as `24.08` or `1.2.3.4`, and can't contain wildcards. |
| `MsiProductCode`                                     | `Guid?`                | The MSI product code, for MSI installers.                                                                                                                                                                                                                                                                         |
| `Notes`, `Owner`                                     | `string?`              | Additional information.                                                                                                                                                                                                                                                                                           |
| `IsMigrationApp`                                     | `bool?`                | Whether the application was migrated from another system.                                                                                                                                                                                                                                                         |

## Methods

### SearchCustomApplicationsAsync

Searches your custom applications.

```csharp
Task<Result<ProductFilterResponse>> SearchCustomApplicationsAsync(
    ProductFilterRequest filterRequest,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                                                    | Description                                                                                               |
| ------------------- | ------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `filterRequest`     | [`ProductFilterRequest`](applications.md#search-filter) | Required. The search criteria. `FeedTypes` is ignored; the search always covers your custom applications. |
| `cancellationToken` | `CancellationToken`                                     | Optional. Cancels the call.                                                                               |

**Returns:** a [`ProductFilterResponse`](applications.md#search-results) with one page of results.

```csharp
var search = await client.SearchCustomApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "{search-text}",
    Skip = 0,
    Limit = 50
});

if (search.IsFailure)
{
    Console.WriteLine($"Search failed: {search.Error.Code} {search.Error.Message}");
    return;
}

foreach (var product in search.Value.Products)
{
    Console.WriteLine($"{product.DisplayName} {product.Version} ({product.ProductId}, latest version {product.UpdateId})");
}
```

**See also:** [Find-PmpcCustomApplication](../powershell/find-pmpccustomapplication.md) and [Search custom applications](../rest-api/applications.md#search-custom-applications).

### GetCustomApplicationDetailsAsync

Gets the full details of one of your custom applications.

```csharp
Task<Result<CustomApplicationDto>> GetCustomApplicationDetailsAsync(
    Guid productId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                   |
| ------------------- | ------------------- | ----------------------------- |
| `productId`         | `Guid`              | Required. The application ID. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.   |

**Returns:** a [`CustomApplicationDto`](custom-applications.md#custom-application-details). If the application doesn't exist, the error code is `NOT_FOUND`. The details don't include the file list; use [`GetApplicationFilesAsync`](applications.md#getapplicationfilesasync) for that.

```csharp
var details = await client.GetCustomApplicationDetailsAsync(productId);
if (details.IsFailure)
{
    Console.WriteLine($"Couldn't read the application: {details.Error.Code} {details.Error.Message}");
    return;
}

var app = details.Value;
Console.WriteLine($"{app.DisplayName} {app.UpdateVersion}");
Console.WriteLine($"Installer: {app.MainFile} {app.SilentInstallArguments}");
```

**See also:** [Get-PmpcCustomApplication](../powershell/get-pmpccustomapplication.md) and [Get custom application details](../rest-api/applications.md#get-custom-application-details).

### CreateCustomApplicationAsync

Creates a custom application and uploads its files in one call.

```csharp
Task<Result<ApplicationData>> CreateCustomApplicationAsync(
    ApplicationMetadata metadata,
    ChunkUploadOptions? uploadOptions = null,
    IProgress<UploadProgress>? progress = null,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                                                          | Description                                                                       |
| ------------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `metadata`          | [`ApplicationMetadata`](applications.md#application-metadata) | Required. The application details and the folder to upload.                       |
| `uploadOptions`     | `ChunkUploadOptions?`                                         | Optional. Upload tuning. `null` uses the defaults.                                |
| `progress`          | `IProgress<UploadProgress>?`                                  | Optional. Receives [upload progress](applications.md#upload-result-and-progress). |
| `cancellationToken` | `CancellationToken`                                           | Optional. Cancels the upload.                                                     |

**Returns:** an [`ApplicationData`](applications.md#upload-result-and-progress) with the new application's `ProductId` and `UpdateId`.

Each new application counts against your custom application limit. If you've reached the limit, the method fails with `VALIDATION_ERROR`. To free a slot, delete an application with [`DeleteCustomApplicationAsync`](custom-applications.md#deletecustomapplicationasync).

```csharp
using PatchMyPC.Cloud.Models;
using PatchMyPC.Cloud.Client;

var created = await client.CreateCustomApplicationAsync(
    new ApplicationMetadata
    {
        FolderPath = @"{path-to-folder}",
        PrimaryInstallerFile = "{installer-file-name}.exe",
        DisplayName = "{display-name}",
        Description = "{description}",
        Publisher = "{publisher}",
        Architecture = RequirementArchitecture.X64,
        CmdArguments = "/S",
        SilentUninstallArg = "/S",
        ArpDisplayNameMatch = "{display-name}",
        ArpVersionMatch = "{version}"
    },
    uploadOptions: new ChunkUploadOptions { MaxFileConcurrency = 4 });

if (created.IsFailure)
{
    Console.WriteLine($"Create failed: {created.Error.Code} {created.Error.Message}");
    return;
}

Console.WriteLine($"Created {created.Value.ProductId}: {created.Value.FilesUploaded} files uploaded");
```

**See also:** [New-PmpcCustomApplication](../powershell/new-pmpccustomapplication.md), [Create custom application draft](../rest-api/applications.md#create-custom-application-draft), and [Complete custom application creation](../rest-api/applications.md#complete-custom-application-creation).

### UpdateCustomApplicationAsync

Publishes a new version of one of your custom applications and uploads its files.

```csharp
Task<Result<ApplicationData>> UpdateCustomApplicationAsync(
    ApplicationUpdateMetadata updateMetadata,
    ChunkUploadOptions? uploadOptions = null,
    IProgress<UploadProgress>? progress = null,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                                                                | Description                                                                           |
| ------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `updateMetadata`    | [`ApplicationUpdateMetadata`](applications.md#application-metadata) | Required. The application, the version the new one follows, and the folder to upload. |
| `uploadOptions`     | `ChunkUploadOptions?`                                               | Optional. Upload tuning. `null` uses the defaults.                                    |
| `progress`          | `IProgress<UploadProgress>?`                                        | Optional. Receives [upload progress](applications.md#upload-result-and-progress).     |
| `cancellationToken` | `CancellationToken`                                                 | Optional. Cancels the upload.                                                         |

**Returns:** an [`ApplicationData`](applications.md#upload-result-and-progress) with the new version's `UpdateId`.

```csharp
var update = await client.UpdateCustomApplicationAsync(new ApplicationUpdateMetadata
{
    ProductId = product.ProductId,
    UpdateId = product.UpdateId,
    FolderPath = @"{path-to-new-version}",
    PrimaryInstallerFile = "{installer-file-name}.exe",
    CmdArguments = "/S",
    ArpVersionMatch = "{version}"
});

if (update.IsFailure)
{
    Console.WriteLine($"Update failed: {update.Error.Code} {update.Error.Message}");
    return;
}

Console.WriteLine($"Published version {update.Value.UpdateId}");
```

**See also:** [Update-PmpcCustomApplication](../powershell/update-pmpccustomapplication.md), [Create custom update draft](../rest-api/applications.md#create-custom-update-draft), and [Complete custom application update](../rest-api/applications.md#complete-custom-application-update).

### EditCustomApplicationAsync

Corrects a custom application's current version in place, without publishing a new version.

```csharp
Task<Result<ApplicationData>> EditCustomApplicationAsync(
    ApplicationEditMetadata editMetadata,
    ChunkUploadOptions? uploadOptions = null,
    IProgress<UploadProgress>? progress = null,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                                                       | Description                                                                       |
| ------------------- | ---------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `editMetadata`      | [`ApplicationEditMetadata`](applications.md#edit-metadata) | Required. The changes to make. `null` properties keep their current value.        |
| `uploadOptions`     | `ChunkUploadOptions?`                                      | Optional. Upload tuning. Ignored when no files change.                            |
| `progress`          | `IProgress<UploadProgress>?`                               | Optional. Receives [upload progress](applications.md#upload-result-and-progress). |
| `cancellationToken` | `CancellationToken`                                        | Optional. Cancels the call.                                                       |

**Returns:** an [`ApplicationData`](applications.md#upload-result-and-progress) for the edited version.

The SDK reads the application's current details and files, applies your changes, uploads only files that are new or changed, and submits the result. To clear the conflicting processes, set `ConflictingProcesses` to an empty list.

```csharp
var edit = await client.EditCustomApplicationAsync(new ApplicationEditMetadata
{
    ProductId = productId,
    Description = "{new-description}",
    ConflictingProcesses = new List<string>()
});

if (edit.IsFailure)
{
    Console.WriteLine($"Edit failed: {edit.Error.Code} {edit.Error.Message}");
    return;
}

Console.WriteLine($"Edited version {edit.Value.UpdateId}");
```

**See also:** [Set-PmpcCustomApplication](../powershell/set-pmpccustomapplication.md), [Create custom edit draft](../rest-api/applications.md#create-custom-edit-draft), and [Complete custom application edit](../rest-api/applications.md#complete-custom-application-edit).

### DeleteApplicationAsync

Deletes one of your custom applications.

```csharp
Task<Result> DeleteApplicationAsync(
    Guid productId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                                 |
| ------------------- | ------------------- | ------------------------------------------- |
| `productId`         | `Guid`              | Required. The custom application to delete. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.                 |

**Returns:** a `Result` that indicates success or failure.

Deleting an application frees a slot against your custom application limit. You can delete only your own custom applications; public catalog applications can't be deleted. The delete is rejected while the application's latest version is in a state that isn't safe to remove, for example while it's still being processed. Deleting can't be undone.

```csharp
var delete = await client.DeleteApplicationAsync(productId);
if (delete.IsFailure)
{
    Console.WriteLine($"Delete failed: {delete.Error.Code} {delete.Error.Message}");
    return;
}

Console.WriteLine("Application deleted.");
```

**See also:** [Remove-PmpcCustomApplication](../powershell/remove-pmpccustomapplication.md) and [Delete an application](../rest-api/applications.md#delete-an-application).

### DeleteCustomApplicationAsync

Deletes one of your custom applications through the custom applications operation.

```csharp
Task<Result> DeleteCustomApplicationAsync(
    Guid productId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                                 |
| ------------------- | ------------------- | ------------------------------------------- |
| `productId`         | `Guid`              | Required. The custom application to delete. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.                 |

**Returns:** a `Result` that indicates success or failure.

This method behaves the same as [`DeleteApplicationAsync`](custom-applications.md#deleteapplicationasync): it frees a slot, it can't delete public catalog applications, and it's rejected while the latest version isn't safe to remove.

```csharp
var delete = await client.DeleteCustomApplicationAsync(productId);
if (delete.IsFailure)
{
    Console.WriteLine($"Delete failed: {delete.Error.Code} {delete.Error.Message}");
    return;
}
```

**See also:** [Remove-PmpcCustomApplication](../powershell/remove-pmpccustomapplication.md) and [Delete a custom application](../rest-api/applications.md#delete-a-custom-application).

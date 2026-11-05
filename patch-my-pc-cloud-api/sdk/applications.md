---
description: >-
  SDK methods for searching applications, reading their details and files, and
  creating, updating, and editing applications.
noIndex: true
noRobotsIndex: true
---

# Applications

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

These methods search for applications, read their details, and create new applications or new versions. Applications come from two catalogs:

* **Your custom applications**—applications you package and upload yourself.
* **The Patch My PC public catalog**—applications Patch My PC packages and maintains.

The methods on this page that don't name a catalog work against your custom applications and keep the behavior the Patch My PC Cloud Customer API has always had. For methods that target your custom applications explicitly, see [Custom applications](custom-applications.md).

All of these methods need an authenticated session. For details, see [SDK authentication methods](authentication.md). Search and read methods need the `appcatbroker:apps:read` scope, and create, update, and edit methods need `appcatbroker:apps:write`.

## Models

The application types live in two namespaces: request models such as `ApplicationMetadata` are in `pmpc.appcatbroker.sdk.Models`, and response types such as `ProductDto` and the `OSType` enumeration are in `pmpc.appcatbroker.client`. The enumerations `RequirementArchitecture` and `InstallationBehavior` are nested in `pmpc.common.Enums`, so add `using static pmpc.common.Enums;` to use them unqualified.

### Search filter

`ProductFilterRequest` describes a search. Every property is optional.

| Property                                   | Type                         | Default         | Description                                                                                                                                          |
| ------------------------------------------ | ---------------------------- | --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `DisplayNameSearchString`                  | `string?`                    | `null`          | Text to match against the application display name.                                                                                                  |
| `VendorIds`                                | `Guid[]?`                    | `null`          | Only return applications from these vendors.                                                                                                         |
| `Languages`                                | `string[]?`                  | `null`          | Only return applications in these languages, for example `en-US`.                                                                                    |
| `Architectures`                            | `RequirementArchitecture[]?` | `null`          | Only return applications for these architectures.                                                                                                    |
| `OsType`                                   | `OSType?`                    | `null`          | The operating system to search. `null` searches Windows applications. macOS applications require the macOS applications entitlement on your account. |
| `FeedTypes`                                | array                        | `null`          | The catalogs to search. The catalog-specific search methods set this for you.                                                                        |
| `ConnectionId`                             | `Guid?`                      | `null`          | The connection to scope a public catalog search to.                                                                                                  |
| `LastModifiedFromUtc`, `LastModifiedToUtc` | `DateTime?`                  | `null`          | Only return applications modified in this range.                                                                                                     |
| `LastUpdatedFromUtc`, `LastUpdatedToUtc`   | `DateTime?`                  | `null`          | Only return applications whose latest version was published in this range.                                                                           |
| `Skip`                                     | `int`                        | `0`             | The number of results to skip, for paging.                                                                                                           |
| `Limit`                                    | `int`                        | `50`            | The maximum number of results to return.                                                                                                             |
| `SortField`                                | `string`                     | `"DisplayName"` | The property to sort by.                                                                                                                             |
| `Ascending`                                | `bool`                       | `true`          | Sort in ascending order.                                                                                                                             |
| `IncludeIconData`                          | `bool`                       | `false`         | Include base64 icon data in each result. This makes responses considerably larger, so leave it off unless you need the icons.                        |

### Search results

`ProductFilterResponse` contains one page of results.

| Property              | Type                              | Description                                                                                       |
| --------------------- | --------------------------------- | ------------------------------------------------------------------------------------------------- |
| `TotalAmount`         | `long`                            | The total number of matching applications across all pages.                                       |
| `TotalVariantsAmount` | `long`                            | The total number of matching application variants, for example language or architecture variants. |
| `Products`            | collection of `ProductSummaryDto` | The applications on this page.                                                                    |

Each `ProductSummaryDto` has these key properties.

| Property                                   | Type                   | Description                                                                                                        |
| ------------------------------------------ | ---------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `ProductId`                                | `Guid`                 | The application ID. `Id` carries the same value; prefer `ProductId`.                                               |
| `UpdateId`                                 | `Guid`                 | The ID of the application's latest version. You need it to publish a new version.                                  |
| `Type`                                     | `string`               | The application type: `pmpc` (Patch My PC catalog), `custom` (your custom applications), or `winget` (Winget).     |
| `DisplayName`                              | `string`               | The display name.                                                                                                  |
| `Description`, `VendorName`, `Language`    | `string?`              | Descriptive details.                                                                                               |
| `Version`                                  | `string?`              | The latest version.                                                                                                |
| `State`                                    | enum                   | The state of the latest version, for example `SuccessfullyCompleted`.                                              |
| `LastUpdated`                              | `DateTimeOffset`       | When the application was last updated.                                                                             |
| `IconURL`, `IconBase64`, `IconContentType` | `string?`              | The icon. `IconBase64` is only set when you request icon data.                                                     |
| `Actions`                                  | collection of `string` | The operations currently available on the application: `deploy`, `update`, `edit`, `delete`, and `download-files`. |

### Application details

`ProductDto` describes one of your applications in detail.

| Property                                               | Type                      | Description                                                  |
| ------------------------------------------------------ | ------------------------- | ------------------------------------------------------------ |
| `ProductId`                                            | `Guid`                    | The application ID.                                          |
| `Type`                                                 | `string`                  | The application type.                                        |
| `DisplayName`, `Description`, `VendorName`, `Language` | `string?`                 | Descriptive details.                                         |
| `UpdateVersion`                                        | `string?`                 | The current version.                                         |
| `MainFile`                                             | `string?`                 | The primary installer file.                                  |
| `Architecture`                                         | `RequirementArchitecture` | The architecture the application targets.                    |
| `InstallerType`                                        | enum                      | The installer type, for example MSI or EXE.                  |
| `InstallContext`                                       | `InstallationBehavior?`   | Whether the application installs for the system or the user. |
| `SilentInstallArguments`, `SilentUninstallArguments`   | `string?`                 | The silent install and uninstall arguments.                  |
| `ConflictingProcessList`                               | collection of `string`    | Processes that block installation while running.             |
| `DetectionRules`                                       | object                    | How Intune detects that the application is installed.        |
| `CustomRequirements`                                   | object                    | The installation requirements.                               |
| `ArpDisplayNameMatch`                                  | `string?`                 | The Add or Remove Programs display name to match.            |
| `MsiProductCode`                                       | `Guid?`                   | The MSI product code, for MSI installers.                    |
| `Notes`, `IntuneNotes`, `Owner`, `Developer`           | `string?`                 | Additional information shown in Intune.                      |
| `PrivacyUrl`, `InformationUrl`                         | `string?`                 | Links shown in Intune.                                       |
| `IconURL`, `IconBase64`, `IconContentType`             | `string?`                 | The icon.                                                    |
| `Actions`                                              | collection of `string`    | The operations currently available on the application.       |

`PublicApplicationDto` describes a public catalog application. It has the descriptive properties of `ProductDto`—`ProductId`, `Type`, `DisplayName`, `Description`, `Language`, `VendorName`, `UpdateVersion`, the icon properties, `PrivacyUrl`, `InformationUrl`, `Developer`, `IntuneNotes`, `InstallerType`, `Architecture`, `InstallContext`, and `Actions`—but not the packaging details, which Patch My PC maintains for you.

### Application metadata

`ApplicationMetadata` describes a new application.

| Property                                             | Type                      | Default   | Description                                                                                                  |
| ---------------------------------------------------- | ------------------------- | --------- | ------------------------------------------------------------------------------------------------------------ |
| `FolderPath`                                         | `string`                  | none      | Required. The folder that contains the application's files. Every file in the folder is uploaded.            |
| `PrimaryInstallerFile`                               | `string`                  | none      | Required. The main installer file, relative to `FolderPath` or as an absolute path.                          |
| `DisplayName`                                        | `string`                  | none      | Required. The display name.                                                                                  |
| `Description`                                        | `string`                  | none      | Required. The description.                                                                                   |
| `Publisher`                                          | `string`                  | none      | Required. The publisher or vendor name.                                                                      |
| `Architecture`                                       | `RequirementArchitecture` | `X64`     | The architecture the application targets.                                                                    |
| `Language`                                           | `string`                  | `"en-US"` | The language code.                                                                                           |
| `InstallContext`                                     | `InstallationBehavior`    | `System`  | Whether the application installs for the system or the user.                                                 |
| `CmdArguments`                                       | `string?`                 | `null`    | The silent install arguments.                                                                                |
| `SilentUninstallArg`                                 | `string?`                 | `null`    | The silent uninstall arguments.                                                                              |
| `MsiProductCode`                                     | `Guid?`                   | `null`    | The MSI product code, for MSI installers.                                                                    |
| `ArpDisplayNameMatch`, `ArpVersionMatch`             | `string?`                 | `null`    | The Add or Remove Programs display name and version to match for detection.                                  |
| `DetectionRules`                                     | object                    | `null`    | Custom detection rules. When omitted, detection uses `MsiProductCode` or the Add or Remove Programs matches. |
| `CustomRequirements`                                 | object                    | `null`    | Custom installation requirements. When omitted, the requirement is derived from `Architecture`.              |
| `ConflictingProcesses`                               | `List<string>`            | empty     | Processes that block installation while running.                                                             |
| `IconPath`                                           | `string?`                 | `null`    | The path to an icon file. The SDK uploads it for you.                                                        |
| `DocumentationUrl`, `PrivacyUrl`, `InformationalUrl` | `string?`                 | `null`    | Links shown in Intune.                                                                                       |
| `Notes`, `IntuneNotes`, `Owner`, `Developer`         | `string?`                 | `null`    | Additional information shown in Intune.                                                                      |

`ApplicationUpdateMetadata` describes a new version of an existing application. It has `ProductId` and `UpdateId`—the application and the version the new one follows—plus the packaging properties from the table above: `FolderPath`, `PrimaryInstallerFile`, `CmdArguments`, `SilentUninstallArg`, `MsiProductCode`, `ArpDisplayNameMatch`, `ArpVersionMatch`, `DetectionRules`, `CustomRequirements`, and `ConflictingProcesses`. Get both IDs from a search result.

### Edit metadata

`ApplicationEditMetadata` describes changes to an application's current version. Apart from `ProductId`, every property is optional, and `null` keeps the current value.

| Property                                                                       | Type            | Description                                                                                                                                  |
| ------------------------------------------------------------------------------ | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `ProductId`                                                                    | `Guid`          | Required. The application to edit.                                                                                                           |
| `UpdateId`                                                                     | `Guid?`         | The version to edit. When omitted, the SDK finds the current version for you.                                                                |
| `DisplayName`, `Description`, `Publisher`, `Owner`, `Developer`, `IntuneNotes` | `string?`       | New descriptive details.                                                                                                                     |
| `PrivacyUrl`, `InformationalUrl`                                               | `string?`       | New links.                                                                                                                                   |
| `IconPath`                                                                     | `string?`       | The path to a replacement icon.                                                                                                              |
| `CmdArguments`, `SilentUninstallArg`                                           | `string?`       | New silent install and uninstall arguments.                                                                                                  |
| `ArpDisplayNameMatch`                                                          | `string?`       | A new Add or Remove Programs display name match.                                                                                             |
| `MsiProductCode`                                                               | `Guid?`         | A new MSI product code. You can't use this to clear the product code, because the installer type can't change during an edit.                |
| `ConflictingProcesses`                                                         | `List<string>?` | A replacement list. An empty list clears it.                                                                                                 |
| `DetectionRules`, `CustomRequirements`                                         | object          | Replacement detection rules or requirements.                                                                                                 |
| `FolderPath`                                                                   | `string?`       | A folder whose contents replace the application's files. The SDK uploads only files that are new or changed. `null` keeps the current files. |
| `PrimaryInstallerFile`                                                         | `string?`       | A new primary installer file, relative to `FolderPath`.                                                                                      |

### Upload result and progress

Create, update, and edit methods return `ApplicationData`.

| Property             | Type       | Description                                       |
| -------------------- | ---------- | ------------------------------------------------- |
| `ProductId`          | `Guid`     | The application ID.                               |
| `UpdateId`           | `Guid`     | The ID of the version that was created or edited. |
| `FilesUploaded`      | `int`      | The number of files uploaded.                     |
| `TotalBytesUploaded` | `long`     | The number of bytes uploaded.                     |
| `Duration`           | `TimeSpan` | How long the operation took.                      |

If you pass an `IProgress<UploadProgress>`, the SDK reports progress as it works.

| Property                                    | Type      | Description                                                                      |
| ------------------------------------------- | --------- | -------------------------------------------------------------------------------- |
| `Stage`                                     | enum      | The current stage: `ComputingHashes`, `Uploading`, `Finalizing`, or `Completed`. |
| `FileName`                                  | `string`  | The file being uploaded.                                                         |
| `BytesUploaded`, `TotalBytes`               | `long`    | Progress for the current file.                                                   |
| `BytesUploadedOverall`, `TotalBytesOverall` | `long`    | Progress across all files.                                                       |
| `FilesProcessed`, `TotalFiles`              | `int`     | Files completed and the total number of files.                                   |
| `ChunksUploaded`, `TotalChunks`             | `int`     | Chunks completed and the total number of chunks.                                 |
| `Message`                                   | `string?` | A status message, if any.                                                        |

To tune the upload, pass `ChunkUploadOptions`. For details, see [Install and configure the SDK](install-and-configure.md).

## Methods

### SearchApplicationsAsync

Searches your custom applications.

```csharp
Task<Result<ProductFilterResponse>> SearchApplicationsAsync(
    ProductFilterRequest filterRequest,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                                                    | Description                    |
| ------------------- | ------------------------------------------------------- | ------------------------------ |
| `filterRequest`     | [`ProductFilterRequest`](applications.md#search-filter) | Required. The search criteria. |
| `cancellationToken` | `CancellationToken`                                     | Optional. Cancels the call.    |

**Returns:** a [`ProductFilterResponse`](applications.md#search-results) with one page of results.

```csharp
var search = await broker.SearchApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "{search-text}",
    Limit = 25
});

if (search.IsFailure)
{
    Console.WriteLine($"Search failed: {search.Error.Code} {search.Error.Message}");
    return;
}

Console.WriteLine($"{search.Value.TotalAmount} matching applications");
foreach (var product in search.Value.Products)
{
    Console.WriteLine($"{product.DisplayName} {product.Version} ({product.ProductId})");
}
```

**See also:** [Find-PmpcCustomApplication](../powershell/find-pmpccustomapplication.md) and [Search applications](../rest-api/applications.md#search-applications).

### GetApplicationDetailsAsync

Gets the details of one of your custom applications.

```csharp
Task<Result<ProductDto>> GetApplicationDetailsAsync(
    Guid productId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                   |
| ------------------- | ------------------- | ----------------------------- |
| `productId`         | `Guid`              | Required. The application ID. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.   |

**Returns:** a [`ProductDto`](applications.md#application-details). If the application doesn't exist, the error code is `NOT_FOUND`. The details don't include the file list; use [`GetApplicationFilesAsync`](applications.md#getapplicationfilesasync) for that.

```csharp
var details = await broker.GetApplicationDetailsAsync(productId);
if (details.IsFailure)
{
    Console.WriteLine($"Couldn't read the application: {details.Error.Message}");
    return;
}

Console.WriteLine($"{details.Value.DisplayName} {details.Value.UpdateVersion}");
Console.WriteLine($"Installer: {details.Value.MainFile} {details.Value.SilentInstallArguments}");
```

**See also:** [Get-PmpcCustomApplication](../powershell/get-pmpccustomapplication.md) and [Get application details](../rest-api/applications.md#get-application-details).

### CreateApplicationAsync

Creates a custom application and uploads its files in one call.

```csharp
Task<Result<ApplicationData>> CreateApplicationAsync(
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

The SDK creates a draft, uploads the files in chunks, and completes the application. Each new application counts against your custom application limit; check `GetCustomerInfoAsync` to see your usage. If you've reached the limit, the method fails with `VALIDATION_ERROR` and a message that says you have reached the maximum number of custom applications.

```csharp
using pmpc.appcatbroker.sdk.Models;
using static pmpc.common.Enums;

var metadata = new ApplicationMetadata
{
    FolderPath = @"{path-to-folder}",
    PrimaryInstallerFile = "{installer-file-name}.msi",
    DisplayName = "{display-name}",
    Description = "{description}",
    Publisher = "{publisher}",
    Architecture = RequirementArchitecture.X64,
    InstallContext = InstallationBehavior.System,
    CmdArguments = "/qn",
    MsiProductCode = Guid.Parse("{msi-product-code}")
};

var progress = new Progress<UploadProgress>(p =>
    Console.WriteLine($"{p.Stage}: {p.BytesUploadedOverall}/{p.TotalBytesOverall} bytes"));

var created = await broker.CreateApplicationAsync(metadata, progress: progress);
if (created.IsFailure)
{
    Console.WriteLine($"Create failed: {created.Error.Code} {created.Error.Message}");
    return;
}

Console.WriteLine($"Created {created.Value.ProductId} in {created.Value.Duration}");
```

**See also:** [New-PmpcCustomApplication](../powershell/new-pmpccustomapplication.md), [Create application draft](../rest-api/applications.md#create-application-draft), and [Complete application creation](../rest-api/applications.md#complete-application-creation).

### UpdateApplicationAsync

Publishes a new version of one of your custom applications and uploads its files.

```csharp
Task<Result<ApplicationData>> UpdateApplicationAsync(
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

To correct the current version without publishing a new one, use [`EditApplicationAsync`](applications.md#editapplicationasync) instead.

```csharp
var update = await broker.UpdateApplicationAsync(new ApplicationUpdateMetadata
{
    ProductId = product.ProductId,
    UpdateId = product.UpdateId,
    FolderPath = @"{path-to-new-version}",
    PrimaryInstallerFile = "{installer-file-name}.msi",
    CmdArguments = "/qn"
});

if (update.IsFailure)
{
    Console.WriteLine($"Update failed: {update.Error.Code} {update.Error.Message}");
    return;
}

Console.WriteLine($"Published version {update.Value.UpdateId}");
```

**See also:** [Update-PmpcCustomApplication](../powershell/update-pmpccustomapplication.md), [Create update draft](../rest-api/applications.md#create-update-draft), and [Complete application update](../rest-api/applications.md#complete-application-update).

### EditApplicationAsync

Corrects an application's current version in place, without publishing a new version.

```csharp
Task<Result<ApplicationData>> EditApplicationAsync(
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

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

Use this method to fix a display name, change an owner, replace an icon, or amend detection rules. The SDK reads the application's current details and files, applies your changes, uploads only files that are new or changed, and submits the result, so you only set the properties you want to change.

```csharp
var edit = await broker.EditApplicationAsync(new ApplicationEditMetadata
{
    ProductId = productId,
    DisplayName = "{new-display-name}",
    Owner = "{new-owner}"
});

if (edit.IsFailure)
{
    Console.WriteLine($"Edit failed: {edit.Error.Code} {edit.Error.Message}");
    return;
}

Console.WriteLine($"Edited version {edit.Value.UpdateId}");
```

**See also:** [Set-PmpcCustomApplication](../powershell/set-pmpccustomapplication.md), [Create edit draft](../rest-api/applications.md#create-edit-draft), and [Complete application edit](../rest-api/applications.md#complete-application-edit).

### GetApplicationFilesAsync

Lists the files in an application's current version.

```csharp
Task<Result<IReadOnlyList<ApplicationFileDto>>> GetApplicationFilesAsync(
    Guid productId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                   |
| ------------------- | ------------------- | ----------------------------- |
| `productId`         | `Guid`              | Required. The application ID. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.   |

**Returns:** a list of `ApplicationFileDto` objects.

| Property                 | Type     | Description                                             |
| ------------------------ | -------- | ------------------------------------------------------- |
| `ProductId`              | `Guid`   | The application ID.                                     |
| `FileName`               | `string` | The file name.                                          |
| `FileSize`               | `long`   | The file size in bytes.                                 |
| `FileType`               | enum     | The file's role, for example `Installation` or `Extra`. |
| `Sha1Hash`, `Sha256Hash` | `string` | The file hashes. `Sha256Hash` can be `null`.            |

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

`EditApplicationAsync` reads the file list for you, so you don't need this method to edit an application.

```csharp
var files = await broker.GetApplicationFilesAsync(productId);
if (files.IsFailure)
{
    Console.WriteLine($"Couldn't list files: {files.Error.Code} {files.Error.Message}");
    return;
}

foreach (var file in files.Value)
{
    Console.WriteLine($"{file.FileName} ({file.FileSize:N0} bytes, {file.FileType})");
}
```

**See also:** [Get-PmpcApplicationFile](../powershell/get-pmpcapplicationfile.md) and [Get application files](../rest-api/applications.md#get-application-files).

### SearchPublicApplicationsAsync

Searches the Patch My PC public catalog.

```csharp
Task<Result<ProductFilterResponse>> SearchPublicApplicationsAsync(
    ProductFilterRequest filterRequest,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                                                    | Description                                                                                                          |
| ------------------- | ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `filterRequest`     | [`ProductFilterRequest`](applications.md#search-filter) | Required. The search criteria. `FeedTypes` is ignored. If `ConnectionId` isn't set, the selected connection is used. |
| `cancellationToken` | `CancellationToken`                                     | Optional. Cancels the call.                                                                                          |

**Returns:** a [`ProductFilterResponse`](applications.md#search-results) with one page of public catalog results.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

A public catalog search needs an Intune connection. Set `ConnectionId` or select a connection first; otherwise the method fails with the message "Either supply a connectionId or call SetSelectedConnectionAsync first." For details, see [Customer information and connections](customer-and-connections.md).

```csharp
var search = await broker.SearchPublicApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "{search-text}",
    OsType = OSType.Windows
});

if (search.IsFailure)
{
    Console.WriteLine($"Search failed: {search.Error.Code} {search.Error.Message}");
    return;
}

foreach (var product in search.Value.Products)
{
    Console.WriteLine($"{product.DisplayName} {product.Version} ({product.ProductId})");
}
```

**See also:** [Find-PmpcApplication](../powershell/find-pmpcapplication.md) and [Search public applications](../rest-api/applications.md#search-public-applications).

### GetPublicApplicationDetailsAsync

Gets the details of one public catalog application.

```csharp
Task<Result<PublicApplicationDto>> GetPublicApplicationDetailsAsync(
    Guid productId,
    Guid? connectionId = null,
    CancellationToken cancellationToken = default);

Task<Result<PublicApplicationDto>> GetPublicApplicationDetailsAsync(
    Guid productId,
    Guid? connectionId,
    OSType? osType,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                                                                            |
| ------------------- | ------------------- | -------------------------------------------------------------------------------------- |
| `productId`         | `Guid`              | Required. The application ID.                                                          |
| `connectionId`      | `Guid?`             | Optional. The connection to scope the lookup to. `null` uses the selected connection.  |
| `osType`            | `OSType?`           | Optional, second overload only. The operating system to look up. `null` means Windows. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.                                                            |

**Returns:** a [`PublicApplicationDto`](applications.md#application-details). If you look up a macOS application and your account isn't entitled to macOS applications, the error code is `NOT_FOUND`.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

```csharp
var details = await broker.GetPublicApplicationDetailsAsync(productId, connectionId: null, osType: OSType.Windows);
if (details.IsFailure)
{
    Console.WriteLine($"Couldn't read the application: {details.Error.Code} {details.Error.Message}");
    return;
}

Console.WriteLine($"{details.Value.DisplayName} {details.Value.UpdateVersion} by {details.Value.VendorName}");
```

**See also:** [Get-PmpcApplication](../powershell/get-pmpcapplication.md) and [Get public application details](../rest-api/applications.md#get-public-application-details).

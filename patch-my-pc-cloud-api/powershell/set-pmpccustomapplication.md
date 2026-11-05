---
description: Edits an application's current version in place.
noIndex: true
noRobotsIndex: true
---

# Set-PmpcCustomApplication

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Edits an application's current version in place.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

### Properties (Default)

```powershell
Set-PmpcCustomApplication [-ProductId] <Guid> [-UpdateId <Guid>] [-DisplayName <String>]
  [-Description <String>] [-Publisher <String>] [-Owner <String>] [-Developer <String>]
  [-IntuneNotes <String>] [-PrivacyUrl <String>] [-InformationalUrl <String>]
  [-IconPath <String>] [-FolderPath <String>] [-PrimaryInstallerFile <String>]
  [-UploadOption <ChunkUploadOptions>] [-ChunkSize <Int32>] [-MaxChunkConcurrency <Int32>]
  [-MaxFileConcurrency <Int32>] [-MaxHashingConcurrency <Int32>]
  [-UploadTimeout <TimeSpan>] [-RetryAttempt <Int32>] [-ArpDisplayNameMatch <String>]
  [-CmdArguments <String>] [-SilentUninstallArg <String>] [-MsiProductCode <Guid>]
  [-ConflictingProcess <String[]>] [-DetectionRules <DetectionRulesDto>]
  [-CustomRequirements <CustomRequirementsDto>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### Metadata

```powershell
Set-PmpcCustomApplication [-Metadata] <ApplicationEditMetadata>
  [-UploadOption <ChunkUploadOptions>] [-ChunkSize <Int32>] [-MaxChunkConcurrency <Int32>]
  [-MaxFileConcurrency <Int32>] [-MaxHashingConcurrency <Int32>]
  [-UploadTimeout <TimeSpan>] [-RetryAttempt <Int32>] [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Corrects an already-published application without publishing a new version: fixes a display name, changes an owner or developer, replaces an icon, or amends detection rules.

Only what you specify changes. Every unspecified property keeps its current value, and specifying nothing about files uploads nothing at all. To ship new content under a new version number, use Update-PmpcCustomApplication instead; that is the one thing this cannot do.

When -FolderPath is supplied, the folder is hashed and compared against the version's current files, and only files that are new or whose content changed are uploaded.

## Parameters

### -ArpDisplayNameMatch

Pattern matched against the application's Add/Remove Programs display name. Used for detection when no custom detection rules are supplied.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -ChunkSize

Size of each upload chunk, in bytes. Defaults to 8 MB. Only applies to files large enough to be chunked.

| Attribute      | Value          |
| -------------- | -------------- |
| Type           | `System.Int32` |
| Required       | False          |
| Position       | Named          |
| Pipeline input | False          |
| Aliases        | None           |
| Parameter sets | All            |

### -CmdArguments

Arguments passed to the installer for a silent install.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -Confirm

Prompts you for confirmation before running the cmdlet.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | cf                                             |

### -ConflictingProcess

Processes that must not be running when the application installs.

| Attribute      | Value                |
| -------------- | -------------------- |
| Type           | `System.String[]`    |
| Required       | False                |
| Position       | Named                |
| Pipeline input | False                |
| Aliases        | ConflictingProcesses |
| Parameter sets | Properties           |

### -CustomRequirements

Custom system requirements. Supplying them replaces the default single-architecture requirement.

| Attribute      | Value                   |
| -------------- | ----------------------- |
| Type           | `CustomRequirementsDto` |
| Required       | False                   |
| Position       | Named                   |
| Pipeline input | False                   |
| Aliases        | None                    |
| Parameter sets | Properties              |

### -Description

Description shown to end users.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -DetectionRules

Custom detection rules. Supplying them replaces the default detection derived from -MsiProductCode or the ARP match patterns.

| Attribute      | Value               |
| -------------- | ------------------- |
| Type           | `DetectionRulesDto` |
| Required       | False               |
| Position       | Named               |
| Pipeline input | False               |
| Aliases        | None                |
| Parameter sets | Properties          |

### -Developer

Developer recorded against the application.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -DisplayName

Name shown to end users.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -FolderPath

Folder whose contents replace the application's files. Omitting it keeps the current file list exactly as it is and uploads nothing.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -IconPath

Replacement icon file to upload. Omitting it keeps the current icon.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -InformationalUrl

Information URL shown to end users.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -IntuneNotes

Notes surfaced on the application in Intune.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -MaxChunkConcurrency

Number of chunks uploaded in parallel for a single file. Defaults to 4.

| Attribute      | Value          |
| -------------- | -------------- |
| Type           | `System.Int32` |
| Required       | False          |
| Position       | Named          |
| Pipeline input | False          |
| Aliases        | None           |
| Parameter sets | All            |

### -MaxFileConcurrency

Number of files uploaded in parallel. Total in-flight requests is roughly this multiplied by -MaxChunkConcurrency.

| Attribute      | Value          |
| -------------- | -------------- |
| Type           | `System.Int32` |
| Required       | False          |
| Position       | Named          |
| Pipeline input | False          |
| Aliases        | None           |
| Parameter sets | All            |

### -MaxHashingConcurrency

Number of files hashed in parallel before upload. Defaults to the processor count.

| Attribute      | Value          |
| -------------- | -------------- |
| Type           | `System.Int32` |
| Required       | False          |
| Position       | Named          |
| Pipeline input | False          |
| Aliases        | None           |
| Parameter sets | All            |

### -Metadata

A fully-built SDK metadata object, for callers that already construct one (for example when driving the module from existing SDK code). Mutually exclusive with the individual property parameters.

| Attribute      | Value                     |
| -------------- | ------------------------- |
| Type           | `ApplicationEditMetadata` |
| Required       | True                      |
| Position       | 0                         |
| Pipeline input | True (ByValue)            |
| Aliases        | None                      |
| Parameter sets | Metadata                  |

### -MsiProductCode

MSI product code. Its presence is what marks the application as an MSI rather than an EXE, so it cannot be used to clear the value on an existing MSI application.

| Attribute      | Value         |
| -------------- | ------------- |
| Type           | `System.Guid` |
| Required       | False         |
| Position       | Named         |
| Pipeline input | False         |
| Aliases        | None          |
| Parameter sets | Properties    |

### -Owner

Owner recorded against the application.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -PrimaryInstallerFile

The installer to run, relative to -FolderPath. Omitting it keeps the current primary installer.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -PrivacyUrl

Privacy policy URL.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -ProductId

ID of the application. Accepted from the pipeline by property name, so results from Find-PmpcCustomApplication and Get-PmpcCustomApplication can be piped straight in.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Guid`         |
| Required       | True                  |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | Id                    |
| Parameter sets | Properties            |

### -Publisher

Publisher or vendor name.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -RetryAttempt

Number of times a failed chunk is retried before the upload fails. Defaults to 3.

| Attribute      | Value          |
| -------------- | -------------- |
| Type           | `System.Int32` |
| Required       | False          |
| Position       | Named          |
| Pipeline input | False          |
| Aliases        | None           |
| Parameter sets | All            |

### -SilentUninstallArg

Arguments passed to the uninstaller for a silent uninstall.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -UpdateId

The version to edit. Resolved automatically when omitted, because the application lookup does not return an update ID.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Guid`         |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |
| Parameter sets | Properties            |

### -UploadOption

A pre-built ChunkUploadOptions object. The individual upload parameters are applied over it, so both can be combined.

| Attribute      | Value                |
| -------------- | -------------------- |
| Type           | `ChunkUploadOptions` |
| Required       | False                |
| Position       | Named                |
| Pipeline input | False                |
| Aliases        | None                 |
| Parameter sets | All                  |

### -UploadTimeout

Timeout for each individual HTTP request, not for the upload as a whole. Defaults to 30 minutes.

| Attribute      | Value             |
| -------------- | ----------------- |
| Type           | `System.TimeSpan` |
| Required       | False             |
| Position       | Named             |
| Pipeline input | False             |
| Aliases        | None              |
| Parameter sets | All               |

### -WhatIf

Shows what would happen if the cmdlet runs. The cmdlet is not run.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | wi                                             |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### ApplicationEditMetadata

A pre-built metadata object, bound to -Metadata.

## Outputs

### ApplicationData

The edited application's IDs and upload statistics.

## Examples

### Example 1: Correct a display name

```powershell
Set-PmpcCustomApplication -ProductId $productId -DisplayName '7-Zip (x64)'
```

Changes only the display name; every other property, and the whole file list, is left untouched.

### Example 2: Replace the icon

```powershell
Set-PmpcCustomApplication -ProductId $productId -IconPath .\icons\7zip.png
```

Uploads the new icon and leaves the application's files alone.

### Example 3: Replace the application's files

```powershell
Set-PmpcCustomApplication -ProductId $productId -FolderPath .\7zip-fixed -PrimaryInstallerFile '7z2408-x64.msi'
```

Hashes the folder and uploads only the files whose content actually changed.

### Example 4: Clear the conflicting-process list

```powershell
Set-PmpcCustomApplication -ProductId $productId -ConflictingProcess @()
```

An explicitly empty array clears the list; omitting the parameter would keep it.

## Notes

The service replaces the whole application, but this cmdlet does not. The SDK reads the application's current metadata and file list, lays your changes over the top, and submits the complete payload, so changing one field means supplying one parameter.

-MsiProductCode cannot be used to clear a product code. Its presence is what tells the service the installer is an MSI, so dropping it reads as a switch to EXE and the edit is rejected.

-ConflictingProcess is the one parameter where an explicitly empty array is meaningful: it clears the list, whereas omitting the parameter keeps it.

## Related links

* [Update-PmpcCustomApplication](update-pmpccustomapplication.md)
* [Get-PmpcCustomApplication](get-pmpccustomapplication.md)
* [Get-PmpcApplicationFile](get-pmpcapplicationfile.md)
* PowerShell module

## See also

* SDK method: [EditCustomApplicationAsync](../sdk/custom-applications.md#editcustomapplicationasync)
* REST operation: [`POST /v1/api/apps/custom/edit-draft`](../rest-api/applications.md#create-custom-edit-draft)
* REST operation: [`PUT /v1/api/apps/custom/edit-complete`](../rest-api/applications.md#complete-custom-application-edit)
* REST operation: [`GET /v1/api/apps/{productId}`](../rest-api/applications.md#get-application-details)
* REST operation: [`GET /v1/api/apps/{productId}/files`](../rest-api/applications.md#get-application-files)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

---
description: Publishes a new version of an existing application.
noIndex: true
noRobotsIndex: true
---

# Update-PmpcCustomApplication

## Synopsis

Publishes a new version of an existing application.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

### Properties (Default)

```powershell
Update-PmpcCustomApplication [-ProductId] <Guid> [-UpdateId] <Guid> [-FolderPath] <String>
  [-PrimaryInstallerFile] <String> [-ArpVersionMatch <String>]
  [-UploadOption <ChunkUploadOptions>] [-ChunkSize <Int32>] [-MaxChunkConcurrency <Int32>]
  [-MaxFileConcurrency <Int32>] [-MaxHashingConcurrency <Int32>]
  [-UploadTimeout <TimeSpan>] [-RetryAttempt <Int32>] [-ArpDisplayNameMatch <String>]
  [-CmdArguments <String>] [-SilentUninstallArg <String>] [-MsiProductCode <Guid>]
  [-ConflictingProcess <String[]>] [-DetectionRules <DetectionRulesDto>]
  [-CustomRequirements <CustomRequirementsDto>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### Metadata

```powershell
Update-PmpcCustomApplication [-Metadata] <ApplicationUpdateMetadata>
  [-UploadOption <ChunkUploadOptions>] [-ChunkSize <Int32>] [-MaxChunkConcurrency <Int32>]
  [-MaxFileConcurrency <Int32>] [-MaxHashingConcurrency <Int32>]
  [-UploadTimeout <TimeSpan>] [-RetryAttempt <Int32>] [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Creates a new version of an existing application from the files in -FolderPath and uploads them.

This is the cmdlet for shipping new content. To correct metadata on the version that is already published, without creating a new one, use Set-PmpcCustomApplication instead.

Product-level details such as display name, vendor, and description are not part of the update flow; they belong to the application, not to a version.

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

### -ArpVersionMatch

Pattern matched against the application's Add/Remove Programs version. Used for detection alongside -ArpDisplayNameMatch.

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

### -FolderPath

Folder containing the application's files. Every file beneath it is uploaded. Relative paths are resolved against the current PowerShell location.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | True            |
| Position       | 2               |
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

| Attribute      | Value                       |
| -------------- | --------------------------- |
| Type           | `ApplicationUpdateMetadata` |
| Required       | True                        |
| Position       | 0                           |
| Pipeline input | True (ByValue)              |
| Aliases        | None                        |
| Parameter sets | Metadata                    |

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

### -PrimaryInstallerFile

The installer to run, as a path relative to -FolderPath.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | True            |
| Position       | 3               |
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

ID of the existing version the new one follows.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Guid`         |
| Required       | True                  |
| Position       | 1                     |
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

### ApplicationUpdateMetadata

A pre-built metadata object, bound to -Metadata.

## Outputs

### ApplicationData

The new version's IDs and upload statistics.

## Examples

### Example 1: Publish a new version

```powershell
Update-PmpcCustomApplication -ProductId $productId -UpdateId $updateId -FolderPath .\7zip-2409 -PrimaryInstallerFile '7z2409-x64.msi'
```

Uploads the new version's files and publishes it.

### Example 2: Publish a new version found by search

```powershell
$app = Find-PmpcCustomApplication -DisplayName '7-Zip' | Select-Object -First 1
Update-PmpcCustomApplication -ProductId $app.Id -UpdateId $app.UpdateId -FolderPath .\7zip-2409 -PrimaryInstallerFile '7z2409-x64.msi'
```

Takes both identifiers from a search result rather than hard-coding them.

## Notes

Requires both -ProductId and -UpdateId, identifying the application and the version the new one follows. Get them from Find-PmpcCustomApplication.

Press Ctrl-C to cancel: the upload is canceled rather than left running to completion in the background.

## Related links

* [New-PmpcCustomApplication](new-pmpccustomapplication.md)
* [Set-PmpcCustomApplication](set-pmpccustomapplication.md)
* PowerShell module

## See also

* SDK method: [UpdateCustomApplicationAsync](../sdk/custom-applications.md#updatecustomapplicationasync)
* REST operation: [`POST /v1/api/apps/custom/update-draft`](../rest-api/applications.md#create-custom-update-draft)
* REST operation: [`PUT /v1/api/apps/custom/complete`](../rest-api/applications.md#complete-custom-application-update)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

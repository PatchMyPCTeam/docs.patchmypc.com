---
description: Creates a custom application and uploads its files.
noIndex: true
noRobotsIndex: true
---

# New-PmpcCustomApplication

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Creates a custom application and uploads its files.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

### Properties (Default)

```powershell
New-PmpcCustomApplication [-FolderPath] <String> [-PrimaryInstallerFile] <String>
  [-DisplayName] <String> -Description <String> -Publisher <String>
  [-Architecture <RequirementArchitecture>] [-Language <String>]
  [-InstallContext <InstallationBehavior>] [-ArpVersionMatch <String>]
  [-IconPath <String>] [-DocumentationUrl <String>] [-PrivacyUrl <String>]
  [-InformationalUrl <String>] [-Notes <String>] [-IntuneNotes <String>] [-Owner <String>]
  [-Developer <String>] [-UploadOption <ChunkUploadOptions>] [-ChunkSize <Int32>]
  [-MaxChunkConcurrency <Int32>] [-MaxFileConcurrency <Int32>]
  [-MaxHashingConcurrency <Int32>] [-UploadTimeout <TimeSpan>] [-RetryAttempt <Int32>]
  [-ArpDisplayNameMatch <String>] [-CmdArguments <String>] [-SilentUninstallArg <String>]
  [-MsiProductCode <Guid>] [-ConflictingProcess <String[]>]
  [-DetectionRules <DetectionRulesDto>] [-CustomRequirements <CustomRequirementsDto>]
  [-WhatIf] [-Confirm] [<CommonParameters>]
```

### Metadata

```powershell
New-PmpcCustomApplication [-Metadata] <ApplicationMetadata>
  [-UploadOption <ChunkUploadOptions>] [-ChunkSize <Int32>] [-MaxChunkConcurrency <Int32>]
  [-MaxFileConcurrency <Int32>] [-MaxHashingConcurrency <Int32>]
  [-UploadTimeout <TimeSpan>] [-RetryAttempt <Int32>] [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Creates a new custom application for the selected company and uploads everything in -FolderPath, reporting progress as it goes.

Files are hashed, then uploaded singly or in chunks depending on size, then the application is finalized in one call. Upload concurrency, chunk size, and retries can all be tuned; the defaults are sensible for most folders.

Detection defaults to the MSI product code when -MsiProductCode is given, and otherwise to the Add or Remove Programs (ARP) match patterns. Supply -DetectionRules to replace that entirely.

## Parameters

### -Architecture

Architecture the application targets. Defaults to X64.

| Attribute       | Value                                 |
| --------------- | ------------------------------------- |
| Type            | `RequirementArchitecture`             |
| Required        | False                                 |
| Position        | Named                                 |
| Pipeline input  | False                                 |
| Aliases         | None                                  |
| Accepted values | Unspecified, X64, X86, ARM, Universal |
| Parameter sets  | Properties                            |

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

### -Description

Description shown to end users.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | True            |
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
| Required       | True            |
| Position       | 2               |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -DocumentationUrl

Documentation URL for the application.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -FolderPath

Folder containing the application's files. Every file beneath it is uploaded. Relative paths are resolved against the current PowerShell location.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | True            |
| Position       | 0               |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -IconPath

Icon file to upload for the application. Relative paths are resolved against the current PowerShell location.

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

### -InstallContext

Whether the application installs per-user or per-machine. Defaults to System.

| Attribute       | Value                  |
| --------------- | ---------------------- |
| Type            | `InstallationBehavior` |
| Required        | False                  |
| Position        | Named                  |
| Pipeline input  | False                  |
| Aliases         | None                   |
| Accepted values | User, System, Any      |
| Parameter sets  | Properties             |

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

### -Language

Language code for the application. Defaults to en-US.

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

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `ApplicationMetadata` |
| Required       | True                  |
| Position       | 0                     |
| Pipeline input | True (ByValue)        |
| Aliases        | None                  |
| Parameter sets | Metadata              |

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

### -Notes

Free-form notes recorded against the application.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

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

The installer to run, as a path relative to -FolderPath.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | True            |
| Position       | 1               |
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

### -Publisher

Publisher or vendor name.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | True            |
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

### ApplicationMetadata

A pre-built metadata object, bound to -Metadata.

## Outputs

### ApplicationData

The created application's IDs and upload statistics.

## Examples

### Example 1: Create an application

```powershell
New-PmpcCustomApplication -FolderPath .\7zip -PrimaryInstallerFile '7z2408-x64.msi' -DisplayName '7-Zip' -Description 'File archiver' -Publisher 'Igor Pavlov'
```

Uploads every file in the folder and creates the application.

### Example 2: Create an EXE application with detection and silent arguments

```powershell
New-PmpcCustomApplication -FolderPath .\app -PrimaryInstallerFile 'setup.exe' -DisplayName 'Contoso App' -Description 'Line of business app' -Publisher 'Contoso' -CmdArguments '/S' -SilentUninstallArg '/S /uninstall' -ArpDisplayNameMatch 'Contoso App*' -ArpVersionMatch '1.*'
```

Supplies silent install and uninstall arguments and Add/Remove Programs detection patterns.

### Example 3: Tune the upload for a large folder

```powershell
New-PmpcCustomApplication -FolderPath .\bigapp -PrimaryInstallerFile 'setup.msi' -DisplayName 'Big App' -Description 'Large application' -Publisher 'Contoso' -MaxFileConcurrency 8 -ChunkSize 16MB -RetryAttempt 5
```

Raises file concurrency and chunk size, and allows more retries on a flaky link.

### Example 4: Create from a metadata object

```powershell
$metadata = [pmpc.appcatbroker.sdk.Models.ApplicationMetadata]::new()
$metadata.FolderPath = 'C:\apps\7zip'
$metadata.PrimaryInstallerFile = '7z2408-x64.msi'
$metadata.DisplayName = '7-Zip'
$metadata.Description = 'File archiver'
$metadata.Publisher = 'Igor Pavlov'
New-PmpcCustomApplication -Metadata $metadata
```

Uses the SDK metadata type directly, which is useful when the values come from a configuration file.

## Notes

Counts against the customer's custom-application limit. Use Remove-PmpcCustomApplication to free a slot.

Press Ctrl-C to cancel: the upload is canceled rather than left running to completion in the background.

## Related links

* [Update-PmpcCustomApplication](update-pmpccustomapplication.md)
* [Set-PmpcCustomApplication](set-pmpccustomapplication.md)
* [Remove-PmpcCustomApplication](remove-pmpccustomapplication.md)
* PowerShell module

## See also

* SDK method: [CreateCustomApplicationAsync](../sdk/custom-applications.md#createcustomapplicationasync)
* REST operation: [`POST /v1/api/apps/custom/draft`](../rest-api/applications.md#create-custom-application-draft)
* REST operation: [`POST /v1/api/apps/custom/complete`](../rest-api/applications.md#complete-custom-application-creation)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

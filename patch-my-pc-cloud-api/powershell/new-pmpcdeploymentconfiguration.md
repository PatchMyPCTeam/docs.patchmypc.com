---
description: Builds a deployment's optional configuration block.
noIndex: true
noRobotsIndex: true
---

# New-PmpcDeploymentConfiguration

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Builds a deployment's optional configuration block.

## Syntax

```powershell
New-PmpcDeploymentConfiguration [[-AdditionalArgument] <String>]
  [-InstallLoggingPath <String>]
  [-CustomRequirements <EditDeploymentCustomRequirementsRequest>]
  [-AppInfo <DeploymentAppInfoDto>]
  [-ConflictingProcess <DeploymentConflictingProcessDto>]
  [-ReturnCode <DeploymentReturnCodeDto[]>] [-BuiltInUpdate <BuiltInUpdate>]
  [-AllowAvailableUninstall <Boolean>] [-RemoveDesktopShortcuts <Boolean>]
  [-AppVersionsRetention <Int32>] [-RoleScopeTagId <String[]>] [<CommonParameters>]
```

## Description

Creates the configuration carried by a deployment, as accepted by the deployment create flow.

Anything you do not name is left unset, and the service reads that as "not specified"—the deployment keeps the value it would otherwise have received. That is why this cmdlet sets nothing by default: filling in a field you never mentioned would silently change it.

ReturnCode replaces the deployment's whole set of exit codes rather than adding to it, so pass every code the deployment should end up with.

ConflictingProcess takes a constructed DeploymentConflictingProcessDto. That subtree nests two levels further, into notification and then deferral policy, and has no builders yet.

## Parameters

### -AdditionalArgument

Extra command-line arguments passed to the installer.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -AllowAvailableUninstall

Whether users may uninstall the application from the Company Portal.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Boolean`      |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -AppInfo

Catalogue metadata built by New-PmpcDeploymentAppInfo.

| Attribute      | Value                  |
| -------------- | ---------------------- |
| Type           | `DeploymentAppInfoDto` |
| Required       | False                  |
| Position       | Named                  |
| Pipeline input | True (ByPropertyName)  |
| Aliases        | None                   |

### -AppVersionsRetention

How many superseded versions of the application are retained.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Int32`        |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -BuiltInUpdate

Whether the application's own updater is left enabled.

| Attribute       | Value                         |
| --------------- | ----------------------------- |
| Type            | `BuiltInUpdate`               |
| Required        | False                         |
| Position        | Named                         |
| Pipeline input  | True (ByPropertyName)         |
| Aliases         | None                          |
| Accepted values | NotAvailable, Disable, Enable |

### -ConflictingProcess

Conflicting-process handling. Build this type directly; it has no builder yet.

| Attribute      | Value                             |
| -------------- | --------------------------------- |
| Type           | `DeploymentConflictingProcessDto` |
| Required       | False                             |
| Position       | Named                             |
| Pipeline input | True (ByPropertyName)             |
| Aliases        | None                              |

### -CustomRequirements

Requirements built by New-PmpcDeploymentRequirement.

| Attribute      | Value                                     |
| -------------- | ----------------------------------------- |
| Type           | `EditDeploymentCustomRequirementsRequest` |
| Required       | False                                     |
| Position       | Named                                     |
| Pipeline input | True (ByPropertyName)                     |
| Aliases        | None                                      |

### -InstallLoggingPath

Directory the installer writes its log to.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -RemoveDesktopShortcuts

Whether desktop shortcuts are removed after installing.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Boolean`      |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -ReturnCode

Installer exit codes built by New-PmpcDeploymentReturnCode. Replaces the existing set.

| Attribute      | Value                       |
| -------------- | --------------------------- |
| Type           | `DeploymentReturnCodeDto[]` |
| Required       | False                       |
| Position       | Named                       |
| Pipeline input | True (ByPropertyName)       |
| Aliases        | ReturnCodes                 |

### -RoleScopeTagId

Scope tag IDs applied to the deployment.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String[]`     |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | RoleScopeTagIds       |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### DeploymentConfigurationRequest

The deployment configuration block.

## Examples

### Example 1: Set the install log path

```powershell
New-PmpcDeploymentConfiguration -InstallLoggingPath 'C:\Windows\Logs\Contoso'
```

Sets only the logging path. Every other configuration field stays unspecified, so the deployment keeps its usual values.

### Example 2: Compose requirements and metadata

```powershell
$req  = New-PmpcDeploymentRequirement -MinimumMemoryInMB 8192
$info = New-PmpcDeploymentAppInfo -CustomOwner 'Workplace IT' -IsFeatured $true
New-PmpcDeploymentConfiguration -CustomRequirements $req -AppInfo $info
```

Builds the nested pieces separately and combines them into one configuration.

### Example 3: Replace the exit codes

```powershell
$codes = @(
    New-PmpcDeploymentReturnCode -Code 0 -Type Success
    New-PmpcDeploymentReturnCode -Code 3010 -Type SoftReboot
)
New-PmpcDeploymentConfiguration -ReturnCode $codes
```

The set replaces the deployment's codes outright, so list every code it should have.

## Notes

This cmdlet makes no network call and does not require a session.

## Related links

* [New-PmpcDeploymentAppInfo](new-pmpcdeploymentappinfo.md)
* [New-PmpcDeploymentReturnCode](new-pmpcdeploymentreturncode.md)
* [New-PmpcDeploymentRequirement](new-pmpcdeploymentrequirement.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

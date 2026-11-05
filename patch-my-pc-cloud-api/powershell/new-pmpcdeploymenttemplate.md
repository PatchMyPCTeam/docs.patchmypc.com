---
description: Creates a deployment template.
noIndex: true
noRobotsIndex: true
---

# New-PmpcDeploymentTemplate

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Creates a deployment template.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
New-PmpcDeploymentTemplate -TemplateName <String> [-OsType <OSType>] [-Default]
  [-BuiltInUpdate <BuiltInUpdate>] [-AllowAvailableUninstall] [-RemoveDesktopShortcuts]
  [-AppVersionsRetention <Int32>] [-CustomVendor <String>] [-CustomDeveloper <String>]
  [-CustomOwner <String>] [-CustomNotes <String>] [-CopyForwardAssignments]
  [-CategoryId <String[]>] [-EspProfileId <String[]>] [-RoleScopeTagId <String[]>]
  [-CustomRequirements <EditDeploymentCustomRequirementsRequest>] [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Creates a deployment template on the selected connection. A template is a stored set of deployment settings that a later deployment can start from.

To use a template, pass the result of Get-PmpcDeploymentTemplate to New-PmpcDeployment -Template, which fills in the new deployment's settings the same way the portal does. Creating a deployment doesn't accept a template ID.

Requirements are stated in the same shape a deployment uses, so New-PmpcDeploymentRequirement produces requirements for either.

## Parameters

### -AllowAvailableUninstall

Allow users to uninstall the application from the Company Portal.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | True (ByPropertyName)                          |
| Aliases        | None                                           |

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

### -CategoryId

Intune application category IDs to file the deployment under.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String[]`     |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -Confirm

Prompts you for confirmation before running the cmdlet.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | cf                                             |

### -CopyForwardAssignments

Deployments created from this template inherit the template's assignments.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | True (ByPropertyName)                          |
| Aliases        | None                                           |

### -CustomDeveloper

Developer applied instead of the catalogue's.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -CustomNotes

Free-text notes applied to deployments created from this template.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -CustomOwner

Owner recorded against deployments created from this template.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -CustomRequirements

Custom system requirements. Supplying them replaces the default single-architecture requirement.

| Attribute      | Value                                     |
| -------------- | ----------------------------------------- |
| Type           | `EditDeploymentCustomRequirementsRequest` |
| Required       | False                                     |
| Position       | Named                                     |
| Pipeline input | True (ByPropertyName)                     |
| Aliases        | None                                      |

### -CustomVendor

Publisher applied instead of the catalogue's.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -Default

Make this the connection's default template, demoting whichever template currently holds that position. The default is what a deployment created without a template inherits, so this changes future creates as well as this template.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | True (ByPropertyName)                          |
| Aliases        | None                                           |

### -EspProfileId

Enrollment Status Page profile IDs the deployment participates in.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String[]`     |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -OsType

Operating system the template applies to. Defaults to Windows.

| Attribute       | Value                 |
| --------------- | --------------------- |
| Type            | `OSType`              |
| Required        | False                 |
| Position        | Named                 |
| Pipeline input  | True (ByPropertyName) |
| Aliases         | None                  |
| Accepted values | Windows, MacOS        |

### -RemoveDesktopShortcuts

Remove desktop shortcuts after installing.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | True (ByPropertyName)                          |
| Aliases        | None                                           |

### -RoleScopeTagId

Scope tag IDs applied to deployments created from this template.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String[]`     |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -TemplateName

Name shown when selecting the template.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

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

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### DeploymentTemplateDto

The created template, read back from the service rather than echoed.

## Examples

### Example 1: Create a minimal template

```powershell
New-PmpcDeploymentTemplate -TemplateName 'Standard Windows apps'
```

Creates a template with default settings on the selected connection.

### Example 2: Create a template that carries requirements

```powershell
$reqs = New-PmpcDeploymentRequirement -MinimumWindowsOSVersion Windows11_21H2 -MinimumMemoryInMB 8192
New-PmpcDeploymentTemplate -TemplateName 'Windows 11 baseline' -CustomRequirements $reqs
```

Deployments created from this template start with the same requirements.

### Example 3: Create the connection default

```powershell
New-PmpcDeploymentTemplate -TemplateName 'Company default' -Default
```

Demotes whichever template is currently the default. A connection has exactly one, and it is what a deployment created without a template inherits.

## Notes

Requires a selected company and connection. The template is created on the selected connection; there is no parameter to target another one.

Custom install scripts, PSADT version, and ring configuration cannot be set here: they have no counterpart on the deployment surface this module exposes, so accepting them would store settings this module can neither show nor act on.

## Related links

* [Get-PmpcDeploymentTemplate](get-pmpcdeploymenttemplate.md)
* [Set-PmpcDeploymentTemplate](set-pmpcdeploymenttemplate.md)
* [New-PmpcDeployment](new-pmpcdeployment.md)
* PowerShell module

## See also

* SDK method: [CreateDeploymentTemplateAsync](../sdk/deployment-templates.md#createdeploymenttemplateasync)
* REST operation: [`POST /v1/api/deployments/templates`](../rest-api/applications.md#create-deployment-template)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

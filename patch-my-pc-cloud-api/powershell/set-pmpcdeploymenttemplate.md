---
description: Replaces the settings on a deployment template.
noIndex: true
noRobotsIndex: true
---

# Set-PmpcDeploymentTemplate

## Synopsis

Replaces the settings on a deployment template.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Set-PmpcDeploymentTemplate [-DeploymentTemplateId] <String> -TemplateName <String>
  [-OsType <OSType>] [-Default] [-BuiltInUpdate <BuiltInUpdate>]
  [-AllowAvailableUninstall] [-RemoveDesktopShortcuts] [-AppVersionsRetention <Int32>]
  [-CustomVendor <String>] [-CustomDeveloper <String>] [-CustomOwner <String>]
  [-CustomNotes <String>] [-CopyForwardAssignments] [-CategoryId <String[]>]
  [-EspProfileId <String[]>] [-RoleScopeTagId <String[]>]
  [-CustomRequirements <EditDeploymentCustomRequirementsRequest>] [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Updates an existing deployment template on the selected connection.

This replaces rather than merges: every field is stored as sent, so a setting you do not supply is cleared. Read the template with Get-PmpcDeploymentTemplate first and pass back the values you want to keep.

Updating a template that no longer exists is refused rather than creating a second one under a new id, so a stale id fails visibly instead of silently producing a duplicate.

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

Make this the connection's default template, demoting whichever template currently holds that position.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | True (ByPropertyName)                          |
| Aliases        | None                                           |

### -DeploymentTemplateId

The template to update.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

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

### System.String

A deployment template id, by property name.

## Outputs

### DeploymentTemplateDto

The updated template, read back from the service.

## Examples

### Example 1: Rename a template

```powershell
Set-PmpcDeploymentTemplate -DeploymentTemplateId $templateId -TemplateName 'Windows 11 baseline (2026)'
```

Every other setting is replaced with its default, because the update replaces rather than merges.

### Example 2: Change one setting and keep the rest

```powershell
$t = Get-PmpcDeploymentTemplate -DeploymentTemplateId $templateId
Set-PmpcDeploymentTemplate -DeploymentTemplateId $templateId -TemplateName $t.TemplateName -OsType $t.OsType -CustomRequirements $t.CustomRequirements -AppVersionsRetention 5
```

Reads the current values and passes them back, so only AppVersionsRetention changes.

## Notes

Requires a selected company and connection.

Because the update replaces the whole template, omitting -CustomRequirements clears any requirements the template previously carried. That is the same behavior the portal has, and it is why reading the template first is the safe pattern.

## Related links

* [Get-PmpcDeploymentTemplate](get-pmpcdeploymenttemplate.md)
* [New-PmpcDeploymentTemplate](new-pmpcdeploymenttemplate.md)
* PowerShell module

## See also

* SDK method: [UpdateDeploymentTemplateAsync](../sdk/deployment-templates.md#updatedeploymenttemplateasync)
* REST operation: [`PUT /v1/api/deployments/templates/{deploymentTemplateId}`](../rest-api/applications.md#update-deployment-template)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

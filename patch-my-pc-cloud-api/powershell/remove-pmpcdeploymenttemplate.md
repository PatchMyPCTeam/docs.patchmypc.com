---
description: Deletes a deployment template.
noIndex: true
noRobotsIndex: true
---

# Remove-PmpcDeploymentTemplate

## Synopsis

Deletes a deployment template.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Remove-PmpcDeploymentTemplate [-DeploymentTemplateId] <String> [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Deletes a deployment template from the selected connection.

The connection's default template cannot be deleted. It is what every deployment created without a template inherits, so removing it would change the behavior of future creates in a way the caller cannot see from here. Make another template the default first.

## Parameters

### -Confirm

Prompts you for confirmation before running the cmdlet.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | cf                                             |

### -DeploymentTemplateId

The template to delete.

| Attribute      | Value                          |
| -------------- | ------------------------------ |
| Type           | `System.String`                |
| Required       | True                           |
| Position       | 0                              |
| Pipeline input | True (ByValue, ByPropertyName) |
| Aliases        | None                           |

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

A deployment template id, by value or by property name.

## Outputs

### None

This cmdlet does not return output.

## Examples

### Example 1: Delete a template

```powershell
Remove-PmpcDeploymentTemplate -DeploymentTemplateId $templateId
```

Prompts for confirmation, because deleting a template cannot be undone.

### Example 2: Delete every non-default template

```powershell
Get-PmpcDeploymentTemplate | Where-Object { -not $_.IsDefault } | Remove-PmpcDeploymentTemplate
```

Filtering out the default first avoids a refusal on the one template that cannot be removed.

## Notes

Requires a selected company and connection. Deleting a template does not affect deployments already created from it: a template's settings are copied into the deployment when it is created, not referenced.

## Related links

* [Get-PmpcDeploymentTemplate](get-pmpcdeploymenttemplate.md)
* [New-PmpcDeploymentTemplate](new-pmpcdeploymenttemplate.md)
* PowerShell module

## See also

* SDK method: [DeleteDeploymentTemplateAsync](../sdk/deployment-templates.md#deletedeploymenttemplateasync)
* REST operation: [`DELETE /v1/api/deployments/templates/{deploymentTemplateId}`](../rest-api/applications.md#delete-deployment-template)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

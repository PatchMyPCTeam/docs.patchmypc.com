---
description: Deletes a deployment template.
noIndex: true
noRobotsIndex: true
---

# Remove-PmpcDeploymentTemplate

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Deletes a deployment template.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

{% code collapsedlinecount="10" %}
```powershell
Remove-PmpcDeploymentTemplate [-DeploymentTemplateId] <String> [-WhatIf] [-Confirm]
  [<CommonParameters>]
```
{% endcode %}

## Description

Deletes a deployment template from the selected connection.

The connection's default template cannot be deleted. It is what every deployment created without a template inherits, so removing it would change the behaviour of future creates in a way the caller cannot see from here. Make another template the default first.

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

### Example 1: Delete a template without prompting

{% code collapsedlinecount="10" %}
```powershell
Remove-PmpcDeploymentTemplate -DeploymentTemplateId $templateId -Confirm:$false
```
{% endcode %}

Deletes the specified non-default template without prompting. Omit -Confirm:$false to make PowerShell prompt before deleting the template. The default template cannot be removed.

## Notes

Requires a selected company and connection. Deleting a template does not affect deployments already created from it: a template's settings are copied into the deployment when it is created, not referenced.

## Related links

* [Get-PmpcDeploymentTemplate](get-pmpcdeploymenttemplate.md)
* [New-PmpcDeploymentTemplate](new-pmpcdeploymenttemplate.md)
* [PowerShell module](./)

## See also

* SDK method: [DeleteDeploymentTemplateAsync](../sdk/deployment-templates.md#deletedeploymenttemplateasync)
* REST operation: [`DELETE /v1/api/deployments/templates/{deploymentTemplateId}`](../rest-api/applications.md#delete-deployment-template)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

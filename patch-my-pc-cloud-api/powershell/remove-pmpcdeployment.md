---
description: Deletes an Intune deployment.
noIndex: true
noRobotsIndex: true
---

# Remove-PmpcDeployment

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Deletes an Intune deployment.

## Syntax

{% code collapsedlinecount="10" %}
```powershell
Remove-PmpcDeployment [-ProductId] <Guid> [-DeploymentId] <String> [-WhatIf] [-Confirm]
  [<CommonParameters>]
```
{% endcode %}

## Description

Removes a deployment from Intune on the selected connection.

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

### -DeploymentId

ID of the deployment, as returned by Get-PmpcDeployment.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | 1                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -ProductId

ID of the application. Accepted from the pipeline by property name, so results from Find-PmpcCustomApplication and Get-PmpcCustomApplication can be piped straight in.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Guid`         |
| Required       | True                  |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | Id                    |

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

### DeploymentDto

A deployment, bound by its ProductId and DeploymentId properties.

## Outputs

### None

This cmdlet returns no output.

## Examples

### Example 1: Delete a deployment

{% code collapsedlinecount="10" %}
```powershell
Remove-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId
```
{% endcode %}

Prompts for confirmation, then deletes the deployment.

### Example 2: Delete a deployment after reading it

{% code collapsedlinecount="10" %}
```powershell
$deployment = Get-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId
if (-not $deployment) { throw 'The requested deployment was not found.' }
Remove-PmpcDeployment -ProductId $deployment.ProductId -DeploymentId $deployment.DeploymentId -Confirm:$false
```
{% endcode %}

Reads one deployment by both IDs, then removes that specific deployment without prompting.

## Notes

Only allowed while the deployment is not actively in progress or already being deleted.

Confirmation impact is High, so this prompts by default. Pass -Confirm:$false to suppress it in automation.

## Related links

* [Get-PmpcDeployment](get-pmpcdeployment.md)
* [New-PmpcDeployment](new-pmpcdeployment.md)
* [PowerShell module](./)

## See also

* SDK method: [DeleteDeploymentAsync](../sdk/deployments.md#deletedeploymentasync)
* REST operation: [`DELETE /v1/api/apps/{productId}/deployments/{deploymentId}`](../rest-api/applications.md#delete-application-deployment)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

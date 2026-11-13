---
description: Forces a deployment to be recreated in Intune.
noIndex: true
noRobotsIndex: true
---

# Restart-PmpcDeployment

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Forces a deployment to be recreated in Intune.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Restart-PmpcDeployment [-ProductId] <Guid> [-DeploymentId] <String> [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Recreates a deployment from scratch in Intune. Use it to recover a deployment that is stuck or corrupted.

For routine version updates, use Sync-PmpcDeployment instead: this is the heavier operation and is meant for troubleshooting.

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

### Example 1: Recreate a stuck deployment

```powershell
Restart-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId
```

Forces Intune to recreate the deployment.

### Example 2: Recreate every failed deployment

```powershell
Get-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId | Restart-PmpcDeployment
```

Pipes failed deployments in and recreates each one.

## Notes

Named Restart because it stops the deployment and starts it again, which is what recreation amounts to. The equivalent SDK method is RedeployDeploymentAsync.

## Related links

* [Sync-PmpcDeployment](sync-pmpcdeployment.md)
* [Get-PmpcDeployment](get-pmpcdeployment.md)
* PowerShell module

## See also

* SDK method: [RedeployDeploymentAsync](../sdk/deployments.md#redeploydeploymentasync)
* REST operation: [`PUT /v1/api/apps/{productId}/deployments/{deploymentId}/redeploy`](../rest-api/applications.md#redeploy-application-deployment)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

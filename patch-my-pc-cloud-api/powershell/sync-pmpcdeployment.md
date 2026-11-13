---
description: Syncs a deployment to its latest pending version.
noIndex: true
noRobotsIndex: true
---

# Sync-PmpcDeployment

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Syncs a deployment to its latest pending version.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Sync-PmpcDeployment [-ProductId] <Guid> [-DeploymentId] <String> [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Brings a deployment up to the application's latest pending version. This is the routine way to roll a new version out to an existing deployment.

For a stuck or corrupted deployment, use Restart-PmpcDeployment instead.

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

### Example 1: Sync a deployment

```powershell
Sync-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId
```

Updates the deployment to the latest pending version.

### Example 2: Sync every deployment of an application

```powershell
Get-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId | Sync-PmpcDeployment
```

Rolls the latest version out to all of the application's deployments.

## Notes

Scoped to the connection selected with Set-PmpcConnection.

## Related links

* [Restart-PmpcDeployment](restart-pmpcdeployment.md)
* [Suspend-PmpcDeployment](suspend-pmpcdeployment.md)
* PowerShell module

## See also

* SDK method: [SyncDeploymentAsync](../sdk/deployments.md#syncdeploymentasync)
* REST operation: [`PUT /v1/api/apps/{productId}/deployments/{deploymentId}/sync`](../rest-api/applications.md#sync-application-deployment)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

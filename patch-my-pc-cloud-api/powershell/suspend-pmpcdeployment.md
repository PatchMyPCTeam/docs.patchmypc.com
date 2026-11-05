---
description: Pauses a deployment's scheduled sync.
noIndex: true
noRobotsIndex: true
---

# Suspend-PmpcDeployment

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Pauses a deployment's scheduled sync.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Suspend-PmpcDeployment [-ProductId] <Guid> [-DeploymentId] <String> [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Stops a deployment from picking up new versions automatically. The deployment itself stays in place and installed devices are unaffected; only the scheduled sync is held.

Use Resume-PmpcDeployment to start it again.

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

### Example 1: Pause a deployment

```powershell
Suspend-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId
```

Holds the deployment's scheduled sync.

### Example 2: Pause every deployment during a change freeze

```powershell
Get-PmpcDeployment -ProductId $productId | Suspend-PmpcDeployment
```

Holds all of the application's deployments so no new version rolls out.

## Notes

Pausing is reflected in the SyncOnHold property returned by Get-PmpcDeployment.

## Related links

* [Resume-PmpcDeployment](resume-pmpcdeployment.md)
* [Sync-PmpcDeployment](sync-pmpcdeployment.md)
* PowerShell module

## See also

* SDK method: [SetDeploymentSyncPauseStatusAsync](../sdk/deployments.md#setdeploymentsyncpausestatusasync)
* REST operation: [`PUT /v1/api/apps/{productId}/deployments/{deploymentId}/scheduled-sync-pause`](../rest-api/applications.md#set-application-deployment-sync-pause-status)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

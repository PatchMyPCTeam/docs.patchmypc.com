---
description: Resumes a deployment's scheduled sync.
noIndex: true
noRobotsIndex: true
---

# Resume-PmpcDeployment

## Synopsis

Resumes a deployment's scheduled sync.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Resume-PmpcDeployment [-ProductId] <Guid> [-DeploymentId] <String> [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Restarts automatic version pickup for a deployment that was paused with Suspend-PmpcDeployment.

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

### Example 1: Resume a deployment

```powershell
Resume-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId
```

Restarts the deployment's scheduled sync.

### Example 2: Resume everything that was paused

```powershell
Get-PmpcDeployment -ProductId $productId | Where-Object SyncOnHold | Resume-PmpcDeployment
```

Finds the paused deployments and restarts each one.

## Notes

Resuming does not itself push a new version. Use Sync-PmpcDeployment to update immediately.

## Related links

* [Suspend-PmpcDeployment](suspend-pmpcdeployment.md)
* [Sync-PmpcDeployment](sync-pmpcdeployment.md)
* PowerShell module

## See also

* SDK method: [SetDeploymentSyncPauseStatusAsync](../sdk/deployments.md#setdeploymentsyncpausestatusasync)
* REST operation: [`PUT /v1/api/apps/{productId}/deployments/{deploymentId}/scheduled-sync-pause`](../rest-api/applications.md#set-application-deployment-sync-pause-status)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

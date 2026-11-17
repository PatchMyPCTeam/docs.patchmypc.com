---
description: Gets an application's Intune deployments, or one deployment in full.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcDeployment

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Gets an application's Intune deployments, or one deployment in full.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

### List (Default)

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcDeployment [-ProductId] <Guid> [<CommonParameters>]
```
{% endcode %}

### Detail

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcDeployment [-ProductId] <Guid> [-DeploymentId] <String> [<CommonParameters>]
```
{% endcode %}

## Description

Without -DeploymentId, lists every deployment of the application on the selected connection.

Both forms include nullable CatalogEntryId alongside the existing ProductId. CatalogEntryId is the stored category identifier: the selected public variant or the customer-owned custom catalog entry. Older deployments without a stored category identifier return null; the identity is never inferred from the current catalog and does not pin a version or revision.

With -DeploymentId, returns that one deployment in full, including its categories, Enrollment Status Page profiles and dependency chain. Those fields are deliberately left off the list form to avoid an extra backend round-trip per item.

## Parameters

### -DeploymentId

Return this one deployment in full instead of listing them all.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | 1                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |
| Parameter sets | Detail                |

### -ProductId

ID of the application. Accepted from the pipeline by property name, so results from Find-PmpcCustomApplication and Get-PmpcCustomApplication can be piped straight in.

| Attribute      | Value                          |
| -------------- | ------------------------------ |
| Type           | `System.Guid`                  |
| Required       | True                           |
| Position       | 0                              |
| Pipeline input | True (ByValue, ByPropertyName) |
| Aliases        | Id                             |
| Parameter sets | All                            |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### System.Guid

The product ID, by value or by the Id/ProductId property.

## Outputs

### DeploymentDto

One object per deployment.

### DeploymentDetailDto

The full deployment, when -DeploymentId is supplied.

## Examples

### Example 1: List an application's deployments

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcDeployment -ProductId $productId
```
{% endcode %}

Returns each deployment with its status and target operating system.

### Example 2: Get one deployment in full

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId
```
{% endcode %}

Returns the deployment including categories, ESP profiles and its parent and child deployments.

### Example 3: Find failed deployments

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcDeployment -ProductId $productId | Where-Object Status -eq 'Failed'
```
{% endcode %}

Filters the list down to deployments that need attention.

## Notes

Scoped to the connection selected with Set-PmpcConnection.

## Related links

* [New-PmpcDeployment](new-pmpcdeployment.md)
* [Set-PmpcDeployment](set-pmpcdeployment.md)
* [PowerShell module](./)

## See also

* SDK method: [GetDeploymentsAsync](../sdk/deployments.md#getdeploymentsasync)
* SDK method: [GetDeploymentDetailsAsync](../sdk/deployments.md#getdeploymentdetailsasync)
* REST operation: [`GET /v1/api/apps/{productId}/deployments`](../rest-api/applications.md#get-application-deployments)
* REST operation: [`GET /v1/api/apps/{productId}/deployments/{deploymentId}`](../rest-api/applications.md#get-application-deployment-details)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

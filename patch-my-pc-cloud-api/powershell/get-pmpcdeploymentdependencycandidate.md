---
description: Lists deployments that can be used as a dependency.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcDeploymentDependencyCandidate

## Synopsis

Lists deployments that can be used as a dependency.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Get-PmpcDeploymentDependencyCandidate [-ProductId] <Guid> [<CommonParameters>]
```

## Description

Returns the deployments eligible to be a parent of a new or edited deployment, for use with the -ParentDeploymentId parameter of New-PmpcDeployment and Set-PmpcDeployment.

## Parameters

### -ProductId

The application whose dependencies are being configured. Informational only: the candidate list is connection-wide.

| Attribute      | Value                          |
| -------------- | ------------------------------ |
| Type           | `System.Guid`                  |
| Required       | True                           |
| Position       | 0                              |
| Pipeline input | True (ByValue, ByPropertyName) |
| Aliases        | Id                             |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### System.Guid

The product ID, by value or by the Id/ProductId property.

## Outputs

### DeploymentDependencyDto

One object per candidate deployment.

## Examples

### Example 1: List dependency candidates

```powershell
Get-PmpcDeploymentDependencyCandidate -ProductId $productId
```

Returns every deployment on the connection that could be a dependency.

### Example 2: Find a specific dependency

```powershell
Get-PmpcDeploymentDependencyCandidate -ProductId $productId | Where-Object Name -like '*Visual C++*'
```

Narrows a connection-wide list down to the runtime the application depends on.

## Notes

The candidate list is connection-wide rather than product-scoped. The product ID is informational. Every deployment on the connection is returned; filter the results yourself.

## Related links

* [New-PmpcDeployment](new-pmpcdeployment.md)
* [Set-PmpcDeployment](set-pmpcdeployment.md)
* PowerShell module

## See also

* SDK method: [GetDeploymentDependencyCandidatesAsync](../sdk/deployments.md#getdeploymentdependencycandidatesasync)
* REST operation: [`GET /v1/api/apps/{productId}/deployments/dependency-candidates`](../rest-api/applications.md#get-application-deployment-dependency-candidates)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

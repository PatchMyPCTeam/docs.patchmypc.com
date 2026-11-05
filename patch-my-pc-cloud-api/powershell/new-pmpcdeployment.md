---
description: Creates an Intune deployment for an application.
noIndex: true
noRobotsIndex: true
---

# New-PmpcDeployment

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Creates an Intune deployment for an application.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

### Properties (Default)

```powershell
New-PmpcDeployment [-ProductId] <Guid> [-OsType] <OSType>
  [-Assignment <CreateDeploymentAssignmentRequest[]>] [-CategoryId <String[]>]
  [-EspProfileId <String[]>] [-ParentDeploymentId <String[]>]
  [-Template <DeploymentTemplateDto>] [-Configuration <DeploymentConfigurationRequest>]
  [-WhatIf] [-Confirm] [<CommonParameters>]
```

### Request

```powershell
New-PmpcDeployment [-ProductId] <Guid> -Request <CreateDeploymentRequest> [-WhatIf]
  [-Confirm] [<CommonParameters>]
```

## Description

Deploys an application to Intune on the selected connection, with the given target operating system and group assignments.

The selected connection is applied automatically; any connection set on a request object is overwritten.

## Parameters

### -Assignment

Group assignments, built with New-PmpcDeploymentAssignment.

| Attribute      | Value                                 |
| -------------- | ------------------------------------- |
| Type           | `CreateDeploymentAssignmentRequest[]` |
| Required       | False                                 |
| Position       | Named                                 |
| Pipeline input | False                                 |
| Aliases        | Assignments                           |
| Parameter sets | Properties                            |

### -CategoryId

Intune application category IDs to file the deployment under.

| Attribute      | Value             |
| -------------- | ----------------- |
| Type           | `System.String[]` |
| Required       | False             |
| Position       | Named             |
| Pipeline input | False             |
| Aliases        | CategoryIds       |
| Parameter sets | Properties        |

### -Configuration

Deployment configuration: conflicting-process behavior, return codes, requirements, install parameters, app-info overrides, and the portal's behavior toggles. Build it with New-PmpcDeploymentConfiguration. Anything left unset gets the value a deployment created without a configuration would have received.

| Attribute      | Value                            |
| -------------- | -------------------------------- |
| Type           | `DeploymentConfigurationRequest` |
| Required       | False                            |
| Position       | Named                            |
| Pipeline input | False                            |
| Aliases        | None                             |
| Parameter sets | Properties                       |

### -Confirm

Prompts you for confirmation before running the cmdlet.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | cf                                             |

### -EspProfileId

Enrollment Status Page profile IDs the deployment participates in.

| Attribute      | Value             |
| -------------- | ----------------- |
| Type           | `System.String[]` |
| Required       | False             |
| Position       | Named             |
| Pipeline input | False             |
| Aliases        | EspProfileIds     |
| Parameter sets | Properties        |

### -OsType

Operating system the deployment targets. When -Template is used it must match the template's own OsType.

| Attribute       | Value          |
| --------------- | -------------- |
| Type            | `OSType`       |
| Required        | True           |
| Position        | 1              |
| Pipeline input  | False          |
| Aliases         | None           |
| Accepted values | Windows, MacOS |
| Parameter sets  | Properties     |

### -ParentDeploymentId

IDs of deployments this one depends on. Candidates come from Get-PmpcDeploymentDependencyCandidate.

| Attribute      | Value               |
| -------------- | ------------------- |
| Type           | `System.String[]`   |
| Required       | False               |
| Position       | Named               |
| Pipeline input | False               |
| Aliases        | ParentDeploymentIds |
| Parameter sets | Properties          |

### -ProductId

The application to deploy. Binds by property name from a piped object with a ProductId property.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Guid`         |
| Required       | True                  |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | Id                    |
| Parameter sets | All                   |

### -Request

A fully-built request object, for callers that already construct one. Mutually exclusive with the individual property parameters.

| Attribute      | Value                     |
| -------------- | ------------------------- |
| Type           | `CreateDeploymentRequest` |
| Required       | True                      |
| Position       | Named                     |
| Pipeline input | True (ByValue)            |
| Aliases        | None                      |
| Parameter sets | Request                   |

### -Template

A template whose settings the deployment starts from, from Get-PmpcDeploymentTemplate. Anything you pass explicitly wins, and template fields this cmdlet cannot set (install scripts, PSADT version, rings, CreateWithDelay, CopyForwardAssignments) are not applied. The template's OsType must match -OsType: a template belongs to one operating system, and a mismatch is refused rather than applied.

| Attribute      | Value                   |
| -------------- | ----------------------- |
| Type           | `DeploymentTemplateDto` |
| Required       | False                   |
| Position       | Named                   |
| Pipeline input | True (ByValue)          |
| Aliases        | None                    |
| Parameter sets | Properties              |

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

### CreateDeploymentRequest

A pre-built creation request, bound to -Request.

## Outputs

### DeploymentDto

The created deployment.

## Examples

### Example 1: Create a deployment

```powershell
New-PmpcDeployment -ProductId $productId -OsType Windows -Assignment (New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required)
```

Deploys the application to Windows devices in the group as a required install.

### Example 2: Create a deployment with a dependency

```powershell
$parent = Get-PmpcDeploymentDependencyCandidate -ProductId $productId | Where-Object Name -like '*Visual C++*'
New-PmpcDeployment -ProductId $productId -OsType Windows -Assignment $assignment -ParentDeploymentId $parent.Id
```

Makes the deployment depend on an existing one, so the runtime installs first.

### Example 3: Create a deployment from a template

```powershell
$t = Get-PmpcDeploymentTemplate | Where-Object IsDefault
New-PmpcDeployment -ProductId $productId -OsType Windows -Template $t
```

Starts from the connection's default template. The template supplies categories, Enrollment Status Page (ESP) profiles, scope tags, and the configuration block.

### Example 4: Override one thing the template sets

```powershell
New-PmpcDeployment -ProductId $productId -OsType Windows -Template $t -CategoryId $categoryId
```

The explicit category wins; everything else still comes from the template.

### Example 5: Create a deployment with a configuration

```powershell
$config = New-PmpcDeploymentConfiguration -AdditionalArgument '/qn' -AppVersionsRetention 3
New-PmpcDeployment -ProductId $productId -OsType Windows -Assignment $assignment -Configuration $config
```

Sets installer arguments and version retention at create time; anything left unset gets the deployment's normal default.

## Notes

Requires a connection selected with Set-PmpcConnection.

## Related links

* [New-PmpcDeploymentAssignment](new-pmpcdeploymentassignment.md)
* [Get-PmpcDeployment](get-pmpcdeployment.md)
* [Set-PmpcDeployment](set-pmpcdeployment.md)
* PowerShell module

## See also

* SDK method: [CreateDeploymentAsync](../sdk/deployments.md#createdeploymentasync)
* REST operation: [`POST /v1/api/apps/{productId}/deployments`](../rest-api/applications.md#create-application-deployment)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

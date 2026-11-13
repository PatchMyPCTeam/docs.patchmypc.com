---
description: Changes an existing Intune deployment.
noIndex: true
noRobotsIndex: true
---

# Set-PmpcDeployment

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Changes an existing Intune deployment.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

### Properties (Default)

```powershell
Set-PmpcDeployment [-ProductId] <Guid> [-DeploymentId] <String> [-Name <String>]
  [-Assignment <CreateDeploymentAssignmentRequest[]>]
  [-Configuration <DeploymentConfigurationRequest>] [-CategoryId <String[]>]
  [-EspProfileId <String[]>] [-ParentDeploymentId <String[]>] [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

### Request

```powershell
Set-PmpcDeployment [-ProductId] <Guid> [-DeploymentId] <String>
  -Request <EditDeploymentRequest> [-WhatIf] [-Confirm] [<CommonParameters>]
```

## Description

Edits a deployment's name, assignments, categories, Enrollment Status Page profiles, dependencies, and its configuration—conflicting-process behavior, return codes, requirements, install parameters, app-info overrides, and the portal's behavior toggles.

Everything you do not specify is preserved unchanged, including every configuration field you do not name. Fields outside this surface (rings, custom scripts, extra files) are preserved too and cannot be changed here.

## Parameters

### -Assignment

Replacement group assignments, built with New-PmpcDeploymentAssignment. An empty array clears them.

| Attribute      | Value                                 |
| -------------- | ------------------------------------- |
| Type           | `CreateDeploymentAssignmentRequest[]` |
| Required       | False                                 |
| Position       | Named                                 |
| Pipeline input | False                                 |
| Aliases        | Assignments                           |
| Parameter sets | Properties                            |

### -CategoryId

Replacement Intune category IDs. An empty array clears them.

| Attribute      | Value             |
| -------------- | ----------------- |
| Type           | `System.String[]` |
| Required       | False             |
| Position       | Named             |
| Pipeline input | False             |
| Aliases        | CategoryIds       |
| Parameter sets | Properties        |

### -Configuration

Deployment configuration changes: conflicting-process behavior, return codes, requirements, install parameters, app-info overrides, and the portal's behavior toggles. Any member left unset keeps the deployment's current value. Build it with New-PmpcDeploymentConfiguration.

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

### -DeploymentId

ID of the deployment, as returned by Get-PmpcDeployment.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | 1                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |
| Parameter sets | All                   |

### -EspProfileId

Replacement Enrollment Status Page profile IDs. An empty array clears them.

| Attribute      | Value             |
| -------------- | ----------------- |
| Type           | `System.String[]` |
| Required       | False             |
| Position       | Named             |
| Pipeline input | False             |
| Aliases        | EspProfileIds     |
| Parameter sets | Properties        |

### -Name

New name for the deployment.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Properties      |

### -ParentDeploymentId

Replacement dependency deployment IDs. An empty array clears them.

| Attribute      | Value               |
| -------------- | ------------------- |
| Type           | `System.String[]`   |
| Required       | False               |
| Position       | Named               |
| Pipeline input | False               |
| Aliases        | ParentDeploymentIds |
| Parameter sets | Properties          |

### -ProductId

ID of the application. Accepted from the pipeline by property name, so results from Find-PmpcCustomApplication and Get-PmpcCustomApplication can be piped straight in.

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

| Attribute      | Value                   |
| -------------- | ----------------------- |
| Type           | `EditDeploymentRequest` |
| Required       | True                    |
| Position       | Named                   |
| Pipeline input | True (ByValue)          |
| Aliases        | None                    |
| Parameter sets | Request                 |

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

### EditDeploymentRequest

A pre-built edit request, bound to -Request.

## Outputs

### DeploymentDto

The updated deployment.

## Examples

### Example 1: Rename a deployment

```powershell
Set-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId -Name '7-Zip (Pilot)'
```

Changes only the name; assignments and every other setting are untouched.

### Example 2: Replace the assignments

```powershell
Set-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId -Assignment (New-PmpcDeploymentAssignment -GroupId $groupId -Intent Available)
```

Replaces the deployment's group assignments with a single available assignment.

### Example 3: Change one configuration setting

```powershell
$config = New-PmpcDeploymentConfiguration -AppVersionsRetention 5
Set-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId -Configuration $config
```

Changes only the retention count. Every other configuration setting the deployment already has, including its conflicting-process behaviour and return codes, is left alone.

### Example 4: Change the installer arguments

```powershell
$config = New-PmpcDeploymentConfiguration -AdditionalArgument '/qn REBOOT=ReallySuppress'
Set-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId -Configuration $config
```

AdditionalArgument is a member of -Configuration; it used to be a parameter of its own.

### Example 5: Remove all categories

```powershell
Set-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId -CategoryId @()
```

An explicitly empty array clears the categories; omitting the parameter would keep them.

## Notes

Not supported for ring-enabled deployments.

Collection parameters distinguish 'not mentioned' from 'cleared': omitting -CategoryId keeps the current categories, while passing an empty array removes them. The same applies inside -Configuration, where a null member keeps the current value and an empty collection clears it.

The selected connection is applied automatically; any connection set on a request object is overwritten.

## Related links

* [Get-PmpcDeployment](get-pmpcdeployment.md)
* [New-PmpcDeployment](new-pmpcdeployment.md)
* PowerShell module

## See also

* SDK method: [EditDeploymentAsync](../sdk/deployments.md#editdeploymentasync)
* REST operation: [`PUT /v1/api/apps/{productId}/deployments/{deploymentId}`](../rest-api/applications.md#edit-application-deployment)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

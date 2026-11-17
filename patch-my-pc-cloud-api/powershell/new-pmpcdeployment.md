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

### Request (Default)

```powershell
New-PmpcDeployment [-ProductId] <Guid> -Request <CreateDeploymentRequest> [-WhatIf]
  [-Confirm] [<CommonParameters>]
```

### Properties

```powershell
New-PmpcDeployment [-ProductId] <Guid> [-OsType] <OSType> -CatalogEntryId <Guid>
  [-Assignment <CreateDeploymentAssignmentRequest[]>] [-CategoryId <String[]>]
  [-EspProfileId <String[]>] [-ParentDeploymentId <String[]>]
  [-Template <DeploymentTemplateDto>] [-Configuration <DeploymentConfigurationRequest>]
  [-WhatIf] [-Confirm] [<CommonParameters>]
```

## Description

Deploys a custom or public application to Intune using its ProductId and an explicit, non-empty CatalogEntryId. Custom details expose the canonical entry under Custom; public details expose selectable Variants. Pipe custom details, their Custom block, or one explicitly selected public variant to supply both IDs.

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

### -CatalogEntryId

Required non-empty recipe ID from custom details or an explicitly selected public variant. Binds from supported typed pipeline selections or by property name. Never substitute ProductId or UpdateId.

| Attribute      | Value                          |
| -------------- | ------------------------------ |
| Type           | `System.Guid`                  |
| Required       | True                           |
| Position       | Named                          |
| Pipeline input | True (ByValue, ByPropertyName) |
| Aliases        | None                           |
| Parameter sets | Properties                     |

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

Deployment configuration: conflicting-process behaviour, return codes, requirements, install parameters, app-info overrides and the portal's behaviour toggles. Anything left unset gets the value a deployment created without a configuration would have received.

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

Operating system the deployment targets. Binds by property name from a selected public variant; supply it explicitly for custom details. When -Template is used it must match the template's own OsType.

| Attribute       | Value                 |
| --------------- | --------------------- |
| Type            | `OSType`              |
| Required        | True                  |
| Position        | 1                     |
| Pipeline input  | True (ByPropertyName) |
| Aliases         | None                  |
| Accepted values | Windows, MacOS        |
| Parameter sets  | Properties            |

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

The owning application/product context. Binds by property name from custom details, their Custom block, or a selected public variant. Both this ID and CatalogEntryId are required.

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

A template whose settings the deployment starts from, from Get-PmpcDeploymentTemplate. Applied client-side: anything you pass explicitly wins, and template fields this create surface cannot express (install scripts, PSADT version, rings, CreateWithDelay, CopyForwardAssignments) are not applied. The template's OsType must match -OsType: a template belongs to one operating system, and a mismatch is refused rather than applied.

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

### CustomApplicationDto

Custom details, supplying ProductId and the nested Custom.CatalogEntryId.

### CustomApplicationDetailsDto

A standalone Custom detail block supplying both IDs.

### PublicApplicationVariantDto

One explicitly selected public variant supplying both IDs and OsType.

## Outputs

### DeploymentDto

The created deployment.

## Examples

### Example 1: Create a custom application deployment

```powershell
Get-PmpcCustomApplication -ProductId $productId | New-PmpcDeployment -OsType Windows -Assignment (New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required)
```

The typed custom details supply ProductId and Custom.CatalogEntryId. No product/update ID fallback or automatic catalog lookup occurs during creation.

### Example 2: Pipe a standalone custom detail block

```powershell
$details = Get-PmpcCustomApplication -ProductId $productId
$assignment = New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required
$details.Custom | New-PmpcDeployment -OsType Windows -Assignment $assignment
```

The canonical Custom block carries both ProductId and CatalogEntryId.

### Example 3: Choose a public catalog variant

```powershell
$app = Get-PmpcApplication -ProductId $productId -OsType Windows
$variants = @($app.Variants | Where-Object { $_.Architecture -eq 'X64' -and $_.InstallerType -eq 'MSI' -and $_.InstallContext -eq 'System' -and $_.Language -eq $language })
if ($variants.Count -ne 1) { throw 'Choose exactly one installer combination from Variants.' }
$variants[0] | New-PmpcDeployment -Assignment (New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required)
```

Set $language to the desired value from the returned variants and choose the installer combination deliberately. The selected variant supplies ProductId, CatalogEntryId and OsType. Nothing automatically selects the first variant.

### Example 4: Create a deployment with a dependency

```powershell
$app = Get-PmpcCustomApplication -ProductId $productId
$parent = @(Get-PmpcDeploymentDependencyCandidate -ProductId $app.ProductId | Where-Object DeploymentId -eq $parentDeploymentId)
if ($parent.Count -ne 1) { throw 'Choose exactly one intended deployment from the dependency candidates.' }
$assignment = New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required
New-PmpcDeployment -ProductId $app.ProductId -CatalogEntryId $app.Custom.CatalogEntryId -OsType Windows -Assignment $assignment -ParentDeploymentId $parent[0].DeploymentId
```

Set $parentDeploymentId to the ID of the intended prerequisite deployment, chosen from the candidates. This configures the dependency rather than choosing an arbitrary deployment on the connection; it does not wait for installation on a device.

### Example 5: Create a deployment from the default template

```powershell
$app = Get-PmpcCustomApplication -ProductId $productId
$summary = Get-PmpcDeploymentTemplate | Where-Object IsDefault | Select-Object -First 1
if (-not $summary) { throw 'No default deployment template is configured for this connection.' }
$t = Get-PmpcDeploymentTemplate -DeploymentTemplateId $summary.DeploymentTemplateId
$assignment = New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required
New-PmpcDeployment -ProductId $app.ProductId -CatalogEntryId $app.Custom.CatalogEntryId -OsType Windows -Template $t -Assignment $assignment
```

Reads the default template summary, then retrieves its detailed settings before applying it. The template supplies categories, Enrollment Status Page (ESP) profiles, scope tags, and the configuration block.

### Example 6: Override one thing the template sets

```powershell
$app = Get-PmpcCustomApplication -ProductId $productId
$summary = Get-PmpcDeploymentTemplate | Where-Object IsDefault | Select-Object -First 1
if (-not $summary) { throw 'No default deployment template is configured for this connection.' }
$t = Get-PmpcDeploymentTemplate -DeploymentTemplateId $summary.DeploymentTemplateId
$assignment = New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required
New-PmpcDeployment -ProductId $app.ProductId -CatalogEntryId $app.Custom.CatalogEntryId -OsType Windows -Template $t -CategoryId $categoryId -Assignment $assignment
```

The explicit category wins; everything else still comes from the template. Define $categoryId as an Intune category ID for your tenant.

### Example 7: Create a deployment with a configuration

```powershell
$app = Get-PmpcCustomApplication -ProductId $productId
$config = New-PmpcDeploymentConfiguration -AdditionalArgument '/qn' -AppVersionsRetention 3
New-PmpcDeployment -ProductId $app.ProductId -CatalogEntryId $app.Custom.CatalogEntryId -OsType Windows -Assignment (New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required) -Configuration $config
```

Sets installer arguments and version retention at create time; anything left unset gets the deployment's normal default.

### Example 8: Create a deployment from a specific template

```powershell
$app = Get-PmpcCustomApplication -ProductId $productId
$t = Get-PmpcDeploymentTemplate -DeploymentTemplateId $templateId
$assignment = New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required
New-PmpcDeployment -ProductId $app.ProductId -CatalogEntryId $app.Custom.CatalogEntryId -OsType Windows -Template $t -Assignment $assignment
```

Set $templateId to the ID of the Windows template you want to apply, listed by Get-PmpcDeploymentTemplate. This retrieves its full settings and applies its categories, ESP profiles, scope tags, supported configuration settings and requirements without making it the default template. The assignment is supplied explicitly; this does not wait for publication or installation.

## Notes

Requires a connection selected with Set-PmpcConnection. Custom search results must first pass through Get-PmpcCustomApplication. Public families and option blocks are not selections; choose exactly one Variants entry. Winget deployments are unsupported.

CatalogEntryId is a durable recipe identity, not ProductId or UpdateId. Creation validates the entry again and uses AppCat's current eligible metadata at lookup, not a version pin or an atomic latest-at-commit guarantee. A pre-built -Request must also carry CatalogEntryId.

## Related links

* [New-PmpcDeploymentAssignment](new-pmpcdeploymentassignment.md)
* [Get-PmpcDeployment](get-pmpcdeployment.md)
* [Set-PmpcDeployment](set-pmpcdeployment.md)
* PowerShell module

## See also

* SDK method: [CreateDeploymentAsync](../sdk/deployments.md#createdeploymentasync)
* REST operation: [`POST /v1/api/apps/{productId}/deployments`](../rest-api/applications.md#create-application-deployment)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

---
description: Lists deployment templates, or reads one in detail.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcDeploymentTemplate

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Lists deployment templates, or reads one in detail.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Get-PmpcDeploymentTemplate [-DeploymentTemplateId] <String> [<CommonParameters>]
```

## Description

Retrieves the deployment templates configured for the selected connection, or the settings of a single template.

A template is a stored set of deployment settings. To use one, pass the result to New-PmpcDeployment -Template, which fills in the new deployment's settings the same way the portal does. Creating a deployment doesn't accept a template ID.

Author templates with New-PmpcDeploymentTemplate, change them with Set-PmpcDeploymentTemplate.

Requirements come back in the same shape a deployment's own detail returns, so New-PmpcDeploymentRequirement produces requirements for either.

## Parameters

### -DeploymentTemplateId

The template to read. Omit it to list every template on the selected connection.

| Attribute      | Value                          |
| -------------- | ------------------------------ |
| Type           | `System.String`                |
| Required       | True                           |
| Position       | 0                              |
| Pipeline input | True (ByValue, ByPropertyName) |
| Aliases        | None                           |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### System.String

A deployment template id, by value or by property name.

## Outputs

### DeploymentTemplateSummaryDto

One entry per template when listing.

### DeploymentTemplateDto

The template settings when an id is supplied.

## Examples

### Example 1: List the templates on the selected connection

```powershell
Get-PmpcDeploymentTemplate
```

Returns every template, including which one is the connection default.

### Example 2: Find the default template

```powershell
Get-PmpcDeploymentTemplate | Where-Object IsDefault
```

The default is what a deployment created without a template inherits.

### Example 3: Read one template in detail

```powershell
Get-PmpcDeploymentTemplate -DeploymentTemplateId $templateId
```

Returns the settings a deployment created from this template would inherit.

## Notes

Requires a selected company and connection. Custom install scripts, PSADT version, ring configuration, and CreateWithDelay are not returned: they have no counterpart on the deployment surface this module exposes.

## Related links

* [New-PmpcDeployment](new-pmpcdeployment.md)
* [New-PmpcDeploymentRequirement](new-pmpcdeploymentrequirement.md)
* PowerShell module

## See also

* SDK method: [GetDeploymentTemplatesAsync](../sdk/deployment-templates.md#getdeploymenttemplatesasync)
* SDK method: [GetDeploymentTemplateAsync](../sdk/deployment-templates.md#getdeploymenttemplateasync)
* REST operation: [`GET /v1/api/deployments/templates`](../rest-api/applications.md#get-deployment-templates)
* REST operation: [`GET /v1/api/deployments/templates/{deploymentTemplateId}`](../rest-api/applications.md#get-deployment-template-details)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

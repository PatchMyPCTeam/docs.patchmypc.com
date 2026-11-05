---
description: Builds the catalogue metadata shown for a deployment.
noIndex: true
noRobotsIndex: true
---

# New-PmpcDeploymentAppInfo

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Builds the catalogue metadata shown for a deployment.

## Syntax

```powershell
New-PmpcDeploymentAppInfo [[-CustomVendor] <String>] [-CustomDeveloper <String>]
  [-CustomOwner <String>] [-CustomDescription <String>] [-CustomNotes <String>]
  [-CustomInformationUrl <String>] [-CustomPrivacyUrl <String>] [-IsFeatured <Boolean>]
  [<CommonParameters>]
```

## Description

Creates the app-information overrides carried by a deployment configuration.

Each value replaces what the catalogue supplies for that field. Anything you do not name is left unset, so the catalogue value survives.

## Parameters

### -CustomDescription

Description shown instead of the catalogue's.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -CustomDeveloper

Developer shown instead of the catalogue's.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -CustomInformationUrl

Information URL shown instead of the catalogue's.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -CustomNotes

Free-text notes stored with the deployment.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -CustomOwner

Owner recorded against the deployment.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -CustomPrivacyUrl

Privacy URL shown instead of the catalogue's.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -CustomVendor

Publisher shown instead of the catalogue's.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -IsFeatured

Whether the application is featured in the Company Portal.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Boolean`      |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### DeploymentAppInfoDto

The deployment app-information overrides.

## Examples

### Example 1: Override the owner

```powershell
New-PmpcDeploymentAppInfo -CustomOwner 'Workplace IT'
```

Sets the owner and leaves every other catalogue value in place.

### Example 2: Feature the application

```powershell
New-PmpcDeploymentAppInfo -IsFeatured $true -CustomDescription 'Approved browser'
```

Features the application in the Company Portal and replaces its description.

## Notes

This cmdlet makes no network call and does not require a session.

## Related links

* [New-PmpcDeploymentConfiguration](new-pmpcdeploymentconfiguration.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

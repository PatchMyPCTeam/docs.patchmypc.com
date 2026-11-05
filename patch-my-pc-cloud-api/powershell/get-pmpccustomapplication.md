---
description: Gets the details of a single custom application.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcCustomApplication

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Gets the details of a single custom application.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Get-PmpcCustomApplication [-ProductId] <Guid> [<CommonParameters>]
```

## Description

Returns the full metadata of one custom application: display name, vendor, version, install arguments, detection rules, and requirements.

## Parameters

### -ProductId

ID of the custom application to retrieve.

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

### CustomApplicationDto

The custom application's details.

## Examples

### Example 1: Get a custom application

```powershell
Get-PmpcCustomApplication -ProductId $productId
```

Returns the custom application details.

### Example 2: Look up search results

```powershell
Find-PmpcCustomApplication -DisplayName '7-Zip' | Get-PmpcCustomApplication
```

Pipes each search result in by its Id property to fetch full details.

## Notes

The returned object does not include the application's file list; use Get-PmpcApplicationFile for that.

## Related links

* [Find-PmpcCustomApplication](find-pmpccustomapplication.md)
* [Get-PmpcApplicationFile](get-pmpcapplicationfile.md)
* [New-PmpcCustomApplication](new-pmpccustomapplication.md)
* PowerShell module

## See also

* SDK method: [GetCustomApplicationDetailsAsync](../sdk/custom-applications.md#getcustomapplicationdetailsasync)
* REST operation: [`GET /v1/api/apps/custom/{productId}`](../rest-api/applications.md#get-custom-application-details)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

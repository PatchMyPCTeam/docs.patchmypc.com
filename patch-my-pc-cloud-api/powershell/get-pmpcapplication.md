---
description: Gets the details of a single public catalog application.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcApplication

## Synopsis

Gets the details of a single public catalog application.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Get-PmpcApplication [-ProductId] <Guid> [-ConnectionId <Guid>] [-OsType <OSType>]
  [<CommonParameters>]
```

## Description

Returns the metadata of one public catalog application from Patch My PC.

## Parameters

### -ConnectionId

Intune connection scoping the lookup. If omitted, the session's selected connection is used.

| Attribute      | Value         |
| -------------- | ------------- |
| Type           | `System.Guid` |
| Required       | False         |
| Position       | Named         |
| Pipeline input | False         |
| Aliases        | None          |

### -OsType

The operating system to resolve the product for. Defaults to Windows when omitted, matching this cmdlet's existing behavior. MacOS additionally requires the customer to be entitled to the "macOS Applications" feature; when they are not, the product is reported as not found rather than the command failing.

| Attribute       | Value          |
| --------------- | -------------- |
| Type            | `OSType`       |
| Required        | False          |
| Position        | Named          |
| Pipeline input  | False          |
| Aliases         | None           |
| Accepted values | Windows, MacOS |

### -ProductId

ID of the public catalog application to retrieve.

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

### PublicApplicationDto

The public catalog application's details.

## Examples

### Example 1: Get a public catalog application

```powershell
Get-PmpcApplication -ProductId $productId
```

Returns the public catalog application details using the session's selected connection.

### Example 2: Get with an explicit connection

```powershell
Get-PmpcApplication -ProductId $productId -ConnectionId $connectionId
```

Resolves the product from the Patch My PC public catalog using the specified connection.

### Example 3: Look up search results

```powershell
Find-PmpcApplication -DisplayName '7-Zip' | Get-PmpcApplication
```

Pipes each search result in by its Id property to fetch full public application details.

## Notes

Resolving a public catalog application requires an Intune connection. If -ConnectionId is omitted, the session's selected connection is used.

## Related links

* [Find-PmpcApplication](find-pmpcapplication.md)
* [Get-PmpcConnection](get-pmpcconnection.md)
* PowerShell module

## See also

* SDK method: [GetPublicApplicationDetailsAsync](../sdk/applications.md#getpublicapplicationdetailsasync)
* REST operation: [`GET /v1/api/apps/public/{productId}`](../rest-api/applications.md#get-public-application-details)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

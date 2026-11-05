---
description: Lists the files that make up an application's current version.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcApplicationFile

## Synopsis

Lists the files that make up an application's current version.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Get-PmpcApplicationFile [-ProductId] <Guid> [<CommonParameters>]
```

## Description

Returns the application's current file list with names, sizes, types, and hashes, in exactly the shape the completion payload accepts.

Get-PmpcCustomApplication returns a trimmed projection with no file list, so this exists to let a caller read a file set back in order to send it again.

## Parameters

### -ProductId

ID of the application. Accepted from the pipeline by property name, so results from Find-PmpcCustomApplication and Get-PmpcCustomApplication can be piped straight in.

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

### ApplicationFileDto

One object per file.

## Examples

### Example 1: List an application's files

```powershell
Get-PmpcApplicationFile -ProductId $productId
```

Returns each file with its size, type, and hashes.

### Example 2: Total an application's size

```powershell
Get-PmpcApplicationFile -ProductId $productId | Measure-Object -Property FileSize -Sum
```

Sums the file sizes to find how large the application is.

## Notes

Set-PmpcCustomApplication does this itself when it needs to, so callers editing an application do not need this cmdlet. It is here for callers driving the completion payload directly.

## Related links

* [Get-PmpcCustomApplication](get-pmpccustomapplication.md)
* [Set-PmpcCustomApplication](set-pmpccustomapplication.md)
* PowerShell module

## See also

* SDK method: [GetApplicationFilesAsync](../sdk/applications.md#getapplicationfilesasync)
* REST operation: [`GET /v1/api/apps/{productId}/files`](../rest-api/applications.md#get-application-files)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

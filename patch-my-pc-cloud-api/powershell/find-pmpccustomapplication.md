---
description: Searches the customer's custom applications catalog.
noIndex: true
noRobotsIndex: true
---

# Find-PmpcCustomApplication

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Searches the customer's custom applications catalog.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

### Criteria (Default)

```powershell
Find-PmpcCustomApplication [[-DisplayName] <String>] [-VendorId <Guid[]>]
  [-Language <String[]>] [-Architecture <RequirementArchitecture[]>]
  [-LastModifiedFrom <DateTimeOffset>] [-LastModifiedTo <DateTimeOffset>]
  [-LastUpdatedFrom <DateTimeOffset>] [-LastUpdatedTo <DateTimeOffset>] [-Skip <Int32>]
  [-Limit <Int32>] [-SortField <String>] [-Descending] [-IncludeIconData] [-AsResponse]
  [<CommonParameters>]
```

### Filter

```powershell
Find-PmpcCustomApplication [-Filter] <ProductFilterRequest> [-AsResponse]
  [<CommonParameters>]
```

## Description

Searches custom applications by name, vendor, language, architecture, and modification dates, returning one object per match.

By default the matching products are written to the pipeline one at a time, which is what makes filtering and piping work naturally. Use -AsResponse when you need the total match count for paging rather than the products themselves.

## Parameters

### -Architecture

Restrict results to these architectures.

| Attribute       | Value                                 |
| --------------- | ------------------------------------- |
| Type            | `RequirementArchitecture[]`           |
| Required        | False                                 |
| Position        | Named                                 |
| Pipeline input  | False                                 |
| Aliases         | Architectures                         |
| Accepted values | Unspecified, X64, X86, ARM, Universal |
| Parameter sets  | Criteria                              |

### -AsResponse

Emit the whole response object, including the total match count, instead of the individual products.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | None                                           |
| Parameter sets | All                                            |

### -Descending

Sort descending. Results are ascending by default.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | None                                           |
| Parameter sets | Criteria                                       |

### -DisplayName

Substring matched against application display names.

| Attribute      | Value                   |
| -------------- | ----------------------- |
| Type           | `System.String`         |
| Required       | False                   |
| Position       | 0                       |
| Pipeline input | False                   |
| Aliases        | DisplayNameSearchString |
| Parameter sets | Criteria                |

### -Filter

A pre-built ProductFilterRequest, for criteria this cmdlet does not surface as individual parameters. Mutually exclusive with those parameters.

| Attribute      | Value                  |
| -------------- | ---------------------- |
| Type           | `ProductFilterRequest` |
| Required       | True                   |
| Position       | 0                      |
| Pipeline input | True (ByValue)         |
| Aliases        | None                   |
| Parameter sets | Filter                 |

### -IncludeIconData

Include base64 icon data on each result. Increases response size considerably.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | None                                           |
| Parameter sets | Criteria                                       |

### -Language

Restrict results to these language codes, for example en-US.

| Attribute      | Value             |
| -------------- | ----------------- |
| Type           | `System.String[]` |
| Required       | False             |
| Position       | Named             |
| Pipeline input | False             |
| Aliases        | Languages         |
| Parameter sets | Criteria          |

### -LastModifiedFrom

Only applications last modified at or after this time.

| Attribute      | Value                   |
| -------------- | ----------------------- |
| Type           | `System.DateTimeOffset` |
| Required       | False                   |
| Position       | Named                   |
| Pipeline input | False                   |
| Aliases        | LastModifiedFromUtc     |
| Parameter sets | Criteria                |

### -LastModifiedTo

Only applications last modified at or before this time.

| Attribute      | Value                   |
| -------------- | ----------------------- |
| Type           | `System.DateTimeOffset` |
| Required       | False                   |
| Position       | Named                   |
| Pipeline input | False                   |
| Aliases        | LastModifiedToUtc       |
| Parameter sets | Criteria                |

### -LastUpdatedFrom

Only applications last updated at or after this time.

| Attribute      | Value                   |
| -------------- | ----------------------- |
| Type           | `System.DateTimeOffset` |
| Required       | False                   |
| Position       | Named                   |
| Pipeline input | False                   |
| Aliases        | LastUpdatedFromUtc      |
| Parameter sets | Criteria                |

### -LastUpdatedTo

Only applications last updated at or before this time.

| Attribute      | Value                   |
| -------------- | ----------------------- |
| Type           | `System.DateTimeOffset` |
| Required       | False                   |
| Position       | Named                   |
| Pipeline input | False                   |
| Aliases        | LastUpdatedToUtc        |
| Parameter sets | Criteria                |

### -Limit

Maximum number of matches to return.

| Attribute      | Value          |
| -------------- | -------------- |
| Type           | `System.Int32` |
| Required       | False          |
| Position       | Named          |
| Pipeline input | False          |
| Aliases        | None           |
| Parameter sets | Criteria       |

### -Skip

Number of matches to skip, for paging. Defaults to 0.

| Attribute      | Value          |
| -------------- | -------------- |
| Type           | `System.Int32` |
| Required       | False          |
| Position       | Named          |
| Pipeline input | False          |
| Aliases        | None           |
| Parameter sets | Criteria       |

### -SortField

Field to sort the results by.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Criteria        |

### -VendorId

Restrict results to these vendors.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.Guid[]` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | VendorIds       |
| Parameter sets | Criteria        |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### ProductFilterRequest

A pre-built filter, bound to -Filter.

## Outputs

### ProductSummaryDto

One object per matching application.

### ProductFilterResponse

The whole response including total counts, with -AsResponse.

## Examples

### Example 1: Search by name

```powershell
Find-PmpcCustomApplication -DisplayName '7-Zip'
```

Returns custom applications whose display name contains 7-Zip.

### Example 2: Page through results

```powershell
Find-PmpcCustomApplication -DisplayName 'Adobe' -Skip 50 -Limit 50
```

Returns the second page of 50 matches.

### Example 3: Get the total match count

```powershell
(Find-PmpcCustomApplication -DisplayName 'Adobe' -Limit 1 -AsResponse).TotalAmount
```

Asks for the count without pulling every match down.

### Example 4: Find recently changed applications

```powershell
Find-PmpcCustomApplication -LastModifiedFrom (Get-Date).AddDays(-7) -SortField 'LastUpdated' -Descending
```

Returns custom applications modified in the last week, newest first.

## Notes

-IncludeIconData embeds base64 icon data in every result and makes responses considerably larger; leave it off unless the icons are the point.

## Related links

* [Get-PmpcCustomApplication](get-pmpccustomapplication.md)
* [New-PmpcCustomApplication](new-pmpccustomapplication.md)
* PowerShell module

## See also

* SDK method: [SearchCustomApplicationsAsync](../sdk/custom-applications.md#searchcustomapplicationsasync)
* REST operation: [`POST /v1/api/apps/custom/search`](../rest-api/applications.md#search-custom-applications)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

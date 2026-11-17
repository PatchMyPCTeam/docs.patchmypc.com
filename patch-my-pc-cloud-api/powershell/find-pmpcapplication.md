---
description: Searches the Patch My PC public catalog.
noIndex: true
noRobotsIndex: true
---

# Find-PmpcApplication

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Searches the Patch My PC public catalog.

## Syntax

### Criteria (Default)

{% code collapsedlinecount="10" %}
```powershell
Find-PmpcApplication [[-DisplayName] <String>] [-VendorId <Guid[]>] [-Language <String[]>]
  [-Architecture <RequirementArchitecture[]>] [-ConnectionId <Guid>] [-OsType <OSType>]
  [-LastModifiedFrom <DateTimeOffset>] [-LastModifiedTo <DateTimeOffset>]
  [-LastUpdatedFrom <DateTimeOffset>] [-LastUpdatedTo <DateTimeOffset>] [-Skip <Int32>]
  [-Limit <Int32>] [-SortField <String>] [-Descending] [-IncludeIconData] [-AsResponse]
  [<CommonParameters>]
```
{% endcode %}

### Filter

{% code collapsedlinecount="10" %}
```powershell
Find-PmpcApplication [-Filter] <ProductFilterRequest> [-AsResponse] [<CommonParameters>]
```
{% endcode %}

## Description

Searches public catalog applications by name, vendor, language, architecture, and modification dates, returning one object per match. Each PMPC summary includes independent architecture, language, installer-type, and install-context options for the requested operating system. These are separate availability sets, not a promise that every combination is valid; use Get-PmpcApplication to inspect the exact selectable variants.

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

### -ConnectionId

Intune connection scoping the search. If omitted, the session's selected connection is used.

| Attribute      | Value         |
| -------------- | ------------- |
| Type           | `System.Guid` |
| Required       | False         |
| Position       | Named         |
| Pipeline input | False         |
| Aliases        | None          |
| Parameter sets | Criteria      |

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

Maximum number of matches to return. Defaults to 50.

| Attribute      | Value          |
| -------------- | -------------- |
| Type           | `System.Int32` |
| Required       | False          |
| Position       | Named          |
| Pipeline input | False          |
| Aliases        | None           |
| Parameter sets | Criteria       |

### -OsType

Restrict results to this operating system. Defaults to Windows when omitted, matching this cmdlet's existing behavior. MacOS additionally requires the customer to be entitled to the "macOS Applications" feature; when they are not, results are returned as empty rather than the command failing.

| Attribute       | Value          |
| --------------- | -------------- |
| Type            | `OSType`       |
| Required        | False          |
| Position        | Named          |
| Pipeline input  | False          |
| Aliases         | None           |
| Accepted values | Windows, MacOS |
| Parameter sets  | Criteria       |

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

### Example 1: Search public catalog by name

{% code collapsedlinecount="10" %}
```powershell
Find-PmpcApplication -DisplayName '7-Zip'
```
{% endcode %}

Returns public catalog applications whose display name contains 7-Zip, using the selected connection.

### Example 2: Search with an explicit connection

{% code collapsedlinecount="10" %}
```powershell
Find-PmpcApplication -DisplayName 'Notepad++' -ConnectionId $connectionId
```
{% endcode %}

Searches the Patch My PC public catalog scoped by the specified Intune connection.

### Example 3: Page through results

{% code collapsedlinecount="10" %}
```powershell
Find-PmpcApplication -DisplayName 'Adobe' -Skip 50 -Limit 50
```
{% endcode %}

Returns the second page of 50 matches.

### Example 4: Search macOS applications

{% code collapsedlinecount="10" %}
```powershell
Find-PmpcApplication -DisplayName 'Zoom' -OsType MacOS
```
{% endcode %}

Searches the public catalog for macOS applications. Requires the customer's "macOS Applications" entitlement; results are returned as empty when the customer is not entitled.

### Example 5: Get the total match count

{% code collapsedlinecount="10" %}
```powershell
(Find-PmpcApplication -DisplayName 'Adobe' -Limit 1 -AsResponse).TotalAmount
```
{% endcode %}

Asks for the count without pulling every match down.

## Notes

Searching the public catalog requires an Intune connection. If -ConnectionId is omitted, the session's selected connection is used.

Inspect Pmpc.Architectures, Pmpc.Languages, Pmpc.InstallerTypes, and Pmpc.InstallContexts for available options. Public search results omit updateId from JSON; the nullable UpdateId property reads as null and must be ignored. Older clients with a non-nullable property read Guid.Empty instead. Get-PmpcApplication returns exact variants with ProductId and CatalogEntryId for deployment selection; pipe one explicitly selected variant, not the search result or family block.

-IncludeIconData embeds base64 icon data in every result and makes responses considerably larger; leave it off unless the icons are the point.

## Related links

* [Get-PmpcApplication](get-pmpcapplication.md)
* [Get-PmpcConnection](get-pmpcconnection.md)
* [PowerShell module](./)

## See also

* SDK method: [SearchPublicApplicationsAsync](../sdk/applications.md#searchpublicapplicationsasync)
* REST operation: [`POST /v1/api/apps/public/search`](../rest-api/applications.md#search-public-applications)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

---
description: Gets the company the session is currently scoped to.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcSelectedCompany

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Gets the company the session is currently scoped to.

## Syntax

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcSelectedCompany [<CommonParameters>]
```
{% endcode %}

## Description

Returns the selected company, or nothing when none has been selected. Use it to confirm the customer context before running a command that changes something.

## Parameters

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input.

## Outputs

### CompanyInfo

The selected company, or nothing when none is selected.

## Examples

### Example 1: Show the selected company

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcSelectedCompany
```
{% endcode %}

Returns the current company, or nothing if none is selected.

## Notes

Writes an explanatory message to the verbose stream, rather than an error, when no company is selected.

## Related links

* [PowerShell module](./)

## See also

* SDK method: [GetSelectedCompany](../sdk/authentication.md#getselectedcompany)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

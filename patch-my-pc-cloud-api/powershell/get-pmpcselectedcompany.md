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

```powershell
Get-PmpcSelectedCompany [<CommonParameters>]
```

## Description

Returns the company the session is scoped to, or nothing when there is none. A session started with Connect-PmpcCloudWithPat is scoped to the customer its token belongs to. Use it to confirm the customer context before running a command that changes something.

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

```powershell
Get-PmpcSelectedCompany
```

Returns the current company, or nothing if none is selected.

## Notes

Writes an explanatory message to the verbose stream, rather than an error, when no company is selected.

## Related links

* [Connect-PmpcCloudWithPat](connect-pmpccloudwithpat.md)
* PowerShell module

## See also

* SDK method: [GetSelectedCompany](../sdk/authentication.md#getselectedcompany)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

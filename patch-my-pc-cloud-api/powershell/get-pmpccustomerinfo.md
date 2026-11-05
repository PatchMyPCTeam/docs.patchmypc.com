---
description: Gets account information and usage limits for the current customer.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcCustomerInfo

## Synopsis

Gets account information and usage limits for the current customer.

## Syntax

```powershell
Get-PmpcCustomerInfo [<CommonParameters>]
```

## Description

Returns the account details and usage limits for the customer the session is scoped to, such as the customer name and the quotas applied to it.

## Parameters

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input.

## Outputs

### CustomerInfoDto

Account information and usage limits.

## Examples

### Example 1: Show customer information

```powershell
Get-PmpcCustomerInfo
```

Returns the current customer account details and limits.

## Notes

Works under either authentication mode. Under a personal access token (PAT), the token must carry the appcatbroker:customer:read scope; without it the call is refused, which is the scope doing its job rather than a fault.

## Related links

* [Get-PmpcSelectedCompany](get-pmpcselectedcompany.md)
* [Connect-PmpcBrokerWithPat](connect-pmpcbrokerwithpat.md)
* PowerShell module

## See also

* SDK method: [GetCustomerInfoAsync](../sdk/customer-and-connections.md#getcustomerinfoasync)
* REST operation: [`GET /v1/api/customer-info`](../rest-api/applications.md#get-customer-info)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

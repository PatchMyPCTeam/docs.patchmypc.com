---
description: Lists the Intune connections available to the selected company.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcConnection

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Lists the Intune connections available to the selected company.

## Syntax

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcConnection [[-Name] <String>] [-ConnectionId <Guid>] [<CommonParameters>]
```
{% endcode %}

## Description

Returns the Intune connections configured for the selected company; Publisher and ConfigMgr connections are not returned. Deployment commands are scoped to one of these, chosen with Set-PmpcConnection, and public-catalog lookups use one to scope the request.

## Parameters

### -ConnectionId

ID of an Intune connection, as returned by Get-PmpcConnection.

| Attribute      | Value         |
| -------------- | ------------- |
| Type           | `System.Guid` |
| Required       | False         |
| Position       | Named         |
| Pipeline input | False         |
| Aliases        | None          |

### -Name

Return only connections whose display name matches. Wildcards are accepted.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | 0               |
| Pipeline input | False           |
| Aliases        | None            |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input.

## Outputs

### ConnectionDto

One object per available connection.

## Examples

### Example 1: List connections

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcConnection
```
{% endcode %}

Shows the display name, ID, type and admin-consent state of each connection.

### Example 2: Find Intune connections

{% code collapsedlinecount="10" %}
```powershell
Get-PmpcConnection | Where-Object Type -eq 'Intune'
```
{% endcode %}

The API currently returns only Intune connections, so this filter makes the intended type explicit.

## Notes

Requires a selected company. Check the AdminConsent property: a connection without admin consent will fail deployment operations.

## Related links

* [Set-PmpcConnection](set-pmpcconnection.md)
* [Get-PmpcSelectedConnection](get-pmpcselectedconnection.md)
* [PowerShell module](./)

## See also

* SDK method: [GetAvailableConnectionsAsync](../sdk/customer-and-connections.md#getavailableconnectionsasync)
* REST operation: [`GET /v1/api/connections`](../rest-api/applications.md#get-available-connections)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

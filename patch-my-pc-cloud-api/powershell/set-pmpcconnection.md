---
description: Selects the Intune connection that deployment commands act on.
noIndex: true
noRobotsIndex: true
---

# Set-PmpcConnection

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Selects the Intune connection that deployment commands act on.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

### Name (Default)

```powershell
Set-PmpcConnection [-Name] <String> [-PassThru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### ConnectionId

```powershell
Set-PmpcConnection -ConnectionId <Guid> [-PassThru] [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

### InputObject

```powershell
Set-PmpcConnection [-InputObject] <ConnectionDto> [-PassThru] [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Sets the connection context for the session. Every deployment command afterwards is scoped to it, and the SDK applies it automatically to creation and edit requests.

The connection can be given by object, by display name, or by ID. Name and ID are resolved against the live list first.

## Parameters

### -Confirm

Prompts you for confirmation before running the cmdlet.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | cf                                             |

### -ConnectionId

ID of an Intune connection, as returned by Get-PmpcConnection.

| Attribute      | Value         |
| -------------- | ------------- |
| Type           | `System.Guid` |
| Required       | True          |
| Position       | Named         |
| Pipeline input | False         |
| Aliases        | None          |
| Parameter sets | ConnectionId  |

### -InputObject

The connection to select, as returned by Get-PmpcConnection.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `ConnectionDto` |
| Required       | True            |
| Position       | 0               |
| Pipeline input | True (ByValue)  |
| Aliases        | None            |
| Parameter sets | InputObject     |

### -Name

Display name of the connection to select. Wildcards are accepted; an exact match wins over a wildcard match.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | True            |
| Position       | 0               |
| Pipeline input | False           |
| Aliases        | None            |
| Parameter sets | Name            |

### -PassThru

Return the object the cmdlet acted on. Without it the cmdlet writes nothing to the pipeline.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | None                                           |
| Parameter sets | All                                            |

### -WhatIf

Shows what would happen if the cmdlet runs. The cmdlet is not run.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | wi                                             |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### ConnectionDto

A connection object, as returned by Get-PmpcConnection.

## Outputs

### ConnectionDto

Returned only with -PassThru.

## Examples

### Example 1: Select a connection by name

```powershell
Set-PmpcConnection -Name 'Contoso Intune'
```

Resolves the name against the available connections and selects the match.

### Example 2: Select a connection from the pipeline

```powershell
Get-PmpcConnection | Where-Object Type -eq 'Intune' | Set-PmpcConnection -PassThru
```

Selects the connection object directly and emits what was selected.

## Notes

Selecting a connection does not change the selected company, but the connection list comes from the selected company, so a company must be selected first.

## Related links

* [Get-PmpcConnection](get-pmpcconnection.md)
* [Get-PmpcSelectedConnection](get-pmpcselectedconnection.md)
* PowerShell module

## See also

* SDK method: [SetSelectedConnectionAsync](../sdk/customer-and-connections.md#setselectedconnectionasync)
* SDK method: [GetAvailableConnectionsAsync](../sdk/customer-and-connections.md#getavailableconnectionsasync)
* REST operation: [`GET /v1/api/connections`](../rest-api/applications.md#get-available-connections)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

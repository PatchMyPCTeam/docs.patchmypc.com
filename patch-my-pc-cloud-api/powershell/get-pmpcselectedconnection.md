---
description: Gets the Intune connection the session is currently scoped to.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcSelectedConnection

## Synopsis

Gets the Intune connection the session is currently scoped to.

## Syntax

```powershell
Get-PmpcSelectedConnection [<CommonParameters>]
```

## Description

Returns the connection selected by Set-PmpcConnection, or nothing when none has been selected. Deployment commands fail without one, so this is worth checking before a bulk operation.

## Parameters

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input.

## Outputs

### ConnectionDto

The selected connection, or nothing when none is selected.

## Examples

### Example 1: Show the selected connection

```powershell
Get-PmpcSelectedConnection
```

Returns the current connection, or nothing if none is selected.

## Notes

Writes an explanatory message to the verbose stream, rather than an error, when no connection is selected.

## Related links

* [Set-PmpcConnection](set-pmpcconnection.md)
* [Get-PmpcConnection](get-pmpcconnection.md)
* PowerShell module

## See also

* SDK method: [GetSelectedConnection](../sdk/customer-and-connections.md#getselectedconnection)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

---
description: Reports the module's current session state.
noIndex: true
noRobotsIndex: true
---

# Get-PmpcBrokerSession

## Synopsis

Reports the module's current session state.

## Syntax

```powershell
Get-PmpcBrokerSession [<CommonParameters>]
```

## Description

Describes whether the module is connected, when it connected, and which company and Intune connection it is scoped to. Useful for confirming what a script is about to act on before it does something destructive.

Safe to call when not connected: it returns an object whose IsConnected is false rather than failing.

## Parameters

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input.

## Outputs

### AppCatBrokerSessionInfo

The session snapshot.

## Examples

### Example 1: Show the current session

```powershell
Get-PmpcBrokerSession
```

Displays connection state along with the selected company and connection.

### Example 2: Guard a script on being connected

```powershell
if (-not (Get-PmpcBrokerSession).IsConnected) { throw 'Run Connect-PmpcBrokerWithPat first.' }
```

Fails fast with a clear message instead of letting the first real command produce a connection error.

## Notes

Credentials are never exposed in the session summary, because a session summary is exactly the kind of object that ends up in a transcript.

## Related links

* [Connect-PmpcBrokerWithPat](connect-pmpcbrokerwithpat.md)
* [Disconnect-PmpcBroker](disconnect-pmpcbroker.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

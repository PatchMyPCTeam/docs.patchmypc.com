---
description: Checks whether the Cloud Customer API responds to a heartbeat request.
noIndex: true
noRobotsIndex: true
---

# Test-PmpcCloudHealth

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Checks whether the Cloud Customer API responds to a heartbeat request.

## Syntax

```powershell
Test-PmpcCloudHealth [<CommonParameters>]
```

## Description

Returns a boolean indicating whether the session received a heartbeat response from the Cloud Customer API. This is a reachability check, not a check of every service dependency.

## Parameters

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input.

## Outputs

### System.Boolean

True when a heartbeat response is received; otherwise False.

## Examples

### Example 1: Check service health

```powershell
Test-PmpcCloudHealth
```

Returns True when a heartbeat response is received.

### Example 2: Gate a script on service health

```powershell
if (-not (Test-PmpcCloudHealth)) { Write-Warning 'Patch My PC Cloud is unhealthy; skipping publish.'; return }
```

Skips the upload when the health check cannot obtain a heartbeat response. The warning alone does not identify the cause.

## Notes

Connect before running this cmdlet; without an active module session it reports a not-connected error. With a session, a failed health check returns $false, including network or token-acquisition failures and a missing selected company. A false result does not distinguish these causes.

## Related links

* PowerShell module

## See also

* SDK method: [IsServiceHealthyAsync](../sdk/authentication.md#isservicehealthyasync)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

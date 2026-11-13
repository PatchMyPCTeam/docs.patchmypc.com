---
description: Checks whether the Patch My PC Cloud service is reachable and healthy.
noIndex: true
noRobotsIndex: true
---

# Test-PmpcCloudHealth

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Checks whether the Patch My PC Cloud service is reachable and healthy.

## Syntax

```powershell
Test-PmpcCloudHealth [<CommonParameters>]
```

## Description

Calls the broker's health endpoint and returns a boolean. Use it to separate 'the service is down' from 'my request was wrong' when something else fails.

## Parameters

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input.

## Outputs

### System.Boolean

True when the service is healthy.

## Examples

### Example 1: Check service health

```powershell
Test-PmpcCloudHealth
```

Returns True when the broker is healthy.

### Example 2: Gate a script on service health

```powershell
if (-not (Test-PmpcCloudHealth)) { Write-Warning 'Patch My PC Cloud is unhealthy; skipping publish.'; return }
```

Avoids starting a long upload against a service that has already said it is unhealthy.

## Notes

Returns $false rather than throwing when the service reports itself unhealthy. A transport failure is reported as an error, because being unable to ask is different from getting an answer of no.

## Related links

* PowerShell module

## See also

* SDK method: [IsServiceHealthyAsync](../sdk/authentication.md#isservicehealthyasync)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

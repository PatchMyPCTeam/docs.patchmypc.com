---
description: Builds one installer exit code and the outcome it maps to.
noIndex: true
noRobotsIndex: true
---

# New-PmpcDeploymentReturnCode

## Synopsis

Builds one installer exit code and the outcome it maps to.

## Syntax

```powershell
New-PmpcDeploymentReturnCode [-Code] <Int32> [-Type] <ReturnCodeType> [<CommonParameters>]
```

## Description

Creates a single return code for a deployment configuration.

Both values are required: an exit code without an outcome tells the service nothing. Collect the results and pass them to New-PmpcDeploymentConfiguration, remembering that the set replaces the deployment's codes outright.

## Parameters

### -Code

The exit code the installer returns.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Int32`        |
| Required       | True                  |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -Type

How that exit code is interpreted.

| Attribute       | Value                                          |
| --------------- | ---------------------------------------------- |
| Type            | `ReturnCodeType`                               |
| Required        | True                                           |
| Position        | 1                                              |
| Pipeline input  | True (ByPropertyName)                          |
| Aliases         | None                                           |
| Accepted values | Success, Retry, HardReboot, SoftReboot, Failed |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### DeploymentReturnCodeDto

A single deployment return code.

## Examples

### Example 1: Map a soft reboot

```powershell
New-PmpcDeploymentReturnCode -Code 3010 -Type SoftReboot
```

Treats exit code 3010 as a success that requires a reboot.

### Example 2: Build a full set

```powershell
@(
    New-PmpcDeploymentReturnCode -Code 0 -Type Success
    New-PmpcDeploymentReturnCode -Code 1618 -Type Retry
) | ForEach-Object { $_ }
```

Collects several codes for one configuration.

## Notes

This cmdlet makes no network call and does not require a session.

## Related links

* [New-PmpcDeploymentConfiguration](new-pmpcdeploymentconfiguration.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

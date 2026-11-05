---
description: Builds an application's installation requirements.
noIndex: true
noRobotsIndex: true
---

# New-PmpcRequirement

## Synopsis

Builds an application's installation requirements.

## Syntax

```powershell
New-PmpcRequirement [[-Architecture] <ApplicableArchitecture[]>]
  [-MinimumWindowsOSVersion <WindowsOSVersion>] [-MinimumNumberOfProcessors <Int32>]
  [-MinimumMemoryInMB <Int32>] [-MinimumCpuSpeedInMHz <Int32>] [-FileRule <FileRuleDto[]>]
  [-RegistryRule <RegistryRuleDto[]>] [-ScriptRule <ScriptRuleDto[]>] [<CommonParameters>]
```

## Description

Creates the requirements an application must satisfy before it installs, as accepted by New-PmpcCustomApplication and Update-PmpcCustomApplication.

Deployment requirements use different property names and handle unset values differently, so they have their own builder: New-PmpcDeploymentRequirement.

## Parameters

### -Architecture

Architectures the application may install on.

| Attribute       | Value                        |
| --------------- | ---------------------------- |
| Type            | `ApplicableArchitecture[]`   |
| Required        | False                        |
| Position        | 0                            |
| Pipeline input  | True (ByPropertyName)        |
| Aliases         | ApplicableArchitectures      |
| Accepted values | None, X86, X64, Arm, Neutral |

### -FileRule

File and folder rules that must pass.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `FileRuleDto[]`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | RequirementFileRules  |

### -MinimumCpuSpeedInMHz

Slowest CPU the application supports, in megahertz.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Int32`        |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -MinimumMemoryInMB

Least physical memory required, in megabytes.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Int32`        |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -MinimumNumberOfProcessors

Fewest logical processors required.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.Int32`        |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -MinimumWindowsOSVersion

Oldest Windows version the application supports.

| Attribute       | Value                                                                                                                                                                                                                                                                                                      |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Type            | `WindowsOSVersion`                                                                                                                                                                                                                                                                                         |
| Required        | False                                                                                                                                                                                                                                                                                                      |
| Position        | Named                                                                                                                                                                                                                                                                                                      |
| Pipeline input  | True (ByPropertyName)                                                                                                                                                                                                                                                                                      |
| Aliases         | None                                                                                                                                                                                                                                                                                                       |
| Accepted values | None, V8\_0, V8\_1, V10\_0, Windows10\_1607, Windows10\_1703, Windows10\_1709, Windows10\_1803, Windows10\_1809, Windows10\_1903, Windows10\_1909, Windows10\_2004, Windows10\_20H2, Windows10\_21H1, Windows10\_21H2, Windows10\_22H2, Windows11\_21H2, Windows11\_22H2, Windows11\_23H2, Windows11\_24H2 |

### -RegistryRule

Registry rules that must pass.

| Attribute      | Value                    |
| -------------- | ------------------------ |
| Type           | `RegistryRuleDto[]`      |
| Required       | False                    |
| Position       | Named                    |
| Pipeline input | True (ByPropertyName)    |
| Aliases        | RequirementRegistryRules |

### -ScriptRule

Script rules that must pass.

| Attribute      | Value                   |
| -------------- | ----------------------- |
| Type           | `ScriptRuleDto[]`       |
| Required       | False                   |
| Position       | Named                   |
| Pipeline input | True (ByPropertyName)   |
| Aliases        | RequirementsScriptRules |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### CustomRequirementsDto

The requirement set.

## Examples

### Example 1: Require 64-bit Windows 11 and 8 GB of memory

```powershell
New-PmpcRequirement -Architecture X64 -MinimumWindowsOSVersion Windows11_22H2 -MinimumMemoryInMB 8192
```

The application installs only where all three hold.

### Example 2: Require a prerequisite to be present

```powershell
$prereq = New-PmpcFileRule -Path 'C:\Program Files\Contoso' -FileOrFolderName 'runtime.dll' -OperationType Exists
New-PmpcRequirement -Architecture X64 -FileRule $prereq
```

Adds a file rule that must pass before the application installs.

## Notes

This cmdlet makes no network call and does not require a session.

## Related links

* [New-PmpcDeploymentRequirement](new-pmpcdeploymentrequirement.md)
* [New-PmpcFileRule](new-pmpcfilerule.md)
* [New-PmpcCustomApplication](new-pmpccustomapplication.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

---
description: Builds a deployment's installation requirements.
noIndex: true
noRobotsIndex: true
---

# New-PmpcDeploymentRequirement

## Synopsis

Builds a deployment's installation requirements.

## Syntax

```powershell
New-PmpcDeploymentRequirement [[-DisableArchitecture] <ApplicableArchitecture[]>]
  [-MinimumWindowsOSVersion <WindowsOSVersion>] [-MinimumNumberOfProcessors <Int32>]
  [-MinimumMemoryInMB <Int32>] [-MinimumCpuSpeedInMHz <Int32>] [-FileRule <FileRuleDto[]>]
  [-RegistryRule <RegistryRuleDto[]>] [-ScriptRule <ScriptRuleDto[]>] [<CommonParameters>]
```

## Description

Creates the requirements a deployment must satisfy before it installs, as accepted by Set-PmpcDeployment.

Separate from New-PmpcRequirement because deployment requirements have a different shape from application requirements. Its lists are nullable, so a list you do not mention is left as it is rather than emptied, and its architecture parameter is inverted: it names the architectures to disable.

## Parameters

### -DisableArchitecture

Architectures the deployment must not install on.

| Attribute       | Value                        |
| --------------- | ---------------------------- |
| Type            | `ApplicableArchitecture[]`   |
| Required        | False                        |
| Position        | 0                            |
| Pipeline input  | True (ByPropertyName)        |
| Aliases         | DisableArchitectures         |
| Accepted values | None, X86, X64, Arm, Neutral |

### -FileRule

File and folder rules that must pass.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `FileRuleDto[]`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | FileRules             |

### -MinimumCpuSpeedInMHz

Slowest CPU the deployment supports, in megahertz.

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

Oldest Windows version the deployment supports.

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

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `RegistryRuleDto[]`   |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | RegistryRules         |

### -ScriptRule

Script rules that must pass.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `ScriptRuleDto[]`     |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | ScriptRules           |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### EditDeploymentCustomRequirementsRequest

The deployment requirement set.

## Examples

### Example 1: Block 32-bit installs

```powershell
$config = New-PmpcDeploymentConfiguration -CustomRequirements (New-PmpcDeploymentRequirement -DisableArchitecture X86)
Set-PmpcDeployment -ProductId $productId -DeploymentId $deploymentId -Configuration $config
```

Stops the deployment installing on x86, leaving every other requirement untouched.

### Example 2: Raise the memory floor

```powershell
New-PmpcDeploymentRequirement -MinimumMemoryInMB 16384
```

Sets only the memory requirement; unmentioned rules are left alone.

## Notes

This cmdlet makes no network call and does not require a session.

## Related links

* [New-PmpcRequirement](new-pmpcrequirement.md)
* [Set-PmpcDeployment](set-pmpcdeployment.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

---
description: Builds a detection rule set.
noIndex: true
noRobotsIndex: true
---

# New-PmpcDetectionRule

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Builds a detection rule set.

## Syntax

```powershell
New-PmpcDetectionRule [-RulesType] <DetectionRuleType> [-FileRule <FileRuleDto[]>]
  [-RegistryRule <RegistryRuleDto[]>] [-ScriptRule <ScriptRuleDto>]
  [-ProductCode <String>] [-ProductVersion <String>] [-ProductCodeOperator <RuleOperator>]
  [<CommonParameters>]
```

## Description

Creates the detection rule set that says whether an application is already installed, as accepted by New-PmpcCustomApplication and Update-PmpcCustomApplication.

Rules come from New-PmpcFileRule, New-PmpcRegistryRule, and New-PmpcScriptRule. A product-code rule is built here rather than by a separate cmdlet because an application has only one MSI product code, so there is nothing to compose.

## Parameters

### -FileRule

File and folder rules.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `FileRuleDto[]`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | FileSystemRules       |

### -ProductCode

MSI product code identifying the installed application.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -ProductCodeOperator

How the installed product version is compared with -ProductVersion.

| Attribute       | Value                                                                                      |
| --------------- | ------------------------------------------------------------------------------------------ |
| Type            | `RuleOperator`                                                                             |
| Required        | False                                                                                      |
| Position        | Named                                                                                      |
| Pipeline input  | True (ByPropertyName)                                                                      |
| Aliases         | None                                                                                       |
| Accepted values | NotConfigured, Equal, NotEqual, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual |

### -ProductVersion

Product version compared against the installed one. Requires -ProductCode.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -RegistryRule

Registry rules.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `RegistryRuleDto[]`   |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | RegistryRules         |

### -RulesType

Which detection strategy the application uses: PMPC (detect by MSI product code, with -ProductCode), Manual (your own file and registry rules), or Script (a detection script).

| Attribute       | Value                      |
| --------------- | -------------------------- |
| Type            | `DetectionRuleType`        |
| Required        | True                       |
| Position        | 0                          |
| Pipeline input  | True (ByPropertyName)      |
| Aliases         | None                       |
| Accepted values | None, PMPC, Script, Manual |

### -ScriptRule

Script rule. Only one is carried, so this is not a collection.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `ScriptRuleDto`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### DetectionRulesDto

The detection rule set.

## Examples

### Example 1: Detect by MSI product code

```powershell
New-PmpcDetectionRule -RulesType PMPC -ProductCode '{12345678-1234-1234-1234-123456789012}'
```

Detects the application by the product code its MSI registers.

### Example 2: Detect by file and registry

```powershell
$file = New-PmpcFileRule -Path 'C:\Program Files\Contoso' -FileOrFolderName 'app.exe' -OperationType Exists
$reg  = New-PmpcRegistryRule -KeyPath 'HKLM:\SOFTWARE\Contoso\App' -OperationType Exists
New-PmpcDetectionRule -RulesType Manual -FileRule $file -RegistryRule $reg
```

Combines rules built by the rule cmdlets into one set.

## Notes

This cmdlet makes no network call and does not require a session.

## Related links

* [New-PmpcFileRule](new-pmpcfilerule.md)
* [New-PmpcRegistryRule](new-pmpcregistryrule.md)
* [New-PmpcScriptRule](new-pmpcscriptrule.md)
* [New-PmpcCustomApplication](new-pmpccustomapplication.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

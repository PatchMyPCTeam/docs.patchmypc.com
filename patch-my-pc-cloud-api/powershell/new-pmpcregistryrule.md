---
description: Builds a registry rule.
noIndex: true
noRobotsIndex: true
---

# New-PmpcRegistryRule

## Synopsis

Builds a registry rule.

## Syntax

```powershell
New-PmpcRegistryRule [-KeyPath] <String> [-OperationType] <RegistryRuleOperationType>
  [[-ValueName] <String>] [-Operator <RuleOperator>] [-ComparisonValue <String>]
  [-Check32BitOn64System] [<CommonParameters>]
```

## Description

Creates a registry rule for use in a detection rule set or a requirement set.

It exists so rules can be built at the prompt without constructing a generated-client type by hand, with tab completion on the operation and operator.

## Parameters

### -Check32BitOn64System

Look in the 32-bit registry view on a 64-bit system.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | True (ByPropertyName)                          |
| Aliases        | None                                           |

### -ComparisonValue

Value the detected one is compared against.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -KeyPath

Registry key the rule inspects.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -OperationType

What about the key or value is being checked.

| Attribute       | Value                                                                                         |
| --------------- | --------------------------------------------------------------------------------------------- |
| Type            | `RegistryRuleOperationType`                                                                   |
| Required        | True                                                                                          |
| Position        | 1                                                                                             |
| Pipeline input  | True (ByPropertyName)                                                                         |
| Aliases         | None                                                                                          |
| Accepted values | NotConfigured, Exists, DoesNotExist, String, Integer, Version, AppVersion, UnknownFutureValue |

### -Operator

How the detected value is compared with -ComparisonValue.

| Attribute       | Value                                                                                      |
| --------------- | ------------------------------------------------------------------------------------------ |
| Type            | `RuleOperator`                                                                             |
| Required        | False                                                                                      |
| Position        | Named                                                                                      |
| Pipeline input  | True (ByPropertyName)                                                                      |
| Aliases         | None                                                                                       |
| Accepted values | NotConfigured, Equal, NotEqual, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual |

### -ValueName

Value under the key to inspect. Omit to inspect the key itself.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | 2                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### RegistryRuleDto

The registry rule.

## Examples

### Example 1: Detect an uninstall key

```powershell
New-PmpcRegistryRule -KeyPath 'HKLM:\SOFTWARE\Contoso\App' -OperationType Exists
```

Passes when the key is present.

### Example 2: Compare a version value

```powershell
New-PmpcRegistryRule -KeyPath 'HKLM:\SOFTWARE\Contoso\App' -ValueName 'Version' -OperationType Version -Operator GreaterThanOrEqual -ComparisonValue '2.1.0'
```

Passes when the recorded version is 2.1.0 or newer.

## Notes

This cmdlet makes no network call and does not require a session.

## Related links

* [New-PmpcDetectionRule](new-pmpcdetectionrule.md)
* [New-PmpcRequirement](new-pmpcrequirement.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

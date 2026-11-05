---
description: Builds a script rule.
noIndex: true
noRobotsIndex: true
---

# New-PmpcScriptRule

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Builds a script rule.

## Syntax

```powershell
New-PmpcScriptRule [-DisplayName] <String> [-ScriptContent] <String>
  [-OperationType] <ScriptRuleOperationType> [-Operator <RuleOperator>]
  [-ComparisonValue <String>] [-RunAsUser] [-EnforceSignatureCheck] [-RunAs32Bit]
  [<CommonParameters>]
```

## Description

Creates a script rule for use in a detection rule set or a requirement set.

Supply the script contents rather than a path: the rule travels to Intune, which has no access to a file on the machine that built it.

## Parameters

### -ComparisonValue

Value the script's output is compared against.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | False                 |
| Position       | Named                 |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -DisplayName

Name shown for the rule.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -EnforceSignatureCheck

Require the script to be signed by a trusted publisher.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | True (ByPropertyName)                          |
| Aliases        | None                                           |

### -OperationType

Type the script's output is interpreted as.

| Attribute       | Value                                                             |
| --------------- | ----------------------------------------------------------------- |
| Type            | `ScriptRuleOperationType`                                         |
| Required        | True                                                              |
| Position        | 2                                                                 |
| Pipeline input  | True (ByPropertyName)                                             |
| Aliases         | None                                                              |
| Accepted values | NotConfigured, String, DateTime, Integer, Float, Version, Boolean |

### -Operator

How the script's output is compared with -ComparisonValue.

| Attribute       | Value                                                                                      |
| --------------- | ------------------------------------------------------------------------------------------ |
| Type            | `RuleOperator`                                                                             |
| Required        | False                                                                                      |
| Position        | Named                                                                                      |
| Pipeline input  | True (ByPropertyName)                                                                      |
| Aliases         | None                                                                                       |
| Accepted values | NotConfigured, Equal, NotEqual, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual |

### -RunAs32Bit

Run the script in a 32-bit host on a 64-bit system.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | True (ByPropertyName)                          |
| Aliases        | None                                           |

### -RunAsUser

Run the script as the signed-in user instead of the system account.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | True (ByPropertyName)                          |
| Aliases        | None                                           |

### -ScriptContent

The script itself, as text rather than a path.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | 1                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### ScriptRuleDto

The script rule.

## Examples

### Example 1: Detect with a script

```powershell
$script = Get-Content .\detect.ps1 -Raw
New-PmpcScriptRule -DisplayName 'Contoso detection' -ScriptContent $script -OperationType Boolean -Operator Equal -ComparisonValue 'true'
```

Reads the script from disk and sends its contents, not its path.

## Notes

This cmdlet makes no network call and does not require a session.

## Related links

* [New-PmpcDetectionRule](new-pmpcdetectionrule.md)
* [New-PmpcRequirement](new-pmpcrequirement.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

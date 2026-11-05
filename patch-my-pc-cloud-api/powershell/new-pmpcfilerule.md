---
description: Builds a file or folder rule.
noIndex: true
noRobotsIndex: true
---

# New-PmpcFileRule

## Synopsis

Builds a file or folder rule.

## Syntax

```powershell
New-PmpcFileRule [-Path] <String> [-FileOrFolderName] <String>
  [-OperationType] <FileRuleOperationType> [-Operator <RuleOperator>]
  [-ComparisonValue <String>] [-Check32BitOn64System] [<CommonParameters>]
```

## Description

Creates a file rule for use in a detection rule set or a requirement set.

It exists so rules can be built at the prompt without constructing a generated-client type by hand, with tab completion on the operation and operator.

## Parameters

### -Check32BitOn64System

Look in the 32-bit locations on a 64-bit system.

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

### -FileOrFolderName

Name of the file or folder to look for.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | 1                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### -OperationType

What about the file or folder is being checked.

| Attribute       | Value                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Type            | `FileRuleOperationType`                                                                                                        |
| Required        | True                                                                                                                           |
| Position        | 2                                                                                                                              |
| Pipeline input  | True (ByPropertyName)                                                                                                          |
| Aliases         | None                                                                                                                           |
| Accepted values | NotConfigured, Exists, ModifiedDate, CreatedDate, Version, SizeInMB, DoesNotExist, SizeInBytes, AppVersion, UnknownFutureValue |

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

### -Path

Folder the file or folder is looked for in.

| Attribute      | Value                 |
| -------------- | --------------------- |
| Type           | `System.String`       |
| Required       | True                  |
| Position       | 0                     |
| Pipeline input | True (ByPropertyName) |
| Aliases        | None                  |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### None

This cmdlet does not accept pipeline input by value.

## Outputs

### FileRuleDto

The file rule.

## Examples

### Example 1: Detect an installed executable

```powershell
New-PmpcFileRule -Path 'C:\Program Files\Contoso' -FileOrFolderName 'app.exe' -OperationType Exists
```

Passes when the file is present.

### Example 2: Require a minimum file version

```powershell
New-PmpcFileRule -Path 'C:\Program Files\Contoso' -FileOrFolderName 'app.exe' -OperationType Version -Operator GreaterThanOrEqual -ComparisonValue '2.1.0'
```

Passes when the installed file is version 2.1.0 or newer.

## Notes

This cmdlet makes no network call and does not require a session.

## Related links

* [New-PmpcDetectionRule](new-pmpcdetectionrule.md)
* [New-PmpcRequirement](new-pmpcrequirement.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

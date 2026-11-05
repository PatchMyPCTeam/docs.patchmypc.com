---
description: Deletes a custom application.
noIndex: true
noRobotsIndex: true
---

# Remove-PmpcCustomApplication

## Synopsis

Deletes a custom application.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Syntax

```powershell
Remove-PmpcCustomApplication [-ProductId] <Guid> [-WhatIf] [-Confirm] [<CommonParameters>]
```

## Description

Deletes a custom application owned by the selected company, freeing a slot against the customer's custom-application limit.

Only the customer's own custom applications can be deleted. Public catalog products are shared across customers and are not deletable.

## Parameters

### -Confirm

Prompts you for confirmation before running the cmdlet.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | cf                                             |

### -ProductId

ID of the application. Accepted from the pipeline by property name, so results from Find-PmpcCustomApplication and Get-PmpcCustomApplication can be piped straight in.

| Attribute      | Value                          |
| -------------- | ------------------------------ |
| Type           | `System.Guid`                  |
| Required       | True                           |
| Position       | 0                              |
| Pipeline input | True (ByValue, ByPropertyName) |
| Aliases        | Id                             |

### -WhatIf

Shows what would happen if the cmdlet runs. The cmdlet is not run.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | wi                                             |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### System.Guid

The product ID, by value or by the Id/ProductId property.

## Outputs

### None

This cmdlet returns no output.

## Examples

### Example 1: Delete an application

```powershell
Remove-PmpcCustomApplication -ProductId $productId
```

Prompts for confirmation, then deletes the application.

### Example 2: Delete without prompting

```powershell
Remove-PmpcCustomApplication -ProductId $productId -Confirm:$false
```

Suppresses the confirmation prompt, for use in automation.

## Notes

The delete is rejected while the application's latest update is in a state that is not safe to remove.

Confirmation impact is High, so this prompts by default. Pass -Confirm:$false to suppress it in automation.

## Related links

* [New-PmpcCustomApplication](new-pmpccustomapplication.md)
* [Get-PmpcCustomApplication](get-pmpccustomapplication.md)
* PowerShell module

## See also

* SDK method: [DeleteCustomApplicationAsync](../sdk/custom-applications.md#deletecustomapplicationasync)
* REST operation: [`DELETE /v1/api/apps/custom/{productId}`](../rest-api/applications.md#delete-a-custom-application)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

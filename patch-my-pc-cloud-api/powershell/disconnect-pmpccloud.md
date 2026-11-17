---
description: Signs out and tears down the module's session.
noIndex: true
noRobotsIndex: true
---

# Disconnect-PmpcCloud

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Signs out and tears down the module's session.

## Syntax

{% code collapsedlinecount="10" %}
```powershell
Disconnect-PmpcCloud [-WhatIf] [-Confirm] [<CommonParameters>]
```
{% endcode %}

## Description

Clears the SDK's cached authentication and selected company, then disposes the session. Any persisted token cache is erased as well, so signing out really does sign out.

Doing nothing when no session is active is not an error; the cmdlet reports it on the verbose stream and returns.

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

### None

This cmdlet does not accept pipeline input.

## Outputs

### None

This cmdlet returns no output.

## Examples

### Example 1: Sign out

{% code collapsedlinecount="10" %}
```powershell
Disconnect-PmpcCloud
```
{% endcode %}

Clears authentication and disposes the session. A later command reports that you are not connected.

## Notes

The sign-out runs before the session is disposed, because clearing credentials goes through the very services the session owns.

## Related links

* [Get-PmpcCloudSession](get-pmpccloudsession.md)
* [PowerShell module](./)

## See also

* SDK method: [ClearAuthenticationAsync](../sdk/authentication.md#clearauthenticationasync)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

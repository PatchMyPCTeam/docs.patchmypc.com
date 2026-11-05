---
description: Signs out and tears down the module's session.
noIndex: true
noRobotsIndex: true
---

# Disconnect-PmpcBroker

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Signs out and tears down the module's session.

## Syntax

```powershell
Disconnect-PmpcBroker [-WhatIf] [-Confirm] [<CommonParameters>]
```

## Description

Clears the current session and the selected company. Run Connect-PmpcBrokerWithPat to connect again.

If no session is active, the cmdlet does nothing and reports that on the verbose stream.

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

```powershell
Disconnect-PmpcBroker
```

Ends the session. A later command reports that you are not connected.

## Notes

Disconnecting doesn't revoke your personal access token. To revoke a token, use the Access Tokens page of the Patch My PC portal.

## Related links

* [Connect-PmpcBrokerWithPat](connect-pmpcbrokerwithpat.md)
* [Get-PmpcBrokerSession](get-pmpcbrokersession.md)
* PowerShell module

## See also

* SDK method: [ClearAuthenticationAsync](../sdk/authentication.md#clearauthenticationasync)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

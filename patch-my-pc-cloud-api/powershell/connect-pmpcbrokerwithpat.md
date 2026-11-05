---
description: Connects to the Cloud Customer API with a personal access token.
noIndex: true
noRobotsIndex: true
---

# Connect-PmpcBrokerWithPat

## Synopsis

Connects to the Cloud Customer API with a personal access token.

## Syntax

```powershell
Connect-PmpcBrokerWithPat [-Token] <SecureString> [-PassThru]
  [-Region <AppCatBrokerRegion>] [-ConfigurationFile <String>]
  [-MaxSingleFileUploadSize <Int64>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## Description

Exchanges a personal access token (PAT) for an access token that's valid for 60 minutes, and scopes the session to the customer that token belongs to. The session exchanges the PAT again when the access token expires. Because it needs no prompt, it works from scripts, scheduled tasks, and build agents. No company selection is needed afterwards, because the token identifies its own customer.

Provide the customer's region with -Region so the token exchange reaches the correct regional service.

## Parameters

### -ConfigurationFile

Path to a JSON configuration file supplying SDK settings, for callers that keep endpoints and keys in a file rather than passing them as arguments.

| Attribute      | Value           |
| -------------- | --------------- |
| Type           | `System.String` |
| Required       | False           |
| Position       | Named           |
| Pipeline input | False           |
| Aliases        | None            |

### -Confirm

Prompts you for confirmation before running the cmdlet.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | cf                                             |

### -MaxSingleFileUploadSize

Largest file uploaded in a single request before the SDK switches to a chunked upload.

| Attribute      | Value          |
| -------------- | -------------- |
| Type           | `System.Int64` |
| Required       | False          |
| Position       | Named          |
| Pipeline input | False          |
| Aliases        | None           |

### -PassThru

Emit the resolved company, which is otherwise not written to the pipeline.

| Attribute      | Value                                          |
| -------------- | ---------------------------------------------- |
| Type           | `System.Management.Automation.SwitchParameter` |
| Required       | False                                          |
| Position       | Named                                          |
| Pipeline input | False                                          |
| Aliases        | None                                           |

### -Region

Production region that owns the customer this token belongs to. Accepted values are Eu, Us, and Uk. Required.

| Attribute       | Value                |
| --------------- | -------------------- |
| Type            | `AppCatBrokerRegion` |
| Required        | False                |
| Position        | Named                |
| Pipeline input  | False                |
| Aliases         | None                 |
| Accepted values | Eu, Us, Uk           |

### -Token

The personal access token, as created in the Patch My PC portal.

| Attribute      | Value                          |
| -------------- | ------------------------------ |
| Type           | `System.Security.SecureString` |
| Required       | True                           |
| Position       | 0                              |
| Pipeline input | False                          |
| Aliases        | None                           |

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

### System.Security.SecureString

The personal access token.

## Outputs

### CompanyInfo

The customer the token belongs to. Emitted only with -PassThru.

## Examples

### Example 1: Authenticate from a stored token

```powershell
$token = Read-Host -AsSecureString "PAT"
Connect-PmpcBrokerWithPat -Token $token -Region Us
```

Prompts without echoing the token, then authenticates against the US production region.

### Example 2: Authenticate unattended and keep the company

```powershell
$token = ConvertTo-SecureString $env:PMPC_PAT -AsPlainText -Force
$company = Connect-PmpcBrokerWithPat -Token $token -Region Eu -PassThru
```

Reads the token from the environment, as a build agent would, and captures the resolved customer.

## Notes

Takes a SecureString so the token is not left in command history or a transcript. What the session can then do is bounded by the scopes the token was granted, so a call may be refused for lack of scope even though authentication succeeded. Creating, listing, and revoking tokens are not available from a PAT session; manage tokens on the Access Tokens page of the Patch My PC portal.

-Region maps to the Patch My PC production regions only.

## Related links

* [Get-PmpcBrokerSession](get-pmpcbrokersession.md)
* [Disconnect-PmpcBroker](disconnect-pmpcbroker.md)
* PowerShell module

## See also

* SDK method: [AuthenticateWithPersonalAccessTokenAsync](../sdk/authentication.md#authenticatewithpersonalaccesstokenasync)
* REST operation: [`POST /v1/api/auth/token`](../rest-api/authentication.md#exchange-a-personal-access-token-for-an-access-token)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

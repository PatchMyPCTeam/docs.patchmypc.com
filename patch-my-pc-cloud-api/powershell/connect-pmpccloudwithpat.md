---
description: Authenticates using a personal access token.
noIndex: true
noRobotsIndex: true
---

# Connect-PmpcCloudWithPat

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

## Synopsis

Authenticates using a personal access token.

## Syntax

```powershell
Connect-PmpcCloudWithPat [-Token] <SecureString> [-PassThru] [-Region <PmpcCloudRegion>]
  [-ConfigurationFile <String>] [-MaxSingleFileUploadSize <Int64>] [-WhatIf] [-Confirm]
  [<CommonParameters>]
```

## Description

Exchanges a personal access token (PAT) for a short-lived gateway token and scopes the session to the customer that token belongs to. This is the authentication path for unattended callers. No company selection is needed afterwards, because the token identifies its own customer.

Provide the customer's region with -Region so the token exchange reaches the correct regional PatchMyPC.Cloud host.

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

| Attribute       | Value             |
| --------------- | ----------------- |
| Type            | `PmpcCloudRegion` |
| Required        | False             |
| Position        | Named             |
| Pipeline input  | False             |
| Aliases         | None              |
| Accepted values | Eu, Us, Uk        |

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
Connect-PmpcCloudWithPat -Token $token -Region Us
```

Prompts without echoing the token, then authenticates against the US production region.

### Example 2: Authenticate unattended and keep the company

```powershell
$token = ConvertTo-SecureString $env:PMPC_PAT -AsPlainText -Force
$company = Connect-PmpcCloudWithPat -Token $token -Region Eu -PassThru
```

Reads the token from the environment, as a build agent would, and captures the resolved customer.

## Notes

Takes a SecureString so the token is not left in command history or a transcript. What the session can then do is bounded by the scopes the token was granted, so a call may be refused for lack of scope even though authentication succeeded. To list or revoke tokens, use the Access Tokens page of the Patch My PC portal.

-Region maps only to Patch My PC production regional hosts.

## Related links

* [Get-PmpcCloudSession](get-pmpccloudsession.md)
* [Disconnect-PmpcCloud](disconnect-pmpccloud.md)
* PowerShell module

## See also

* SDK method: [AuthenticateWithPersonalAccessTokenAsync](../sdk/authentication.md#authenticatewithpersonalaccesstokenasync)
* REST operation: [`POST /v1/api/auth/token`](../rest-api/authentication.md#exchange-a-personal-access-token-for-an-access-token)
* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)

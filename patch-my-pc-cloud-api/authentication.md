---
description: >-
  Create a personal access token, exchange it for an access token, and send the
  access token with each request.
noIndex: true
noRobotsIndex: true
---

# Authentication

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

The Patch My PC Cloud Customer API authenticates each request with a short-lived access token. You get an access token by exchanging a personal access token (PAT). The same flow works from the REST API, the .NET SDK, and the PowerShell module, and it doesn't need a person at the keyboard, so you can use it in scripts, services, and pipelines.

Authentication takes three steps:

1. [Create a PAT](authentication.md#create-a-personal-access-token) with the scopes your job needs.
2. [Exchange the PAT for an access token](authentication.md#exchange-the-pat-for-an-access-token). The access token is valid for 60 minutes.
3. [Send the access token with each request](authentication.md#send-the-access-token), and exchange the PAT again when the access token expires.

The SDK and the PowerShell module do steps 2 and 3 for you.

## Create a personal access token

A PAT is a long-lived secret that lets your automation call the Cloud Customer API on your behalf. Each PAT belongs to one company—your Patch My PC cloud account—and has a name, an expiration date, and one or more scopes.

You create, view, and revoke PATs in the Patch My PC portal, under **Settings** > **Access Tokens**:

1. Select **Create Token**, and enter a name that describes what the token is for, for example `nightly-catalog-report`.
2. Choose the [scopes](authentication.md#scopes) the token needs.
3. In **Expires In Days**, enter a lifetime from 1 to 365 days. If you leave it blank, the token lasts 90 days.
4. Copy the token value and store it securely, for example in Azure Key Vault or your pipeline's secret variables.

{% hint style="warning" %}
The token value is shown only once. If you lose it, you can't retrieve it—create a new token and revoke the old one.
{% endhint %}

For step-by-step instructions, see [Create a personal access token](create-a-personal-access-token.md). For a full walkthrough of an unattended job, see [Automate with a personal access token](guides/automate-with-a-personal-access-token.md).

### Scopes

| Scope                        | Allows                                                                                                 |
| ---------------------------- | ------------------------------------------------------------------------------------------------------ |
| `appcatbroker:apps:read`     | Search applications, read application details and files, and list your connections                     |
| `appcatbroker:apps:write`    | Create, update, edit, and delete custom applications. Includes the access of `appcatbroker:apps:read`. |
| `appcatbroker:apps:deploy`   | Read, create, edit, sync, pause, redeploy, and delete deployments, and manage deployment templates     |
| `appcatbroker:customer:read` | Read your account information and usage limits                                                         |

Request only the scopes a job needs. In the portal, each scope appears with a label, such as **Read applications**. See [Choose scopes](create-a-personal-access-token.md#choose-scopes).

When a request needs a scope the token doesn't have, the Cloud Customer API returns `403 Forbidden` with the problem title `insufficient_scope`. The response names the scope that's required and the scopes the token has:

```json
{
  "title": "insufficient_scope",
  "status": 403,
  "detail": "{explanation}",
  "requiredScope": "appcatbroker:apps:write",
  "grantedScopes": ["appcatbroker:apps:read", "appcatbroker:customer:read"]
}
```

You can't add scopes to an existing token. Create a new token with the scopes you need and revoke the old one.

### What a PAT can and can't do

* **A PAT never has more access than the user who created it.** When you create a token, the requested scopes are narrowed to the permissions you hold. The token lists the scopes it was actually granted, which can be fewer than you requested.
* **You manage PATs in the portal.** Create, view, and revoke tokens on the **Access Tokens** page. A PAT can't create, list, or revoke tokens—including itself.
* **Treat the token like a password.** Keep it in a secret store and never write it to logs.
* **Revocation ends sessions.** A revoked token can't be exchanged again, and sessions that are already using it stop working shortly afterward, without waiting for their access token to expire.

## Exchange the PAT for an access token

A PAT isn't sent with every request. Instead, you exchange it for an access token that's valid for 60 minutes and send the access token on later requests.

{% tabs %}
{% tab title="REST" %}
Send the PAT in the `Authorization` header. The request has no body and no other authentication.

```http
POST https://us.portal.patchmypc.com/v1/api/auth/token
Authorization: Bearer {personal-access-token}
```

The examples on this page use the US host. If your Patch My PC account is in the EU region, use `https://eu.portal.patchmypc.com` instead.

A successful response returns the access token in the `gatewayJwt` property, and its lifetime in seconds:

```json
{
  "gatewayJwt": "{access-token}",
  "expiresIn": 3600
}
```

| Status                                           | Meaning                                                                                          | What to do                                                                                                          |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| `200 OK`                                         | The exchange succeeded                                                                           | Use the value of `gatewayJwt` as the access token                                                                   |
| `401 Unauthorized`                               | The `Authorization` header is missing or malformed, or the token is invalid, expired, or revoked | Check the header, then create a new token if needed. For security, the response doesn't say which of these applies. |
| `403 Forbidden`                                  | Your account isn't entitled to use personal access tokens                                        | Contact Patch My PC                                                                                                 |
| `429 Too Many Requests`                          | Too many exchanges from your network address                                                     | Wait for the `Retry-After` interval, then try again                                                                 |
| `400 Bad Request` or `500 Internal Server Error` | The exchange couldn't be completed                                                               | Retry with backoff                                                                                                  |

See [Exchange a personal access token for an access token](rest-api/authentication.md#exchange-a-personal-access-token-for-an-access-token).
{% endtab %}

{% tab title="C#" %}
{% code title="Program.cs" %}
```csharp
var pat = Environment.GetEnvironmentVariable("PMPC_PAT");

var session = await client.AuthenticateWithPersonalAccessTokenAsync(pat!);
if (session.IsFailure)
{
    // For example PAT_NOT_ENTITLED, PAT_EXCHANGE_THROTTLED, or AUTH_ERROR.
    Console.WriteLine($"{session.Error.Code}: {session.Error.Message}");
    return;
}

// The session now works with the token's company.
var info = await client.GetCustomerInfoAsync();
```
{% endcode %}

To route the session to your company's region, set `Region` (`Eu` or `Us`) in the `AppCatBrokerSdkConfig` configuration section.

See [AuthenticateWithPersonalAccessTokenAsync](sdk/authentication.md#authenticatewithpersonalaccesstokenasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
$pat = Read-Host -AsSecureString -Prompt 'Personal access token'
Connect-PmpcBrokerWithPat -Token $pat -Region Us
Get-PmpcCustomerInfo
```

`-Token` takes a `SecureString`. Set `-Region` to your company's region, `Eu` or `Us`. The session works with the token's company.

See [Connect-PmpcBrokerWithPat](powershell/connect-pmpcbrokerwithpat.md).
{% endtab %}
{% endtabs %}

## Send the access token

Send the access token as a bearer token in the `Authorization` header of every REST request:

```http
GET https://us.portal.patchmypc.com/v1/api/customer-info
Authorization: Bearer {access-token}
Accept: application/json
```

## Manage token lifetime

* **Access tokens last 60 minutes.** Read `expiresIn` from the exchange response and exchange the PAT again shortly before the access token expires, or when a request returns `401 Unauthorized` with the error `invalid_token`. There's no separate refresh operation—the exchange is the refresh.
* **A session ends when its PAT stops being valid.** If the PAT is revoked or expires, or its owner loses access, later requests return `401 Unauthorized` and exchanging the same PAT again fails. Create a new token.
* **The SDK and PowerShell module renew for you.** They cache the access token and exchange the PAT again as needed for as long as the session runs.
* **PATs expire too.** A PAT lasts 90 days by default and at most 365 days. Create a replacement before the old token expires, update your secret store, and then revoke the old token.
* **Don't exchange on every request.** Reuse the access token until it's close to expiry. Exchanges from the same network address are throttled.

## Related pages

* [Create a personal access token](create-a-personal-access-token.md)
* [Automate with a personal access token](guides/automate-with-a-personal-access-token.md)
* [Errors](errors.md)
* [Rate limits](rate-limits.md)

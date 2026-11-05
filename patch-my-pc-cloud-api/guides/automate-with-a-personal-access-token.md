---
description: >-
  Create a personal access token, store it securely, and use it to call the
  Patch My PC Cloud Customer API from unattended automation.
noIndex: true
noRobotsIndex: true
---

# Automate with a personal access token

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

Scheduled tasks, build agents, and other unattended jobs call the Cloud Customer API with a personal access token (PAT). You create the token once in the Patch My PC portal, store it in a secret store, and the job exchanges it for an access token each time it runs. The access token is valid for 60 minutes.

For how tokens, scopes, and access tokens work, see [Authentication](../authentication.md).

## Before you begin

* Have a Patch My PC portal account for your company that can open **Settings** > **Access Tokens**. A token never has more access than the user who creates it, so the account needs the permissions the job will use.
* Decide which scopes the job needs. See [Scopes](../authentication.md#scopes).
* Choose where to store the token, for example Azure Key Vault or your pipeline's secret variables.
* Know your company's region, US or EU. The REST API uses the matching host, and the SDK and PowerShell module need the region to exchange the token.

## Step 1: Create the token

Create the token in the Patch My PC portal:

1. In the Patch My PC portal, go to **Settings** > **Access Tokens** and select **Create Token**.
2. Enter a descriptive name, for example the name of the job that uses it.
3. Choose the scopes the job needs.
4. In **Expires In Days**, enter a lifetime from 1 to 365 days. If you leave it blank, the token lasts 90 days.
5. Select **Create**, then copy the token value straight into your secret store. It's shown only once.

The token's scopes can be fewer than you chose if your own account lacks a permission. For step-by-step instructions with screenshots, see [Create a personal access token](../create-a-personal-access-token.md).

## Step 2: Store the token securely

1. Save the token value in a secret store that your job can read at run time.
2. Make the job read it into memory, for example through an environment variable that the pipeline injects from a secret variable.
3. Never commit the token to source control, pass it on a command line that's logged, or write it to output. Log the token's ID or prefix instead.

## Step 3: Exchange the token

The job exchanges the token for an access token. The token identifies its own company, so the job doesn't select one.

{% tabs %}
{% tab title="REST" %}
This example uses the US host. If your account is hosted in the EU, use `https://eu.portal.patchmypc.com` instead.

```http
POST https://us.portal.patchmypc.com/v1/api/auth/token
Authorization: Bearer {personal-access-token}
```

The `gatewayJwt` property of the response holds the access token:

```json
{
  "gatewayJwt": "{access-token}",
  "expiresIn": 3600
}
```

Keep the access token in memory and note when it expires: the time of the response plus `expiresIn` seconds.

See [Exchange a personal access token for an access token](../rest-api/authentication.md#exchange-a-personal-access-token-for-an-access-token).
{% endtab %}

{% tab title="C#" %}
Set your company's region in configuration, for example the environment variable `AppCatBrokerSdkConfig__Region=Us`, then exchange the token:

{% code title="Program.cs" %}
```csharp
var pat = Environment.GetEnvironmentVariable("PMPC_PAT");

var session = await broker.AuthenticateWithPersonalAccessTokenAsync(pat!);
if (session.IsFailure)
{
    // For example PAT_NOT_ENTITLED, PAT_EXCHANGE_THROTTLED, or AUTH_ERROR.
    Console.WriteLine($"{session.Error.Code}: {session.Error.Message}");
    return;
}
```
{% endcode %}

See [AuthenticateWithPersonalAccessTokenAsync](../sdk/authentication.md#authenticatewithpersonalaccesstokenasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
$token = ConvertTo-SecureString $env:PMPC_PAT -AsPlainText -Force
Connect-PmpcBrokerWithPat -Token $token -Region Us
```

`-Token` takes a `SecureString`, so the token value isn't left in your command history. If your account is hosted in the EU, use `-Region Eu`.

See [Connect-PmpcBrokerWithPat](../powershell/connect-pmpcbrokerwithpat.md).
{% endtab %}
{% endtabs %}

## Step 4: Call the API

Make requests as usual. What the job can do is limited to the token's scopes; a request outside them returns `403 Forbidden` with the problem title `insufficient_scope`.

{% tabs %}
{% tab title="REST" %}
```http
GET https://us.portal.patchmypc.com/v1/api/customer-info
Authorization: Bearer {access-token}
Accept: application/json
```

Exchange the PAT again shortly before the access token expires, or when a request returns `401 Unauthorized` with the error `invalid_token`. Don't exchange on every request—exchanges are throttled.

See [Get customer info](../rest-api/applications.md#get-customer-info).
{% endtab %}

{% tab title="C#" %}
```csharp
var info = await broker.GetCustomerInfoAsync();
if (info.IsFailure)
{
    Console.WriteLine($"{info.Error.Code}: {info.Error.Message}");
}
```

The SDK exchanges the PAT again when it needs a new access token.

See [GetCustomerInfoAsync](../sdk/customer-and-connections.md#getcustomerinfoasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcCustomerInfo
```

The module exchanges the PAT again when it needs a new access token.

See [Get-PmpcCustomerInfo](../powershell/get-pmpccustomerinfo.md).
{% endtab %}
{% endtabs %}

## Step 5: Rotate and revoke tokens

Replace a token before it expires, and revoke any token you no longer use or suspect was exposed. Revocation can't be undone.

1. Create a replacement token, as in Step 1.
2. Update the secret store with the new value.
3. Confirm the job runs with the new token.
4. In the portal, go to **Settings** > **Access Tokens**, find the old token, select the revoke (trash) icon at the end of its row, and confirm.

Any automation that still uses the old token loses access immediately. Use the **Expires** and **Last Used** columns to find tokens that are about to expire or are no longer used. For details, see [Revoke a token](../create-a-personal-access-token.md#revoke-a-token).

## Related pages

* [Authentication](../authentication.md)
* [Create a personal access token](../create-a-personal-access-token.md)
* [Errors](../errors.md)
* [Rate limits](../rate-limits.md)

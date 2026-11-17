---
description: >-
  Create a personal access token, store it securely, and use it to call the
  Patch My PC Cloud Customer API from unattended automation.
noIndex: true
noRobotsIndex: true
---

# Automate with a personal access token

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

Scheduled tasks, build agents, and other unattended jobs call the Cloud Customer API with a personal access token (PAT). You create the token once in the Patch My PC portal, store it in a secret store, and the job exchanges it for an access token each time it runs. The exchange response tells you how long the access token is valid.

For how tokens, scopes, and access tokens work, see [Authentication](../authentication.md).

The examples below exchange a PAT and read your company's account information using the SDK, PowerShell module, or direct REST requests. For an application workflow, see [Create and deploy a custom application with REST](https://docs.patchmypc.com/patch-my-pc-cloud-api/guides/create-a-custom-application-with-rest). See the [REST authentication reference](https://docs.patchmypc.com/patch-my-pc-cloud-api/rest-api/authentication) for the token exchange contract.

## Before you begin

* Have a Patch My PC portal account for your company that can open **Settings** > **Access Tokens**. A token never has more access than the user who creates it, so the account needs the permissions the job will use.
* Decide which scopes the job needs. The customer-info call in this guide requires `appcatbroker:customer:read`. See [Scopes](https://docs.patchmypc.com/patch-my-pc-cloud-api/authentication#scopes).
* Choose where to store the token, for example Azure Key Vault or your pipeline's secret variables.
* Know your company's region, US, EU, or UK. The REST API uses the matching host, and the SDK and PowerShell module need the region to exchange the token.
* For the REST examples, use PowerShell 7.4 or later and run Steps 3 and 4 in the same session. They use built-in HTTP commands, not the Patch My PC PowerShell module.

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
{% tab title="C#" %}
Set your company's region in configuration, for example the environment variable `PmpcCloudSdkConfig__Region=Us`, then exchange the token:

{% code title="Program.cs" collapsedlinecount="10" %}
```csharp
var pat = Environment.GetEnvironmentVariable("PMPC_PAT");

var session = await client.AuthenticateWithPersonalAccessTokenAsync(pat!);
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
{% code collapsedlinecount="10" %}
```powershell
$token = ConvertTo-SecureString $env:PMPC_PAT -AsPlainText -Force
Connect-PmpcCloudWithPat -Token $token -Region Us
```
{% endcode %}

`-Token` takes a `SecureString`, so the token value isn't left in your command history. Set `-Region` to your company's region: `Us`, `Eu`, or `Uk`.

See [Connect-PmpcCloudWithPat](../powershell/connect-pmpccloudwithpat.md).
{% endtab %}

{% tab title="REST (PowerShell)" %}
Read the PAT from the environment variable supplied by your secret store. Use `eu.portal.patchmypc.com` or `uk.portal.patchmypc.com` instead of the US host when appropriate.

{% code collapsedlinecount="10" %}
```powershell
$ErrorActionPreference = 'Stop'
$api = 'https://us.portal.patchmypc.com/v1/api'

if ([string]::IsNullOrWhiteSpace($env:PMPC_PAT)) {
    throw 'Set PMPC_PAT from your secret store before running this example.'
}

$exchange = Invoke-RestMethod -Method Post -Uri "$api/auth/token" -Headers @{
    Authorization = "Bearer $env:PMPC_PAT"
    Accept = 'application/json'
}
$accessToken = $exchange.gatewayJwt
$expiresIn = 0
if ([string]::IsNullOrWhiteSpace($accessToken) -or
    -not [int]::TryParse([string]$exchange.expiresIn, [ref]$expiresIn) -or
    $expiresIn -le 0) {
    throw 'The exchange did not return an access token and a positive lifetime.'
}

$accessTokenExpiresAt = [datetimeoffset]::UtcNow.AddSeconds($expiresIn)
'Access token expires at {0:o}' -f $accessTokenExpiresAt
```
{% endcode %}

Keep the access token in memory; do not print `$exchange` or `$accessToken`. A direct REST caller must exchange the PAT again before the access token expires. This example does not implement a refresh loop.
{% endtab %}
{% endtabs %}

## Step 4: Call the API

Make requests as usual. What the job can do is limited to the token's scopes; a request outside them returns `403 Forbidden` with the problem title `insufficient_scope`.

{% tabs %}
{% tab title="C#" %}
{% code collapsedlinecount="10" %}
```csharp
var info = await client.GetCustomerInfoAsync();
if (info.IsFailure)
{
    Console.WriteLine($"{info.Error.Code}: {info.Error.Message}");
}
```
{% endcode %}

The SDK exchanges the PAT again when it needs a new access token.

See [GetCustomerInfoAsync](../sdk/customer-and-connections.md#getcustomerinfoasync).
{% endtab %}

{% tab title="PowerShell" %}
{% code collapsedlinecount="10" %}
```powershell
Get-PmpcCustomerInfo
```
{% endcode %}

The module exchanges the PAT again when it needs a new access token.

See [Get-PmpcCustomerInfo](../powershell/get-pmpccustomerinfo.md).
{% endtab %}

{% tab title="REST (PowerShell)" %}
Use the access token from Step 3, not the PAT, as the bearer credential:

{% code collapsedlinecount="10" %}
```powershell
$headers = @{
    Authorization = "Bearer $accessToken"
    Accept = 'application/json'
}
$info = Invoke-RestMethod -Method Get -Uri "$api/customer-info" -Headers $headers
$info | Select-Object customerId, customerName, limits, limitsProgress
```
{% endcode %}

The result identifies your company and shows its account limits and current usage. The PAT's `appcatbroker:customer:read` scope is needed even if it already has application scopes.
{% endtab %}
{% endtabs %}

## Step 5: Rotate and revoke tokens

Replace a token before it expires, and revoke any token you no longer use or suspect was exposed. Revocation can't be undone.

1. Create a replacement token, as in Step 1.
2. Update the secret store with the new value.
3. Confirm the job runs with the new token.
4. In the portal, go to **Settings** > **Access Tokens**, find the old token, select the revoke (trash) icon at the end of its row, and confirm.

After revocation, the old PAT can no longer be exchanged for a new access token. Already-issued access tokens are not immediately invalidated, so do not rely on revocation to end every active session immediately. Use the **Expires** and **Last Used** columns to find tokens that are about to expire or are no longer used. For details, see [Revoke a token](https://docs.patchmypc.com/patch-my-pc-cloud-api/create-a-personal-access-token#revoke-a-token).

## Related pages

* [Authentication](../authentication.md)
* [Create a personal access token](../create-a-personal-access-token.md)
* [Errors](../errors.md)
* [Rate limits](../rate-limits.md)

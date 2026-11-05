---
description: >-
  Set up access to the Patch My PC Cloud Customer API and make your first call
  from REST, C#, or PowerShell.
noIndex: true
noRobotsIndex: true
---

# Getting started

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

This page takes you from nothing to a first successful call to the Patch My PC Cloud Customer API. The first call reads your account information, which every account can do.

## Before you begin

You need:

* **A Patch My PC cloud account.** The Cloud Customer API acts on the account—also called the company—that your token belongs to. Your account is hosted in one region, US or EU.
* **Permissions in that account.** The Cloud Customer API never lets you do more than you can do yourself. To read applications you need read access to applications; to create or update them you need write access; to manage deployments you need deployment access.
* **A personal access token (PAT).** Create one in the Patch My PC portal, and give it the `appcatbroker:customer:read` scope for this first call. For the steps, see [Create a personal access token](authentication.md#create-a-personal-access-token).

{% hint style="info" %}
Some operations—for example deployments, connections, and editing or deleting applications—must be enabled for your account. Reading your account information, searching your own applications, and creating applications and publishing new versions of them are always available.
{% endhint %}

## Choose a surface

| If you…                                                        | Use               |
| -------------------------------------------------------------- | ----------------- |
| Build a .NET application                                       | .NET SDK          |
| Write scripts or work at a PowerShell prompt                   | PowerShell module |
| Work in another language, or want full control of each request | REST API          |

The SDK and the PowerShell module handle the token exchange, regional endpoints, token renewal, file uploads, and retries for you. The REST API gives you the raw operations.

## Make your first call

Read your account information and usage limits.

{% tabs %}
{% tab title="REST" %}
These examples use the US host, `https://us.portal.patchmypc.com`. If your account is hosted in the EU, use `https://eu.portal.patchmypc.com` instead.

1. Exchange your PAT for an access token. For details, see [Exchange the PAT for an access token](authentication.md#exchange-the-pat-for-an-access-token).

```http
POST https://us.portal.patchmypc.com/v1/api/auth/token
Authorization: Bearer {personal-access-token}
```

2. Call the customer information operation with the access token from the `gatewayJwt` property of the response. The access token is valid for 60 minutes.

```http
GET https://us.portal.patchmypc.com/v1/api/customer-info
Authorization: Bearer {access-token}
Accept: application/json
```

See [Get customer info](rest-api/applications.md#get-customer-info).
{% endtab %}

{% tab title="C#" %}
1. Add the `pmpc.appcatbroker.sdk` package from nuget.org to your project. The SDK targets .NET 8 and .NET 10.

```bash
dotnet add package pmpc.appcatbroker.sdk
```

2. Set your account's region, `Us` or `Eu`, in configuration.

{% code title="appsettings.json" %}
```json
{
  "AppCatBrokerSdkConfig": {
    "Region": "Us"
  }
}
```
{% endcode %}

3. Register the SDK, authenticate with your PAT, and make the call. This example reads the PAT from the `PMPC_PAT` environment variable, so the token stays out of your source code.

{% code title="Program.cs" %}
```csharp
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using pmpc.appcatbroker.sdk.Extensions;
using pmpc.appcatbroker.sdk.Services;

var configuration = new ConfigurationBuilder()
    .AddJsonFile("appsettings.json")
    .AddEnvironmentVariables()
    .Build();

var services = new ServiceCollection();
services.AddSingleton<IConfiguration>(configuration);
services.AddAppCatBrokerSdk();

var broker = services.BuildServiceProvider().GetRequiredService<IAppCatBroker>();

var pat = Environment.GetEnvironmentVariable("PMPC_PAT")
    ?? throw new InvalidOperationException("Set PMPC_PAT to a personal access token.");

// Exchanges the PAT for an access token for the token's company.
var session = await broker.AuthenticateWithPersonalAccessTokenAsync(pat);
if (session.IsFailure)
{
    Console.WriteLine($"{session.Error.Code}: {session.Error.Message}");
    return;
}

var info = await broker.GetCustomerInfoAsync();
if (info.IsSuccess)
{
    Console.WriteLine(info.Value.CustomerName);
}
```
{% endcode %}

See [GetCustomerInfoAsync](sdk/customer-and-connections.md#getcustomerinfoasync).
{% endtab %}

{% tab title="PowerShell" %}
1. Install the module from the PowerShell Gallery. It requires PowerShell 7.4 or later on Windows, macOS, or Linux.

```powershell
Install-Module PatchMyPC.AppCatBroker -Scope CurrentUser
```

2. Connect with your PAT and make the call. `Read-Host -AsSecureString` prompts for the token without showing it on screen.

```powershell
$token = Read-Host -AsSecureString -Prompt 'Personal access token'
Connect-PmpcBrokerWithPat -Token $token -Region Us
Get-PmpcCustomerInfo
```

If your account is hosted in the EU, use `-Region Eu`.

See [Connect-PmpcBrokerWithPat](powershell/connect-pmpcbrokerwithpat.md) and [Get-PmpcCustomerInfo](powershell/get-pmpccustomerinfo.md).
{% endtab %}
{% endtabs %}

Every SDK method returns a result instead of throwing an exception, and every cmdlet writes a PowerShell error record with a stable error code. See [Errors](errors.md).

## Next steps

* [Authentication](authentication.md)
* [Automate with a personal access token](guides/automate-with-a-personal-access-token.md)
* [Search the catalog](guides/search-the-catalog.md)
* [Create a custom application](guides/create-a-custom-application.md)
* [Deploy an application](guides/deploy-an-application.md)
* [Rate limits](rate-limits.md)

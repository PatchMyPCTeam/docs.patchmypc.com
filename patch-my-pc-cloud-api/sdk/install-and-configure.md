---
description: >-
  Install the .NET SDK package, register it with dependency injection, and
  configure its region and upload options.
noIndex: true
noRobotsIndex: true
---

# Install and configure the SDK

This page shows you how to add the .NET SDK for the Patch My PC Cloud Customer API to a project, register it with dependency injection, set its options, and get an `IAppCatBroker` instance to call.

## Prerequisites

* .NET 8 or .NET 10. The package targets `net8.0` and `net10.0`.
* A personal access token (PAT) with the scopes your application needs. You create one in the Patch My PC portal. For details, see [Create a personal access token](../create-a-personal-access-token.md).

## Install the package

The `pmpc.appcatbroker.sdk` package is published on nuget.org. Add it to your project:

```bash
dotnet add package pmpc.appcatbroker.sdk
```

The examples on this page also use the .NET generic host, so add it if your project doesn't reference it already:

```bash
dotnet add package Microsoft.Extensions.Hosting
```

## Register the SDK

Call `AddAppCatBrokerSdk` on your service collection. It registers `IAppCatBroker` and everything it depends on, and binds the `AppCatBrokerSdkConfig` configuration section to the SDK's options.

```csharp
using pmpc.appcatbroker.sdk.Extensions;

builder.Services.AddAppCatBrokerSdk();
```

`AddAppCatBrokerSdk` reads its options from `IConfiguration`, so register configuration before you call it. The .NET generic host (`Host.CreateApplicationBuilder` or `Host.CreateDefaultBuilder`) does this for you.

## Configure the SDK

Put the SDK's options in an `AppCatBrokerSdkConfig` section, for example in `appsettings.json`:

{% code title="appsettings.json" %}
```json
{
  "AppCatBrokerSdkConfig": {
    "Region": "Us"
  }
}
```
{% endcode %}

Like any .NET configuration, you can also supply the values as environment variables, for example `AppCatBrokerSdkConfig__Region=Eu`. Keep your personal access token out of configuration files and source control; read it from a secret store or an environment variable at run time.

### SDK options

| Option   | Type                 | Default | Description                                                                                                                                  |
| -------- | -------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `Region` | `AppCatBrokerRegion` | None    | The region your Patch My PC account is hosted in: `Us` or `Eu`. Required, so the SDK knows which regional service to exchange your PAT with. |

### Upload options

`CreateApplicationAsync`, `UpdateApplicationAsync`, `EditApplicationAsync`, and their custom-application counterparts accept an optional `ChunkUploadOptions` that controls how installer files are uploaded. Leave it `null` to use the defaults.

| Option                  | Type       | Default                             | Description                                                                                                                    |
| ----------------------- | ---------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `ChunkSize`             | `int`      | 8 MB (`8 * 1024 * 1024`)            | Size of each upload chunk in bytes. Files larger than 32 MB are uploaded in chunks; smaller files are uploaded in one request. |
| `MaxChunkConcurrency`   | `int`      | 4                                   | Maximum number of chunks of one file uploaded at the same time.                                                                |
| `MaxFileConcurrency`    | `int`      | 4                                   | Maximum number of files uploaded at the same time.                                                                             |
| `MaxHashingConcurrency` | `int`      | Number of processors on the machine | Maximum number of files hashed at the same time before upload.                                                                 |
| `Timeout`               | `TimeSpan` | 30 minutes                          | Timeout for each upload request.                                                                                               |
| `RetryAttempts`         | `int`      | 3                                   | Number of times a failed chunk upload is retried.                                                                              |

One application version can contain up to 1,000 files and 30 GB in total.

```csharp
var uploadOptions = new ChunkUploadOptions
{
    ChunkSize = 16 * 1024 * 1024,
    MaxChunkConcurrency = 8,
    MaxFileConcurrency = 8,
};
```

## Get an IAppCatBroker instance

Resolve `IAppCatBroker` from a dependency injection scope. The SDK registers it as a scoped service, and the instance remembers your access token, company, and selected connection, so use the same instance for a whole session.

```csharp
using var scope = host.Services.CreateScope();
var broker = scope.ServiceProvider.GetRequiredService<IAppCatBroker>();
```

In an ASP.NET Core application or a worker service, inject `IAppCatBroker` into your own scoped services instead.

## Authenticate

Before you call most methods, authenticate with your personal access token. Call `AuthenticateWithPersonalAccessTokenAsync`: it exchanges the PAT for an access token, scopes the session to the token's company in one step, and renews the access token for you as it expires.

For deployment, deployment template, and public catalog methods, also select a connection with `SetSelectedConnectionAsync`. For details, see [SDK authentication methods](authentication.md) and [Customer information and connections](customer-and-connections.md).

## Complete example

This console application authenticates with a personal access token read from the `PMPC_PAT` environment variable, selects the first connection, prints the account's information, and lists the first page of applications. Set `Region` in configuration before you run it.

{% code title="Program.cs" %}
```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using pmpc.appcatbroker.client;
using pmpc.appcatbroker.sdk.Extensions;
using pmpc.appcatbroker.sdk.Services;

var builder = Host.CreateApplicationBuilder(args);
builder.Services.AddAppCatBrokerSdk();
using var host = builder.Build();

using var scope = host.Services.CreateScope();
var broker = scope.ServiceProvider.GetRequiredService<IAppCatBroker>();

// Authenticate with a personal access token. The session uses the token's company.
var pat = Environment.GetEnvironmentVariable("PMPC_PAT");
if (string.IsNullOrWhiteSpace(pat))
{
    Console.WriteLine("Set PMPC_PAT to a personal access token.");
    return 1;
}

var session = await broker.AuthenticateWithPersonalAccessTokenAsync(pat);
if (session.IsFailure)
{
    Console.WriteLine($"Authentication failed: {session.Error.Code} {session.Error.Message}");
    return 1;
}

var company = session.Value;
Console.WriteLine($"Working with {company.CompanyName}");

// Show account information and limits.
var customerInfo = await broker.GetCustomerInfoAsync();
if (customerInfo.IsSuccess)
{
    Console.WriteLine($"Account: {customerInfo.Value.CustomerName}");
}

// Select a connection for deployment and catalog calls.
var connections = await broker.GetAvailableConnectionsAsync();
if (connections.IsSuccess && connections.Value.Count > 0)
{
    await broker.SetSelectedConnectionAsync(connections.Value[0]);
    Console.WriteLine($"Connection: {connections.Value[0].DisplayName}");
}

// List the first page of your applications.
var search = await broker.SearchApplicationsAsync(new ProductFilterRequest
{
    Skip = 0,
    Limit = 25,
});

if (search.IsFailure)
{
    Console.WriteLine($"Search failed: {search.Error.Code} {search.Error.Message}");
    return 1;
}

Console.WriteLine($"{search.Value.TotalAmount} applications found");
foreach (var product in search.Value.Products)
{
    Console.WriteLine($"  {product.DisplayName} {product.Version} ({product.ProductId})");
}

await broker.ClearAuthenticationAsync();
return 0;
```
{% endcode %}

The example needs a PAT with the `appcatbroker:apps:read` and `appcatbroker:customer:read` scopes.

## Related pages

{% content-ref url="results-and-errors.md" %}
[results-and-errors.md](results-and-errors.md)
{% endcontent-ref %}

{% content-ref url="authentication.md" %}
[authentication.md](authentication.md)
{% endcontent-ref %}

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

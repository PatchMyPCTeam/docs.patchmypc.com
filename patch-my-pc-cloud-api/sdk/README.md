---
description: >-
  Use the .NET SDK to call the Patch My PC Cloud Customer API from your own
  applications and automation.
noIndex: true
noRobotsIndex: true
---

# .NET SDK

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

The .NET SDK is a client library for the Patch My PC Cloud Customer API. It authenticates with a personal access token, keeps track of the company and connection you're working with, uploads installer files in parallel chunks, and returns every outcome as a result object instead of throwing exceptions. Everything the SDK exposes is on one interface, `IAppCatBroker`.

Use the SDK when you're building a .NET application or service. If you're scripting, the PowerShell module wraps the same interface with one cmdlet per method. If you're working from another language, call the REST API directly.

## Supported frameworks

The NuGet package `pmpc.appcatbroker.sdk` targets:

| Target framework | Use it for                       |
| ---------------- | -------------------------------- |
| `net8.0`         | Applications that run on .NET 8  |
| `net10.0`        | Applications that run on .NET 10 |

The SDK authenticates with a personal access token (PAT), so it needs no user at the keyboard and suits services, scheduled jobs, and pipelines. You create the PAT in the Patch My PC portal. For details, see [Create a personal access token](../create-a-personal-access-token.md) and [Authentication](../authentication.md).

## Quick start

1.  Add the package to your project. It's published on nuget.org:

    ```bash
    dotnet add package pmpc.appcatbroker.sdk
    ```
2. Set your account's region, `Us` or `Eu`, in the `AppCatBrokerSdkConfig` configuration section, for example with the environment variable `AppCatBrokerSdkConfig__Region=Us`.
3.  Register the SDK, authenticate with your personal access token, and make a call:

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

    var pat = Environment.GetEnvironmentVariable("PMPC_PAT")
        ?? throw new InvalidOperationException("Set PMPC_PAT to a personal access token.");

    var session = await broker.AuthenticateWithPersonalAccessTokenAsync(pat);
    if (session.IsFailure)
    {
        Console.WriteLine($"Authentication failed: {session.Error.Code} {session.Error.Message}");
        return;
    }

    var search = await broker.SearchApplicationsAsync(new ProductFilterRequest { DisplayNameSearchString = "Contoso" });
    if (search.IsSuccess)
    {
        foreach (var product in search.Value.Products)
        {
            Console.WriteLine($"{product.ProductId} {product.DisplayName} {product.Version}");
        }
    }
    ```

For configuration options and a complete console example, see [Install and configure the SDK](install-and-configure.md).

## Method index

### Authentication

| Method                                                                                                   | Description                                                         |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| [`AuthenticateWithPersonalAccessTokenAsync`](authentication.md#authenticatewithpersonalaccesstokenasync) | Authenticates with a personal access token and selects its company. |
| [`GetSelectedCompany`](authentication.md#getselectedcompany)                                             | Returns the company the session works with.                         |
| [`ClearAuthenticationAsync`](authentication.md#clearauthenticationasync)                                 | Signs out and clears the session's company.                         |
| [`IsServiceHealthyAsync`](authentication.md#isservicehealthyasync)                                       | Checks whether the Cloud Customer API is reachable.                 |

### Customer information and connections

| Method                                                                                     | Description                                                   |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------- |
| [`GetCustomerInfoAsync`](customer-and-connections.md#getcustomerinfoasync)                 | Gets your account information and usage limits.               |
| [`GetAvailableConnectionsAsync`](customer-and-connections.md#getavailableconnectionsasync) | Lists the connections for your company.                       |
| [`SetSelectedConnectionAsync`](customer-and-connections.md#setselectedconnectionasync)     | Selects the connection that deployment and catalog calls use. |
| [`GetSelectedConnection`](customer-and-connections.md#getselectedconnection)               | Returns the currently selected connection.                    |

### Applications

| Method                                                                                 | Description                                                     |
| -------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| [`SearchApplicationsAsync`](applications.md#searchapplicationsasync)                   | Searches your applications with filters, sorting, and paging.   |
| [`GetApplicationDetailsAsync`](applications.md#getapplicationdetailsasync)             | Gets the details of one of your applications.                   |
| [`CreateApplicationAsync`](applications.md#createapplicationasync)                     | Uploads installer files and creates a new application.          |
| [`UpdateApplicationAsync`](applications.md#updateapplicationasync)                     | Uploads a new version of an existing application.               |
| [`EditApplicationAsync`](applications.md#editapplicationasync)                         | Corrects the metadata or files of the current version in place. |
| [`GetApplicationFilesAsync`](applications.md#getapplicationfilesasync)                 | Lists the files in an application's current version.            |
| [`SearchPublicApplicationsAsync`](applications.md#searchpublicapplicationsasync)       | Searches the Patch My PC public catalog.                        |
| [`GetPublicApplicationDetailsAsync`](applications.md#getpublicapplicationdetailsasync) | Gets the details of a public catalog application.               |

### Custom applications

| Method                                                                                        | Description                                               |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| [`SearchCustomApplicationsAsync`](custom-applications.md#searchcustomapplicationsasync)       | Searches your custom applications.                        |
| [`GetCustomApplicationDetailsAsync`](custom-applications.md#getcustomapplicationdetailsasync) | Gets the details of a custom application.                 |
| [`CreateCustomApplicationAsync`](custom-applications.md#createcustomapplicationasync)         | Uploads installer files and creates a custom application. |
| [`UpdateCustomApplicationAsync`](custom-applications.md#updatecustomapplicationasync)         | Uploads a new version of a custom application.            |
| [`EditCustomApplicationAsync`](custom-applications.md#editcustomapplicationasync)             | Corrects a custom application's current version in place. |
| [`DeleteApplicationAsync`](custom-applications.md#deleteapplicationasync)                     | Deletes one of your custom applications.                  |
| [`DeleteCustomApplicationAsync`](custom-applications.md#deletecustomapplicationasync)         | Deletes one of your custom applications.                  |

### Deployments

| Method                                                                                            | Description                                                    |
| ------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| [`GetDeploymentsAsync`](deployments.md#getdeploymentsasync)                                       | Lists an application's deployments on the selected connection. |
| [`GetDeploymentDetailsAsync`](deployments.md#getdeploymentdetailsasync)                           | Gets the full detail of one deployment.                        |
| [`GetDeploymentDependencyCandidatesAsync`](deployments.md#getdeploymentdependencycandidatesasync) | Lists deployments that can be used as dependencies.            |
| [`CreateDeploymentAsync`](deployments.md#createdeploymentasync)                                   | Creates a deployment for an application.                       |
| [`EditDeploymentAsync`](deployments.md#editdeploymentasync)                                       | Changes selected settings on an existing deployment.           |
| [`DeleteDeploymentAsync`](deployments.md#deletedeploymentasync)                                   | Deletes a deployment.                                          |
| [`RedeployDeploymentAsync`](deployments.md#redeploydeploymentasync)                               | Recreates a deployment from scratch.                           |
| [`SyncDeploymentAsync`](deployments.md#syncdeploymentasync)                                       | Moves a deployment to its latest pending version.              |
| [`SetDeploymentSyncPauseStatusAsync`](deployments.md#setdeploymentsyncpausestatusasync)           | Pauses or resumes a deployment's scheduled sync.               |

### Deployment templates

| Method                                                                                   | Description                                                |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [`GetDeploymentTemplatesAsync`](deployment-templates.md#getdeploymenttemplatesasync)     | Lists the deployment templates on the selected connection. |
| [`GetDeploymentTemplateAsync`](deployment-templates.md#getdeploymenttemplateasync)       | Gets the settings stored in a deployment template.         |
| [`CreateDeploymentTemplateAsync`](deployment-templates.md#createdeploymenttemplateasync) | Creates a deployment template.                             |
| [`UpdateDeploymentTemplateAsync`](deployment-templates.md#updatedeploymenttemplateasync) | Replaces the settings of a deployment template.            |
| [`DeleteDeploymentTemplateAsync`](deployment-templates.md#deletedeploymenttemplateasync) | Deletes a deployment template.                             |

## Related pages

{% content-ref url="install-and-configure.md" %}
[install-and-configure.md](install-and-configure.md)
{% endcontent-ref %}

{% content-ref url="results-and-errors.md" %}
[results-and-errors.md](results-and-errors.md)
{% endcontent-ref %}

{% content-ref url="../authentication.md" %}
[authentication.md](../authentication.md)
{% endcontent-ref %}

{% content-ref url="../cross-reference.md" %}
[cross-reference.md](../cross-reference.md)
{% endcontent-ref %}

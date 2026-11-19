---
description: >-
  Find your own custom applications and applications in the Patch My PC catalog,
  and read their details, with the Patch My PC Cloud Customer API.
noIndex: true
noRobotsIndex: true
---

# Search the catalog

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

Use the Patch My PC Cloud Customer API to find applications and read their details. There are two catalogs:

* **Your custom applications**—the applications your company created and uploaded.
* **The Patch My PC catalog**—the public catalog of applications that Patch My PC packages and maintains for you. Searching it is scoped to one of your connections.

This guide covers the SDK and PowerShell module. For REST search requests, see [Search applications](../rest-api/applications.md#search-applications) and [Search public applications](../rest-api/applications.md#search-public-applications). For a complete custom-application workflow, see [Create and deploy a custom application with REST](https://docs.patchmypc.com/patch-my-pc-cloud-api/guides/create-a-custom-application-with-rest); it does not demonstrate public-catalog search.

## Which ID should I use?

| What you want to do                                | Which ID to use                                                                                                          |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Read application details                           | Use `productId` from the search result for either catalog.                                                               |
| Publish a new version of your custom application   | Use `productId` and `custom.updateId` from the custom search result.                                                     |
| Deploy your custom application                     | Use `productId` and `custom.catalogEntryId` from the custom application details.                                         |
| Deploy an application from the Patch My PC catalog | Choose an installer variant in the application details and use that variant's `productId` and `catalogEntryId` together. |

## Before you begin

* Exchange a personal access token (PAT) for an access token. See [Authentication](../authentication.md).
* A PAT needs the `appcatbroker:apps:read` scope.

## Search your custom applications

1. Send a search with the text to match against the display name. Every filter is optional; for example, you can also filter by language, architecture, or the date an application was last updated.
2. Page through the results with `skip` and `limit`. The default page size is 50; `totalAmount` reports the number of matches across all pages.
3. Note the `productId` and `custom.updateId` of the application you want.

{% tabs %}
{% tab title="C#" %}
{% code title="Program.cs" %}
```csharp
using PatchMyPC.Cloud.Client;

const int pageSize = 50;
var skip = 0;
long totalAmount;

do
{
    var pageResult = await client.SearchCustomApplicationsAsync(new ProductFilterRequest
    {
        DisplayNameSearchString = "Contoso",
        Skip = skip,
        Limit = pageSize
    });

    if (pageResult.IsFailure)
    {
        Console.WriteLine($"{pageResult.Error.Code}: {pageResult.Error.Message}");
        return;
    }

    var page = pageResult.Value;
    totalAmount = page.TotalAmount;
    foreach (var app in page.Products)
    {
        Console.WriteLine($"{app.DisplayName} {app.Version}  product: {app.ProductId}  update: {app.Custom?.UpdateId}");
    }

    if (page.Products.Count == 0)
    {
        break;
    }

    skip += page.Products.Count;
}
while (skip < totalAmount);
```
{% endcode %}

See [SearchApplicationsAsync](../sdk/applications.md#searchapplicationsasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Find-PmpcCustomApplication -DisplayName 'Contoso' -Limit 25 |
    Select-Object DisplayName, Version, ProductId, @{ Name = 'UpdateId'; Expression = { $_.Custom.UpdateId } }
```

This returns one page. To request the next 25 matches, set `-Skip 25 -Limit 25`; continue increasing `-Skip` until you reach the total from `Find-PmpcCustomApplication -DisplayName 'Contoso' -Limit 1 -AsResponse`.

See [Find-PmpcCustomApplication](../powershell/find-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Get the details of a custom application

1. Use the product ID from a search result to read the application's details, including its current version, installer, install arguments, and detection rules.

{% tabs %}
{% tab title="C#" %}
```csharp
var details = await client.GetCustomApplicationDetailsAsync(productId);
if (details.IsSuccess)
{
    Console.WriteLine($"{details.Value.DisplayName} {details.Value.UpdateVersion} ({details.Value.MainFile})");
    Console.WriteLine($"Version ID: {details.Value.Custom?.UpdateId}");
    Console.WriteLine($"Deployment entry: {details.Value.Custom?.CatalogEntryId}");
}
```

See [GetApplicationDetailsAsync](../sdk/applications.md#getapplicationdetailsasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcCustomApplication -ProductId '{product-id}'
```

See [Get-PmpcCustomApplication](../powershell/get-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Search the Patch My PC catalog

The legacy `/apps/search` route is for custom applications. Public catalog results come from `/apps/public/search`. A public catalog search is scoped to one of your connections, so you choose a connection first. Public search results omit `updateId` from JSON (the SDK's nullable property reads as `null`); use the `catalogEntryId` values in public details to select a deployment.

1. List your connections and note the `connectionId` of the one you want. A PAT needs the `appcatbroker:apps:read` scope to list connections.
2. Search the catalog with that connection.
3. To search macOS applications, set the operating system to `MacOS`. If your account isn't entitled to macOS applications, the search returns no results and a details lookup reports the application as not found.

{% tabs %}
{% tab title="C#" %}
Select a connection once. The SDK uses the selected connection when you don't set `ConnectionId` on the request. This search returns one page; set `Skip` and `Limit` on `ProductFilterRequest` to page through additional results as described above.

{% code title="Program.cs" %}
```csharp
using PatchMyPC.Cloud.Client;

var connections = await client.GetAvailableConnectionsAsync();
if (connections.IsFailure)
{
    Console.WriteLine($"{connections.Error.Code}: {connections.Error.Message}");
    return;
}

await client.SetSelectedConnectionAsync(connections.Value[0]);

var results = await client.SearchPublicApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "7-Zip",
    OsType = OSType.Windows,
    Skip = 0,
    Limit = 25
});
```
{% endcode %}

See [GetAvailableConnectionsAsync](../sdk/customer-and-connections.md#getavailableconnectionsasync), [SetSelectedConnectionAsync](../sdk/customer-and-connections.md#setselectedconnectionasync), and [SearchPublicApplicationsAsync](../sdk/applications.md#searchpublicapplicationsasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcConnection
Set-PmpcConnection -Name '{connection-name}'
Find-PmpcApplication -DisplayName '7-Zip' -OsType Windows -Limit 25
```

`Find-PmpcApplication` uses the selected connection unless you pass `-ConnectionId`.

See [Get-PmpcConnection](../powershell/get-pmpcconnection.md), [Set-PmpcConnection](../powershell/set-pmpcconnection.md), and [Find-PmpcApplication](../powershell/find-pmpcapplication.md).
{% endtab %}
{% endtabs %}

If you don't know the vendor ID, search by application name and check the publisher in the results.

## Get the details of a catalog application

1. Use the product ID from a catalog search result and the same connection.
2. Optionally, set the operating system. It defaults to Windows.

The details of a catalog application include its descriptive information—for example the vendor, version, and links—but not packaging details, which Patch My PC maintains for you.

{% tabs %}
{% tab title="C#" %}
```csharp
var app = await client.GetPublicApplicationDetailsAsync(productId, connectionId: null, osType: OSType.Windows);
if (app.IsSuccess)
{
    foreach (var variant in app.Value.Variants)
    {
        Console.WriteLine($"{variant.ProductId} / {variant.CatalogEntryId}: {variant.Architecture} {variant.InstallerType} {variant.Language}");
    }
}
```

Passing `null` for `connectionId` uses the selected connection.

See [GetPublicApplicationDetailsAsync](../sdk/applications.md#getpublicapplicationdetailsasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcApplication -ProductId '{product-id}' -OsType Windows
```

See [Get-PmpcApplication](../powershell/get-pmpcapplication.md).
{% endtab %}
{% endtabs %}

## Read custom version IDs

Read `custom.updateId` from your custom search result and use it to [publish a new version](update-an-application.md#step-1-find-the-application-and-its-current-version).

```csharp
var customResults = await client.SearchApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "Contoso Sample Agent",
    Limit = 25
});

if (customResults.IsFailure)
{
    Console.WriteLine($"Search failed: {customResults.Error.Code} {customResults.Error.Message}");
    return;
}

foreach (var result in customResults.Value.Products)
{
    Console.WriteLine($"{result.DisplayName}: {result.Custom?.UpdateId}");
}
```

## Check public search and detail IDs

Public search results omit `updateId` from JSON. The nullable SDK property therefore reads as `null`:

```csharp
var publicResults = await client.SearchPublicApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "7-Zip",
    OsType = OSType.Windows,
    Limit = 25
});

if (publicResults.IsFailure)
{
    Console.WriteLine($"Search failed: {publicResults.Error.Code} {publicResults.Error.Message}");
    return;
}

foreach (var result in publicResults.Value.Products)
{
    Console.WriteLine(result.UpdateId is null ? $"{result.DisplayName}: no updateId" : $"{result.DisplayName}: {result.UpdateId}");
}
```

Use a public detail response to choose the installer you want. For deployment, take both `productId` and `catalogEntryId` from that same variant:

```csharp
var publicDetails = await client.GetPublicApplicationDetailsAsync(productId, connectionId: null, osType: OSType.Windows);
if (publicDetails.IsFailure)
{
    Console.WriteLine($"Details failed: {publicDetails.Error.Code} {publicDetails.Error.Message}");
    return;
}

foreach (var variant in publicDetails.Value.Variants)
{
    Console.WriteLine($"Product {variant.ProductId}; catalog entry {variant.CatalogEntryId}");
}
```

## Related pages

* [Create a custom application](create-a-custom-application.md)
* [Update an application](update-an-application.md)
* [Deploy an application](deploy-an-application.md)
* [Rate limits](../rate-limits.md)

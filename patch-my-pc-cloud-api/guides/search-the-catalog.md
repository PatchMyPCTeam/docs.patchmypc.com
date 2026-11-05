---
description: >-
  Find your own custom applications and applications in the Patch My PC catalog,
  and read their details, with the Patch My PC Cloud Customer API.
noIndex: true
noRobotsIndex: true
---

# Search the catalog

Use the Patch My PC Cloud Customer API to find applications and read their details. There are two catalogs:

* **Your custom applications**—the applications your company created and uploaded.
* **The Patch My PC catalog**—the public catalog of applications that Patch My PC packages and maintains for you. Searching it is scoped to one of your connections.

You need the product ID from a search result to read details, publish a new version, or create a deployment.

## Before you begin

* Exchange a personal access token (PAT) for an access token. See [Authentication](../authentication.md).
* The REST examples use the US host, `https://us.portal.patchmypc.com`. If your account is hosted in the EU, use `https://eu.portal.patchmypc.com` instead.
* A PAT needs the `appcatbroker:apps:read` scope.

## Search your custom applications

1. Send a search with the text to match against the display name. Every filter is optional; for example, you can also filter by language, architecture, or the date an application was last updated.
2. Page through the results with `skip` and `limit`. A page returns up to 50 applications by default.
3. Note the `productId` and `updateId` of the application you want. You need the `updateId` to publish a new version.

{% tabs %}
{% tab title="REST" %}
```http
POST https://us.portal.patchmypc.com/v1/api/apps/search
Authorization: Bearer {access-token}
Content-Type: application/json

{
  "displayNameSearchString": "Contoso",
  "skip": 0,
  "limit": 25,
  "sortField": "DisplayName",
  "ascending": true
}
```

The response contains one page of results and the total number of matches:

```json
{
  "totalAmount": 1,
  "products": [
    {
      "productId": "{product-id}",
      "updateId": "{update-id}",
      "displayName": "Contoso Agent",
      "vendorName": "Contoso",
      "version": "4.2.0",
      "state": "SuccessfullyCompleted",
      "actions": ["deploy", "update", "edit", "delete", "download-files"]
    }
  ]
}
```

A search is a read operation even though it uses `POST`. See [Rate limits](../rate-limits.md).

See [Search applications](../rest-api/applications.md#search-applications).
{% endtab %}

{% tab title="C#" %}
{% code title="Program.cs" %}
```csharp
using pmpc.appcatbroker.client;

var search = await broker.SearchApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "Contoso",
    Skip = 0,
    Limit = 25
});

if (search.IsFailure)
{
    Console.WriteLine($"{search.Error.Code}: {search.Error.Message}");
    return;
}

Console.WriteLine($"{search.Value.TotalAmount} match(es)");
foreach (var app in search.Value.Products)
{
    Console.WriteLine($"{app.DisplayName} {app.Version}  product: {app.ProductId}  update: {app.UpdateId}");
}
```
{% endcode %}

See [SearchApplicationsAsync](../sdk/applications.md#searchapplicationsasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Find-PmpcCustomApplication -DisplayName 'Contoso' -Limit 25 |
    Select-Object DisplayName, Version, ProductId, UpdateId
```

`Find-PmpcCustomApplication` uses an operation that must be enabled for your account. Until it is, the cmdlet reports the error code `FEATURE_NOT_ENABLED`.

See [Find-PmpcCustomApplication](../powershell/find-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Get the details of a custom application

1. Use the product ID from a search result to read the application's details, including its current version, installer, install arguments, and detection rules.

{% tabs %}
{% tab title="REST" %}
```http
GET https://us.portal.patchmypc.com/v1/api/apps/{product-id}
Authorization: Bearer {access-token}
Accept: application/json
```

If no application with that ID exists in your company, the response is `404 Not Found`.

See [Get application details](../rest-api/applications.md#get-application-details).
{% endtab %}

{% tab title="C#" %}
```csharp
var details = await broker.GetApplicationDetailsAsync(productId);
if (details.IsSuccess)
{
    Console.WriteLine($"{details.Value.DisplayName} {details.Value.UpdateVersion} ({details.Value.MainFile})");
}
```

See [GetApplicationDetailsAsync](../sdk/applications.md#getapplicationdetailsasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcCustomApplication -ProductId '{product-id}'
```

Like `Find-PmpcCustomApplication`, this cmdlet reports `FEATURE_NOT_ENABLED` until the operation is enabled for your account.

See [Get-PmpcCustomApplication](../powershell/get-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Search the Patch My PC catalog

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

A search of the Patch My PC catalog is scoped to one of your connections, so you choose a connection first.

1. List your connections and note the `connectionId` of the one you want. A PAT needs the `appcatbroker:apps:read` scope to list connections.
2. Search the catalog with that connection.
3. To search macOS applications, set the operating system to `MacOS`. macOS applications must be enabled for your account; otherwise a macOS search returns no results, and a details lookup reports the application as not found.

{% tabs %}
{% tab title="REST" %}
1) List your connections.

```http
GET https://us.portal.patchmypc.com/v1/api/connections
Authorization: Bearer {access-token}
Accept: application/json
```

2. Search, passing the `connectionId`. It's required for this operation.

```http
POST https://us.portal.patchmypc.com/v1/api/apps/public/search
Authorization: Bearer {access-token}
Content-Type: application/json

{
  "connectionId": "{connection-id}",
  "displayNameSearchString": "7-Zip",
  "osType": "Windows",
  "limit": 25
}
```

See [Get available connections](../rest-api/applications.md#get-available-connections) and [Search public applications](../rest-api/applications.md#search-public-applications).
{% endtab %}

{% tab title="C#" %}
Select a connection once. The SDK uses the selected connection when you don't set `ConnectionId` on the request.

{% code title="Program.cs" %}
```csharp
var connections = await broker.GetAvailableConnectionsAsync();
if (connections.IsFailure)
{
    Console.WriteLine($"{connections.Error.Code}: {connections.Error.Message}");
    return;
}

await broker.SetSelectedConnectionAsync(connections.Value[0]);

var results = await broker.SearchPublicApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "7-Zip",
    OsType = OSType.Windows,
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

## Get the details of a catalog application

1. Use the product ID from a catalog search result and the same connection.
2. Optionally, set the operating system. It defaults to Windows.

The details of a catalog application include its descriptive information—for example the vendor, version, and links—but not packaging details, which Patch My PC maintains for you.

{% tabs %}
{% tab title="REST" %}
```http
GET https://us.portal.patchmypc.com/v1/api/apps/public/{product-id}?connectionId={connection-id}&osType=Windows
Authorization: Bearer {access-token}
Accept: application/json
```

See [Get public application details](../rest-api/applications.md#get-public-application-details).
{% endtab %}

{% tab title="C#" %}
```csharp
var app = await broker.GetPublicApplicationDetailsAsync(productId, connectionId: null, osType: OSType.Windows);
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

## Related pages

* [Create a custom application](create-a-custom-application.md)
* [Update an application](update-an-application.md)
* [Deploy an application](deploy-an-application.md)
* [Rate limits](../rate-limits.md)

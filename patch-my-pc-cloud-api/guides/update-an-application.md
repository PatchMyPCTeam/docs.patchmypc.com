---
description: >-
  Publish a new version of one of your custom applications with the Patch My PC
  Cloud Customer API.
noIndex: true
noRobotsIndex: true
---

# Update an application

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

When a vendor releases a new version of an application you packaged yourself, you publish it as an update to the existing custom application. The application keeps its product ID, and the new version gets its own update ID.

An update replaces the application's files and packaging details—for example the installer, install arguments, and detection. The application's descriptive details, such as its display name and publisher, stay the same.

Like creating an application, an update uploads files. The .NET SDK and the PowerShell module do the upload for you, so we recommend them over REST.

## Before you begin

* Exchange a personal access token (PAT) for an access token. See [Authentication](../authentication.md).
* The REST examples use the US host, `https://us.portal.patchmypc.com`. Use `https://eu.portal.patchmypc.com` for EU accounts or `https://uk.portal.patchmypc.com` for UK accounts.
* A PAT needs the `appcatbroker:apps:write` scope, and `appcatbroker:apps:read` to look up the application.
* Prepare a folder with the new version's installer and supporting files, as described in [Create a custom application](create-a-custom-application.md).

## Step 1: Find the application and its current version

1. Search for the application.
2. Note its `productId` and its `updateId`. The `updateId` identifies the current version, which the new version follows.

{% tabs %}
{% tab title="REST" %}
```http
POST https://us.portal.patchmypc.com/v1/api/apps/search
Authorization: Bearer {access-token}
Content-Type: application/json

{
  "displayNameSearchString": "Contoso Sample Agent"
}
```

Each result in `products` has a `productId` and an `updateId`.

See [Search applications](../rest-api/applications.md#search-applications).
{% endtab %}

{% tab title="C#" %}
```csharp
var search = await client.SearchApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "Contoso Sample Agent"
});

var current = search.Value.Products.First();
```

See [SearchApplicationsAsync](../sdk/applications.md#searchapplicationsasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
$current = Find-PmpcCustomApplication -DisplayName 'Contoso Sample Agent' | Select-Object -First 1
$current | Select-Object DisplayName, Version, ProductId, UpdateId
```

See [Find-PmpcCustomApplication](../powershell/find-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Step 2: Publish the new version

{% tabs %}
{% tab title="REST" %}
1. Create an update draft for the application's current version.

```http
POST https://us.portal.patchmypc.com/v1/api/apps/update-draft
Authorization: Bearer {access-token}
Content-Type: application/json

{
  "productId": "{product-id}",
  "updateId": "{current-update-id}"
}
```

The response has the same shape as a new draft: the same `productId`, a new `updateId` and `revisionId`, and the paths to upload files to.

2. Upload the new version's files to those paths. The upload works the same way as for a new application—see [Create a custom application](create-a-custom-application.md).
3. Complete the update with `PUT`. Send the IDs from the update draft, the packaging details, and the list of files.

```http
PUT https://us.portal.patchmypc.com/v1/api/apps/complete
Authorization: Bearer {access-token}
Content-Type: application/json

{
  "productId": "{product-id}",
  "updateId": "{new-update-id}",
  "revisionId": 123,
  "primaryInstallerFile": "ContosoAgent.msi",
  "msiProductCode": "{msi-product-code}",
  "files": [
    {
      "productId": "{product-id}",
      "fileName": "ContosoAgent.msi",
      "fileSize": 53477376,
      "fileType": "{file-type}",
      "sha1Hash": "{sha1-hash}",
      "sha256Hash": "{sha256-hash}"
    }
  ]
}
```

If the application or draft doesn't exist, the response is `404 Not Found`. Completing an update can take up to a minute.

See [Create update draft](../rest-api/applications.md#create-update-draft) and [Complete application update](../rest-api/applications.md#complete-application-update).
{% endtab %}

{% tab title="C#" %}
{% code title="Program.cs" %}
```csharp
var updated = await client.UpdateApplicationAsync(new ApplicationUpdateMetadata
{
    ProductId = current.ProductId,
    UpdateId = current.UpdateId,
    FolderPath = @"C:\Packages\ContosoAgent-4.3",
    PrimaryInstallerFile = "ContosoAgent.msi",
    MsiProductCode = Guid.Parse("{msi-product-code}"),
    CmdArguments = "/qn",
    ArpVersionMatch = "{version}"
});

if (updated.IsFailure)
{
    Console.WriteLine($"{updated.Error.Code}: {updated.Error.Message}");
    return;
}

Console.WriteLine($"New version {updated.Value.UpdateId} of product {updated.Value.ProductId}");
```
{% endcode %}

You can pass an `IProgress<UploadProgress>` to report upload progress, as when creating an application.

See [UpdateApplicationAsync](../sdk/applications.md#updateapplicationasync).
{% endtab %}

{% tab title="PowerShell" %}
Use the product and update IDs returned by `Get-PmpcCustomApplication` or `Find-PmpcCustomApplication`. Provide the new version with `-ArpVersionMatch`. For an MSI installer, also provide the new installer's product code; the installer type cannot change between versions.

```powershell
Update-PmpcCustomApplication -ProductId '{product-id}' -UpdateId '{update-id}' -FolderPath 'C:\Packages\ContosoAgent-4.3' -PrimaryInstallerFile 'ContosoAgent.msi' -MsiProductCode '{msi-product-code}' -CmdArguments '/qn' -ArpVersionMatch '{version}'
```

The cmdlets in this example use operations that must be enabled for your account. Until they are, they report the error code `FEATURE_NOT_ENABLED`.

See [Update-PmpcCustomApplication](../powershell/update-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Step 3: Roll out the new version to an existing deployment

If the application is already deployed, sync the deployment to move it to the latest pending version instead of waiting for its scheduled sync. Deployments belong to a connection, so select the connection first—see [Deploy an application](deploy-an-application.md).

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

1. List the application's deployments and note the `deploymentId` of the one to update.
2. Sync that deployment.

{% tabs %}
{% tab title="REST" %}
```http
PUT https://us.portal.patchmypc.com/v1/api/apps/{product-id}/deployments/{deployment-id}/sync?connectionId={connection-id}
Authorization: Bearer {access-token}
```

A PAT needs the `appcatbroker:apps:deploy` scope. See [Sync application deployment](../rest-api/applications.md#sync-application-deployment).
{% endtab %}

{% tab title="C#" %}
```csharp
var sync = await client.SyncDeploymentAsync(current.ProductId, "{deployment-id}");
if (sync.IsFailure)
{
    Console.WriteLine($"{sync.Error.Code}: {sync.Error.Message}");
}
```

See [SyncDeploymentAsync](../sdk/deployments.md#syncdeploymentasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcDeployment -ProductId $current.ProductId
Sync-PmpcDeployment -ProductId $current.ProductId -DeploymentId '{deployment-id}'
```

See [Sync-PmpcDeployment](../powershell/sync-pmpcdeployment.md).
{% endtab %}
{% endtabs %}

## Related pages

* [Create a custom application](create-a-custom-application.md)
* [Search the catalog](search-the-catalog.md)
* [Deploy an application](deploy-an-application.md)

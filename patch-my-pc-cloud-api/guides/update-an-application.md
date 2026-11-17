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

This guide covers the SDK and PowerShell module. For REST, see [Create update draft](https://docs.patchmypc.com/patch-my-pc-cloud-api/rest-api/applications#create-update-draft), [Complete application update](https://docs.patchmypc.com/patch-my-pc-cloud-api/rest-api/applications#complete-application-update), and [Sync application deployment](https://docs.patchmypc.com/patch-my-pc-cloud-api/rest-api/applications#sync-application-deployment). The separate [REST walkthrough](https://docs.patchmypc.com/patch-my-pc-cloud-api/guides/create-a-custom-application-with-rest) demonstrates creating and deploying an application, not publishing a new version.

## Before you begin

* Exchange a personal access token (PAT) for an access token. See [Authentication](../authentication.md).
* A PAT needs the `appcatbroker:apps:write` scope, and `appcatbroker:apps:read` to look up the application.
* Prepare a folder with the new version's installer and supporting files, as described in [Create a custom application](create-a-custom-application.md).

## Step 1: Find the application and its current version

1. Search for the application.
2. Note its `productId` and `custom.updateId`. `custom.updateId` is the canonical ID of the current version, which the new version follows. The deprecated top-level `updateId` is retained only for compatibility.

{% tabs %}
{% tab title="C#" %}
{% code collapsedlinecount="10" %}
```csharp
var search = await client.SearchApplicationsAsync(new ProductFilterRequest
{
    DisplayNameSearchString = "Contoso Sample Agent"
});

var current = search.Value.Products.First();
```
{% endcode %}

See [SearchApplicationsAsync](../sdk/applications.md#searchapplicationsasync).
{% endtab %}

{% tab title="PowerShell" %}
{% code collapsedlinecount="10" %}
```powershell
$current = Find-PmpcCustomApplication -DisplayName 'Contoso Sample Agent' | Select-Object -First 1
$current | Select-Object DisplayName, Version, ProductId, @{ Name = 'UpdateId'; Expression = { $_.Custom.UpdateId } }
```
{% endcode %}

See [Find-PmpcCustomApplication](../powershell/find-pmpccustomapplication.md).
{% endtab %}
{% endtabs %}

## Step 2: Publish the new version

{% tabs %}
{% tab title="C#" %}
{% code title="Program.cs" collapsedlinecount="10" %}
```csharp
var updated = await client.UpdateApplicationAsync(new ApplicationUpdateMetadata
{
    ProductId = current.ProductId,
    UpdateId = current.Custom!.UpdateId,
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

{% code collapsedlinecount="10" %}
```powershell
Update-PmpcCustomApplication -ProductId '{product-id}' -UpdateId '{update-id}' -FolderPath 'C:\Packages\ContosoAgent-4.3' -PrimaryInstallerFile 'ContosoAgent.msi' -MsiProductCode '{msi-product-code}' -CmdArguments '/qn' -ArpVersionMatch '{version}'
```
{% endcode %}

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
{% tab title="C#" %}
{% code collapsedlinecount="10" %}
```csharp
var sync = await client.SyncDeploymentAsync(current.ProductId, "{deployment-id}");
if (sync.IsFailure)
{
    Console.WriteLine($"{sync.Error.Code}: {sync.Error.Message}");
}
```
{% endcode %}

See [SyncDeploymentAsync](../sdk/deployments.md#syncdeploymentasync).
{% endtab %}

{% tab title="PowerShell" %}
{% code collapsedlinecount="10" %}
```powershell
Get-PmpcDeployment -ProductId $current.ProductId
Sync-PmpcDeployment -ProductId $current.ProductId -DeploymentId '{deployment-id}'
```
{% endcode %}

See [Sync-PmpcDeployment](../powershell/sync-pmpcdeployment.md).
{% endtab %}
{% endtabs %}

## Related pages

* [Create a custom application](create-a-custom-application.md)
* [Search the catalog](search-the-catalog.md)
* [Deploy an application](deploy-an-application.md)

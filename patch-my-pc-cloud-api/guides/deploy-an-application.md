---
description: >-
  Deploy an application to Microsoft Intune through one of your connections with
  the Patch My PC Cloud Customer API.
noIndex: true
noRobotsIndex: true
---

# Deploy an application

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

A deployment publishes an application to Microsoft Intune through one of your company's connections and assigns it to groups of users or devices. You can deploy catalog applications and your own custom applications.

This guide covers the SDK and PowerShell module. For direct HTTP requests, follow [Create and deploy a custom application with REST](https://docs.patchmypc.com/patch-my-pc-cloud-api/guides/create-a-custom-application-with-rest). For other deployment operations, see the [REST API reference](https://docs.patchmypc.com/patch-my-pc-cloud-api/rest-api).

## Before you begin

* Exchange a personal access token (PAT) for an access token. See [Authentication](../authentication.md).
* A PAT needs the `appcatbroker:apps:read` scope to list connections and the `appcatbroker:apps:deploy` scope to create and read deployments.
* Find the product ID of the application to deploy. See [Search the catalog](search-the-catalog.md). A deployment also requires a catalog entry ID: use `custom.catalogEntryId` from custom application details, or choose one public variant and use its `catalogEntryId`.
* Have the object IDs of the Microsoft Entra ID groups you want to assign the application to.

## Step 1: Select a connection

Every deployment belongs to a connection. With the SDK and the PowerShell module, you select a connection once and later deployment calls use it.

1. List your connections.
2. Choose an Intune connection whose `adminConsent` is `Granted`.
3. Note its `connectionId`, or select it.

{% tabs %}
{% tab title="C#" %}
{% code collapsedlinecount="10" %}
```csharp
var connections = await client.GetAvailableConnectionsAsync();
if (connections.IsFailure)
{
    Console.WriteLine($"{connections.Error.Code}: {connections.Error.Message}");
    return;
}

var connection = connections.Value.First(c => c.DisplayName == "Contoso Intune");
await client.SetSelectedConnectionAsync(connection);
```
{% endcode %}

See [GetAvailableConnectionsAsync](../sdk/customer-and-connections.md#getavailableconnectionsasync) and [SetSelectedConnectionAsync](../sdk/customer-and-connections.md#setselectedconnectionasync).
{% endtab %}

{% tab title="PowerShell" %}
{% code collapsedlinecount="10" %}
```powershell
Get-PmpcConnection
Set-PmpcConnection -Name 'Contoso Intune'
```
{% endcode %}

See [Get-PmpcConnection](../powershell/get-pmpcconnection.md) and [Set-PmpcConnection](../powershell/set-pmpcconnection.md).
{% endtab %}
{% endtabs %}

## Step 2: Plan the assignments

Each assignment pairs an installation intent with a target. Choose one or more:

| Target                              | Intents                                                                             | Group ID      |
| ----------------------------------- | ----------------------------------------------------------------------------------- | ------------- |
| A group (the default)               | `Required`, `Available`, `Uninstall`, or `UpdateOnly`                               | Required      |
| A group (the default)               | `AvailableWithoutEnrollment`                                                        | Optional      |
| `AllUsers` or `AllDevices`          | `Required`, `Available`, `Uninstall`, `UpdateOnly`, or `AvailableWithoutEnrollment` | Must be empty |
| None (`NotSet`, or omit the target) | `NoAssignmentsInstall` or `NoAssignmentsUpdate`                                     | Must be empty |

The `NoAssignmentsInstall` and `NoAssignmentsUpdate` intents publish the application to Intune without assigning it to anyone. A combination that isn't in the table is rejected with `400 Bad Request`.

## Step 3: Create the deployment

1. Choose the exact catalog entry. For a custom application, read its details and use `custom.catalogEntryId`. For a public application, read public details for the operating system and choose one item from `variants`.
2. Send the product ID, required catalog entry ID, operating system, and assignments.
3. Optionally, add category IDs, Enrollment Status Page profile IDs, deployments this one depends on, and configuration settings.
4. Note the `deploymentId` in the response.

{% tabs %}
{% tab title="C#" %}
{% code title="Program.cs" collapsedlinecount="10" %}
```csharp
using PatchMyPC.Cloud.Client;

var details = await client.GetCustomApplicationDetailsAsync(productId);
if (details.IsFailure || details.Value.Custom?.CatalogEntryId is not Guid catalogEntryId)
{
    Console.WriteLine("Couldn't find a deployment entry for the custom application.");
    return;
}

var created = await client.CreateDeploymentAsync(productId, new CreateDeploymentRequest
{
    CatalogEntryId = catalogEntryId,
    OsType = OSType.Windows,
    Assignments = new List<CreateDeploymentAssignmentRequest>
    {
        new CreateDeploymentAssignmentRequest
        {
            GroupId = "{group-id}",
            Intent = InstallationIntent.Required
        }
    }
});

if (created.IsFailure)
{
    Console.WriteLine($"{created.Error.Code}: {created.Error.Message}");
    return;
}

Console.WriteLine($"Created {created.Value.DeploymentId} ({created.Value.Status})");
```
{% endcode %}

The SDK uses the selected connection and ignores any `ConnectionId` you set on the request.

See [CreateDeploymentAsync](../sdk/deployments.md#createdeploymentasync).
{% endtab %}

{% tab title="PowerShell" %}
{% code collapsedlinecount="10" %}
```powershell
$assignments = @(
    New-PmpcDeploymentAssignment -GroupId '{group-id}' -Intent Required
)

$app = Get-PmpcCustomApplication -ProductId '{product-id}'
$deployment = New-PmpcDeployment -ProductId $app.ProductId -CatalogEntryId $app.Custom.CatalogEntryId -OsType Windows -Assignment $assignments
[pscustomobject]@{
    ProductId = $app.ProductId
    DeploymentId = $deployment.DeploymentId
}
```
{% endcode %}

`New-PmpcDeployment` supports `-WhatIf` and `-Confirm`. `-CatalogEntryId` is required; get it from custom details or from one selected public variant. `ProductId` and `UpdateId` are not substitutes.

See [New-PmpcDeploymentAssignment](../powershell/new-pmpcdeploymentassignment.md) and [New-PmpcDeployment](../powershell/new-pmpcdeployment.md).
{% endtab %}
{% endtabs %}

### Create a deployment for a selected public variant

Select the exact variant from public application details and pass its `CatalogEntryId` in the create request. The product ID alone does not identify which catalog entry to deploy.

{% code collapsedlinecount="10" %}
```csharp
var publicDetails = await client.GetPublicApplicationDetailsAsync(productId, connectionId: null, osType: OSType.Windows);
if (publicDetails.IsFailure)
{
    Console.WriteLine($"Could not load public application details: {publicDetails.Error.Code} {publicDetails.Error.Message}");
    return;
}

var matchingVariants = publicDetails.Value.Variants
    .Where(variant =>
        variant.Architecture == RequirementArchitecture.X64 &&
        variant.InstallerType == InstallerType.MSI &&
        variant.InstallContext == InstallationBehavior.System &&
        variant.Language == "en-US")
    .ToList();

if (matchingVariants.Count != 1)
{
    Console.WriteLine($"Expected one x64, MSI, system, en-US variant; found {matchingVariants.Count}. Choose your intended variant explicitly.");
    return;
}

var selectedVariant = matchingVariants[0];
var deployment = await client.CreateDeploymentAsync(selectedVariant.ProductId, new CreateDeploymentRequest
{
    CatalogEntryId = selectedVariant.CatalogEntryId,
    OsType = OSType.Windows,
    Assignments = new List<CreateDeploymentAssignmentRequest>
    {
        new CreateDeploymentAssignmentRequest
        {
            GroupId = "{group-id}",
            Intent = InstallationIntent.Required
        }
    }
});

if (deployment.IsFailure)
{
    Console.WriteLine($"Deployment failed: {deployment.Error.Code} {deployment.Error.Message}");
    return;
}

Console.WriteLine($"Created {deployment.Value.DeploymentId}");
```
{% endcode %}

## Step 4: Monitor the deployment

A new deployment is processed in the background. Check its status until it settles.

1. Read the deployment's details.
2. Check `status`. `InProgress`, `Retrying`, and `Scheduled` mean work is still pending; `Success` and `Failed` are final.
3. Review `warningMessages` and `errorMessages`. A deployment can succeed and still carry warnings.

{% tabs %}
{% tab title="C#" %}
{% code collapsedlinecount="10" %}
```csharp
var details = await client.GetDeploymentDetailsAsync(productId, created.Value.DeploymentId);
if (details.IsSuccess)
{
    Console.WriteLine($"Status: {details.Value.Status}");
    foreach (var warning in details.Value.WarningMessages ?? Enumerable.Empty<string>())
    {
        Console.WriteLine($"Warning: {warning}");
    }
}
```
{% endcode %}

See [GetDeploymentDetailsAsync](../sdk/deployments.md#getdeploymentdetailsasync) and [GetDeploymentsAsync](../sdk/deployments.md#getdeploymentsasync).
{% endtab %}

{% tab title="PowerShell" %}
{% code collapsedlinecount="10" %}
```powershell
Get-PmpcDeployment -ProductId '{product-id}' -DeploymentId '{deployment-id}' |
    Select-Object DisplayName, Status, WarningMessages, ErrorMessages
```
{% endcode %}

To list every deployment of the application, omit `-DeploymentId`.

See [Get-PmpcDeployment](../powershell/get-pmpcdeployment.md).
{% endtab %}
{% endtabs %}

## Related pages

* [Update an application](update-an-application.md)
* [Search the catalog](search-the-catalog.md)
* [Deployments](../sdk/deployments.md)
* [Rate limits](../rate-limits.md)

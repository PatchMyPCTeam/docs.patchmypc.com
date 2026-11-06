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

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

## Before you begin

* Exchange a personal access token (PAT) for an access token. See [Authentication](../authentication.md).
* The REST examples use the US host, `https://us.portal.patchmypc.com`. If your account is hosted in the EU, use `https://eu.portal.patchmypc.com` instead.
* A PAT needs the `appcatbroker:apps:read` scope to list connections and the `appcatbroker:apps:deploy` scope to create and read deployments.
* Find the product ID of the application to deploy. See [Search the catalog](search-the-catalog.md).
* Have the object IDs of the Microsoft Entra ID groups you want to assign the application to.

## Step 1: Select a connection

Every deployment belongs to a connection. With the SDK and the PowerShell module, you select a connection once and later deployment calls use it. With REST, you pass the connection ID on each deployment request.

1. List your connections.
2. Choose an Intune connection whose `adminConsent` is `Granted`.
3. Note its `connectionId`, or select it.

{% tabs %}
{% tab title="REST" %}
```http
GET https://us.portal.patchmypc.com/v1/api/connections
Authorization: Bearer {access-token}
Accept: application/json
```

```json
[
  {
    "connectionId": "{connection-id}",
    "displayName": "Contoso Intune",
    "type": "Intune",
    "adminConsent": "Granted"
  }
]
```

See [Get available connections](../rest-api/applications.md#get-available-connections).
{% endtab %}

{% tab title="C#" %}
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

See [GetAvailableConnectionsAsync](../sdk/customer-and-connections.md#getavailableconnectionsasync) and [SetSelectedConnectionAsync](../sdk/customer-and-connections.md#setselectedconnectionasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcConnection
Set-PmpcConnection -Name 'Contoso Intune'
```

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

1. Send the operating system and the assignments.
2. Optionally, add category IDs, Enrollment Status Page profile IDs, deployments this one depends on, and configuration settings.
3. Note the `deploymentId` in the response.

{% tabs %}
{% tab title="REST" %}
```http
POST https://us.portal.patchmypc.com/v1/api/apps/{product-id}/deployments
Authorization: Bearer {access-token}
Content-Type: application/json

{
  "connectionId": "{connection-id}",
  "osType": "Windows",
  "assignments": [
    { "groupId": "{group-id}", "intent": "Required" },
    { "targetType": "AllUsers", "intent": "Available" }
  ]
}
```

The response describes the new deployment, including its `deploymentId` and `status`.

See [Create application deployment](../rest-api/applications.md#create-application-deployment).
{% endtab %}

{% tab title="C#" %}
{% code title="Program.cs" %}
```csharp
using pmpc.appcatbroker.client;

var created = await client.CreateDeploymentAsync(productId, new CreateDeploymentRequest
{
    OsType = OSType.Windows,
    Assignments = new List<CreateDeploymentAssignmentRequest>
    {
        new CreateDeploymentAssignmentRequest
        {
            GroupId = "{group-id}",
            Intent = InstallationIntent.Required
        },
        new CreateDeploymentAssignmentRequest
        {
            TargetType = AssignmentTargetType.AllUsers,
            Intent = InstallationIntent.Available
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
```powershell
$assignments = @(
    New-PmpcDeploymentAssignment -GroupId '{group-id}' -Intent Required
    New-PmpcDeploymentAssignment -TargetType AllUsers -Intent Available
)

$deployment = New-PmpcDeployment -ProductId '{product-id}' -OsType Windows -Assignment $assignments
$deployment.DeploymentId
```

`New-PmpcDeployment` supports `-WhatIf` and `-Confirm`.

See [New-PmpcDeploymentAssignment](../powershell/new-pmpcdeploymentassignment.md) and [New-PmpcDeployment](../powershell/new-pmpcdeployment.md).
{% endtab %}
{% endtabs %}

## Step 4: Monitor the deployment

A new deployment is processed in the background. Check its status until it settles.

1. Read the deployment's details.
2. Check `status`. `InProgress`, `Retrying`, and `Scheduled` mean work is still pending; `Success` and `Failed` are final.
3. Review `warningMessages` and `errorMessages`. A deployment can succeed and still carry warnings.

{% tabs %}
{% tab title="REST" %}
```http
GET https://us.portal.patchmypc.com/v1/api/apps/{product-id}/deployments/{deployment-id}?connectionId={connection-id}
Authorization: Bearer {access-token}
Accept: application/json
```

To list every deployment of the application on the connection, omit the deployment ID: `GET /v1/api/apps/{product-id}/deployments?connectionId={connection-id}`.

See [Get application deployment details](../rest-api/applications.md#get-application-deployment-details) and [Get application deployments](../rest-api/applications.md#get-application-deployments).
{% endtab %}

{% tab title="C#" %}
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

See [GetDeploymentDetailsAsync](../sdk/deployments.md#getdeploymentdetailsasync) and [GetDeploymentsAsync](../sdk/deployments.md#getdeploymentsasync).
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcDeployment -ProductId '{product-id}' -DeploymentId $deployment.DeploymentId |
    Select-Object DisplayName, Status, WarningMessages, ErrorMessages
```

To list every deployment of the application, omit `-DeploymentId`.

See [Get-PmpcDeployment](../powershell/get-pmpcdeployment.md).
{% endtab %}
{% endtabs %}

## Related pages

* [Update an application](update-an-application.md)
* [Search the catalog](search-the-catalog.md)
* [Deployments](../sdk/deployments.md)
* [Rate limits](../rate-limits.md)

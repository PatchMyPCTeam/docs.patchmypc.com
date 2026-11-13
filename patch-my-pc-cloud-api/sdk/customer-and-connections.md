---
description: >-
  SDK methods for reading your account information and limits, and for listing
  and selecting connections.
noIndex: true
noRobotsIndex: true
---

# Customer information and connections

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

These methods read information about your Patch My PC account and manage the connection the SDK works with. A connection links your Patch My PC account to a Microsoft Intune tenant. Deployment, deployment template, and public catalog methods run against the selected connection, so select one before you call them.

All of these methods need an authenticated session. For details, see [SDK authentication methods](authentication.md).

## Models

### Customer information

`CustomerInfoDto` (namespace `PatchMyPC.Cloud.Client`) describes your account.

| Property                   | Type     | Description                                                                                                                     |
| -------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `CustomerId`               | `Guid`   | Your customer ID.                                                                                                               |
| `CustomerName`             | `string` | Your company name.                                                                                                              |
| `License`                  | object   | Your license details.                                                                                                           |
| `Limits`                   | object   | The limits that apply to your account, for example how many custom applications you can create.                                 |
| `LimitsProgress`           | object   | Your current usage against those limits.                                                                                        |
| `MacOSApplicationsEnabled` | `bool`   | `true` if your account is entitled to macOS applications. When it's `false`, searches for macOS applications return no results. |

### Connection

`ConnectionDto` (namespace `PatchMyPC.Cloud.Client`) describes one connection.

| Property       | Type      | Description                                                                                                                        |
| -------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `ConnectionId` | `Guid`    | The connection ID. Pass it wherever a method asks for a connection ID.                                                             |
| `DisplayName`  | `string?` | The connection's display name, if one is set.                                                                                      |
| `Type`         | enum      | The connection type. Only Intune connections are returned.                                                                         |
| `AdminConsent` | enum      | Whether an administrator has granted consent for the connection. Deployment operations fail on a connection without admin consent. |

## Methods

### GetCustomerInfoAsync

Gets your account information and usage limits.

```csharp
Task<Result<CustomerInfoDto>> GetCustomerInfoAsync(CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                 |
| ------------------- | ------------------- | --------------------------- |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call. |

**Returns:** a [`CustomerInfoDto`](customer-and-connections.md#customer-information) for your company.

The personal access token (PAT) needs the `appcatbroker:customer:read` scope.

```csharp
var info = await client.GetCustomerInfoAsync();
if (info.IsFailure)
{
    Console.WriteLine($"Couldn't read account information: {info.Error.Message}");
    return;
}

Console.WriteLine($"{info.Value.CustomerName} ({info.Value.CustomerId})");
Console.WriteLine($"macOS applications enabled: {info.Value.MacOSApplicationsEnabled}");
```

**See also:** [Get-PmpcCustomerInfo](../powershell/get-pmpccustomerinfo.md) and [Get customer info](../rest-api/applications.md#get-customer-info).

### GetAvailableConnectionsAsync

Lists the Intune connections for your company.

```csharp
Task<Result<IReadOnlyList<ConnectionDto>>> GetAvailableConnectionsAsync(CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                 |
| ------------------- | ------------------- | --------------------------- |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call. |

**Returns:** a list of [`ConnectionDto`](customer-and-connections.md#connection) objects. The list is empty if the company has no Intune connections.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

A PAT needs the `appcatbroker:apps:read` scope.

```csharp
var connections = await client.GetAvailableConnectionsAsync();
if (connections.IsFailure)
{
    Console.WriteLine($"Couldn't list connections: {connections.Error.Code} {connections.Error.Message}");
    return;
}

foreach (var connection in connections.Value)
{
    Console.WriteLine($"{connection.DisplayName} ({connection.ConnectionId}) consent: {connection.AdminConsent}");
}
```

**See also:** [Get-PmpcConnection](../powershell/get-pmpcconnection.md) and [Get available connections](../rest-api/applications.md#get-available-connections).

### SetSelectedConnectionAsync

Selects the connection that deployment, deployment template, and public catalog methods use.

```csharp
Task<Result> SetSelectedConnectionAsync(ConnectionDto selectedConnection);
```

| Parameter            | Type                                                      | Description                                                                  |
| -------------------- | --------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `selectedConnection` | [`ConnectionDto`](customer-and-connections.md#connection) | Required. One of the connections returned by `GetAvailableConnectionsAsync`. |

**Returns:** a `Result` that indicates success or failure. Passing `null` fails with `VALIDATION_ERROR`.

Selecting a connection doesn't change the session's company. The SDK applies the selected connection automatically to deployment create and edit requests, overwriting any connection ID you set on the request. Until you select a connection, deployment methods fail with `VALIDATION_ERROR` and the message "No connection selected. Please call SetSelectedConnectionAsync first."

```csharp
var connection = connections.Value.FirstOrDefault(c => c.DisplayName == "{connection-name}");
if (connection is null)
{
    Console.WriteLine("Connection not found.");
    return;
}

var select = await client.SetSelectedConnectionAsync(connection);
if (select.IsFailure)
{
    Console.WriteLine($"Couldn't select the connection: {select.Error.Message}");
    return;
}
```

**See also:** [Set-PmpcConnection](../powershell/set-pmpcconnection.md). This method has no REST operation; the selection is stored in the SDK.

### GetSelectedConnection

Returns the currently selected connection.

```csharp
ConnectionDto? GetSelectedConnection();
```

This method has no parameters.

**Returns:** the selected [`ConnectionDto`](customer-and-connections.md#connection), or `null` if no connection is selected. Unlike most methods, it returns the value directly rather than a result object.

```csharp
var current = client.GetSelectedConnection();
Console.WriteLine(current is null
    ? "No connection selected."
    : $"Using connection {current.DisplayName} ({current.ConnectionId})");
```

**See also:** [Get-PmpcSelectedConnection](../powershell/get-pmpcselectedconnection.md). This method has no REST operation; it reads the selection stored in the SDK.

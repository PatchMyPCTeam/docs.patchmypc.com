---
description: >-
  SDK methods for authenticating with a personal access token, reading the
  session's company, signing out, and checking service health.
noIndex: true
noRobotsIndex: true
---

# SDK authentication methods

These methods authenticate the SDK with the Patch My PC Cloud Customer API, report which company later calls run against, and sign you out.

The SDK authenticates with a personal access token (PAT). Call [`AuthenticateWithPersonalAccessTokenAsync`](authentication.md#authenticatewithpersonalaccesstokenasync) once, before any other method. It needs no user at the keyboard, so it suits services, scheduled jobs, and pipelines. You create the PAT in the Patch My PC portal; see [Create a personal access token](../create-a-personal-access-token.md).

Until you authenticate, most other methods fail with `VALIDATION_ERROR` because no company is selected. For an overview of how authentication works, see [Authentication](../authentication.md).

## Company model

`CompanyInfo` (namespace `pmpc.appcatbroker.sdk.Models`) identifies the company a session works with.

| Property      | Type                          | Description                                                                                  |
| ------------- | ----------------------------- | -------------------------------------------------------------------------------------------- |
| `CustomerId`  | `string`                      | The company's customer ID.                                                                   |
| `CompanyName` | `string`                      | The company's display name.                                                                  |
| `RegionId`    | `Guid`                        | The region the company's data is hosted in.                                                  |
| `RegionUrls`  | `IDictionary<string, string>` | The regional addresses the SDK uses for this company. You don't normally need to read these. |
| `Metadata`    | `Dictionary<string, object>?` | Additional information about the company, if any.                                            |

## Methods

### AuthenticateWithPersonalAccessTokenAsync

Authenticates with a personal access token and selects the token's company, so the SDK is ready to use in one step.

```csharp
Task<Result<CompanyInfo>> AuthenticateWithPersonalAccessTokenAsync(
    string personalAccessToken,
    CancellationToken cancellationToken = default);
```

| Parameter             | Type                | Description                                                          |
| --------------------- | ------------------- | -------------------------------------------------------------------- |
| `personalAccessToken` | `string`            | Required. The full token value, as shown when the token was created. |
| `cancellationToken`   | `CancellationToken` | Optional. Cancels the call.                                          |

**Returns:** the [`CompanyInfo`](authentication.md#company-model) of the company the token belongs to. Every later call runs against that company.

The SDK exchanges the PAT for an access token that's valid for 60 minutes, then exchanges the PAT again as the access token expires, so one authenticated `IAppCatBroker` instance works for a long-running job. Set `Region` (`Us` or `Eu`) in the SDK configuration so the SDK knows which regional service to authenticate with. For details, see [Install and configure the SDK](install-and-configure.md).

A PAT can only do what its scopes allow, and never more than the user who created it. The `appcatbroker:apps:deploy` scope covers both deployments and deployment templates. For the full list, see [Scopes](../authentication.md#scopes). Calls outside its scopes fail with `AUTHZ_ERROR`. Authentication itself can fail with these codes:

| Code                     | Meaning                                                           |
| ------------------------ | ----------------------------------------------------------------- |
| `AUTH_ERROR`             | The token is invalid, expired, or revoked.                        |
| `PAT_EXCHANGE_THROTTLED` | Too many token exchanges in a short time. Wait, then retry.       |
| `PAT_NOT_ENTITLED`       | The token's company isn't entitled to use personal access tokens. |

The usual pattern is to create a PAT once in the Patch My PC portal, store it in a secret store, and read it on every run:

```csharp
var token = Environment.GetEnvironmentVariable("PMPC_PAT")
    ?? throw new InvalidOperationException("Set PMPC_PAT to a personal access token.");

var session = await broker.AuthenticateWithPersonalAccessTokenAsync(token);
if (session.IsFailure)
{
    Console.WriteLine($"Authentication failed: {session.Error.Code} {session.Error.Message}");
    return;
}

Console.WriteLine($"Connected to {session.Value.CompanyName}");
```

**See also:** [Connect-PmpcBrokerWithPat](../powershell/connect-pmpcbrokerwithpat.md) and [Exchange a personal access token for an access token](../rest-api/authentication.md#exchange-a-personal-access-token-for-an-access-token).

### GetSelectedCompany

Returns the company the session works with.

```csharp
CompanyInfo? GetSelectedCompany();
```

This method has no parameters.

**Returns:** the [`CompanyInfo`](authentication.md#company-model) of the token's company, or `null` if you haven't authenticated yet. Unlike the other methods, it returns the value directly rather than a result object.

```csharp
var current = broker.GetSelectedCompany();
Console.WriteLine(current is null
    ? "Not authenticated."
    : $"Working with {current.CompanyName}");
```

**See also:** [Get-PmpcSelectedCompany](../powershell/get-pmpcselectedcompany.md). This method has no REST operation; it reads the company stored in the SDK.

### ClearAuthenticationAsync

Signs out by clearing the session's company and service configuration.

```csharp
Task<Result> ClearAuthenticationAsync();
```

This method has no parameters.

**Returns:** a `Result` that indicates success or failure.

After this call, methods that need a company fail until you authenticate again.

```csharp
var signOut = await broker.ClearAuthenticationAsync();
if (signOut.IsFailure)
{
    Console.WriteLine($"Sign-out failed: {signOut.Error.Message}");
}
```

**See also:** [Disconnect-PmpcBroker](../powershell/disconnect-pmpcbroker.md). This method has no REST operation.

### IsServiceHealthyAsync

Checks whether the Cloud Customer API is reachable for the session's company.

```csharp
Task<Result<bool>> IsServiceHealthyAsync(CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                 |
| ------------------- | ------------------- | --------------------------- |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call. |

**Returns:** `true` if the service responded as healthy; otherwise `false`. A failed health check, or a call made before you authenticate, returns `false` rather than a failed result, so you only need to check `Value`.

```csharp
var health = await broker.IsServiceHealthyAsync();
if (health.IsSuccess && health.Value)
{
    Console.WriteLine("The Cloud Customer API is available.");
}
else
{
    Console.WriteLine("The Cloud Customer API isn't reachable. Check your network connection and that you've authenticated.");
}
```

**See also:** [Test-PmpcBrokerHealth](../powershell/test-pmpcbrokerhealth.md). This method calls the service's health endpoint, which isn't part of the documented REST operations.

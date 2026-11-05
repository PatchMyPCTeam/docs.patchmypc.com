---
description: >-
  How the .NET SDK reports success and failure through Result objects, and what
  to do about each error code.
noIndex: true
noRobotsIndex: true
---

# Results and errors

Every `IAppCatBroker` method returns a result object instead of throwing an exception when a call fails. Check the result before you use it. This page describes the result types, the error details they carry, and how to respond to each error code.

## The result types

Methods that return data return `Result<T>`, where `T` is the data type. Methods that only perform an action return `Result`. Both are in the `pmpc.appcatbroker.sdk.Models` namespace.

| Member      | Available on          | Description                                                                                                                            |
| ----------- | --------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `IsSuccess` | `Result`, `Result<T>` | `true` when the call succeeded.                                                                                                        |
| `IsFailure` | `Result`, `Result<T>` | `true` when the call failed. The opposite of `IsSuccess`.                                                                              |
| `Value`     | `Result<T>`           | The returned data. Read it only when `IsSuccess` is `true`; reading it on a failed result throws `InvalidOperationException`.          |
| `Error`     | `Result`, `Result<T>` | Details of the failure. Read it only when `IsFailure` is `true`; reading it on a successful result throws `InvalidOperationException`. |

The usual pattern is to check `IsFailure` first and return early:

```csharp
var result = await broker.GetApplicationDetailsAsync(productId);
if (result.IsFailure)
{
    Console.WriteLine($"{result.Error.Code}: {result.Error.Message}");
    return;
}

var product = result.Value;
Console.WriteLine($"{product.DisplayName} {product.UpdateVersion}");
```

### Helper methods

The result types also provide helpers for composing calls without nested `if` statements:

| Method                                      | Description                                                                                       |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `Match(onSuccess, onFailure)`               | Runs one of two functions and returns its value. `Result<T>` only.                                |
| `Map(mapper)`                               | Transforms the value of a successful result. Passes failures through unchanged. `Result<T>` only. |
| `Bind(binder)` and `BindAsync(binder)`      | Runs another result-returning call only if this one succeeded.                                    |
| `OnSuccess(action)` and `OnFailure(action)` | Runs an action for one outcome and returns the same result.                                       |
| `ToResult()` and `ToResult(value)`          | Converts between `Result` and `Result<T>`.                                                        |

```csharp
var message = (await broker.GetCustomerInfoAsync()).Match(
    onSuccess: info => $"Connected to {info.CustomerName}",
    onFailure: error => $"Couldn't read account information: {error.Message}");
```

## Error details

`Error` is a record with these properties:

| Property    | Type                         | Description                                                                                                                              |
| ----------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `Code`      | `string`                     | A stable, machine-readable code. Branch on this value. See [Error codes](results-and-errors.md#error-codes).                             |
| `Message`   | `string`                     | A human-readable description you can show to a user or write to a log. Don't parse it; the text can change.                              |
| `Type`      | `ErrorType`                  | The broad category: `Unknown`, `Validation`, `Authentication`, `Authorization`, `Network`, `Business`, `Configuration`, or `Unexpected`. |
| `Exception` | `Exception?`                 | The underlying exception for unexpected and network failures, so you can log its details. Otherwise `null`.                              |
| `Metadata`  | `Dictionary<string, object>` | Structured details about the failure. Which keys are present depends on the failure, so always use `TryGetValue`.                        |

### Metadata keys

| Key                 | Present on            | Description                                                                 |
| ------------------- | --------------------- | --------------------------------------------------------------------------- |
| `retryAfterSeconds` | `RATE_LIMITED`        | How many seconds to wait before you retry. Integer values arrive as `long`. |
| `limit`             | `RATE_LIMITED`        | The number of requests allowed in the rate-limit window.                    |
| `remaining`         | `RATE_LIMITED`        | The number of requests left in the current window.                          |
| `resetSeconds`      | `RATE_LIMITED`        | Seconds until the current window resets.                                    |
| `policy`            | `RATE_LIMITED`        | Which limit you exceeded, for example `tenant:read` or `tenant:write`.      |
| `requiredFeature`   | `FEATURE_NOT_ENABLED` | The feature to mention when you ask Patch My PC to enable it.               |

Validation failures can also carry details about which fields were rejected.

## Error codes

The SDK exposes the codes it returns from the Cloud Customer API as constants on `BrokerErrorCodes`, in the `pmpc.appcatbroker.sdk.Constants` namespace. Compare `Error.Code` against these constants rather than against string literals.

| Constant                 | Value                    | Meaning                                                                                                                                                                                                      | What to do                                                                                                                                          |
| ------------------------ | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ValidationError`        | `VALIDATION_ERROR`       | The request was invalid, for example a missing required value. The SDK also returns this code when you call a method before its prerequisites are met, for example before selecting a company or connection. | Read `Error.Message`, fix the input or call the missing setup method, and try again. Don't retry unchanged.                                         |
| `NotFound`               | `NOT_FOUND`              | The resource doesn't exist or isn't visible to your account.                                                                                                                                                 | Check the ID. Confirm you selected the right company and connection.                                                                                |
| `Conflict`               | `CONFLICT`               | The request conflicts with the current state of the resource, for example a duplicate name.                                                                                                                  | Read the current state, adjust your request, and try again.                                                                                         |
| `RateLimited`            | `RATE_LIMITED`           | You exceeded your account's request rate.                                                                                                                                                                    | Wait for `retryAfterSeconds` from `Error.Metadata`, then retry. See [Rate limits](../rate-limits.md).                                               |
| `FeatureNotEnabled`      | `FEATURE_NOT_ENABLED`    | The operation belongs to a feature that isn't enabled for your account yet.                                                                                                                                  | Contact Patch My PC to enable it. Quote `requiredFeature` from `Error.Metadata` if it's present. Retrying won't help.                               |
| `AuthenticationFailed`   | `AUTH_ERROR`             | You haven't authenticated, or your personal access token (PAT) was rejected, expired, or revoked.                                                                                                            | Check the PAT in the portal, create a new one if needed, and call `AuthenticateWithPersonalAccessTokenAsync` again.                                 |
| `AuthorizationFailed`    | `AUTHZ_ERROR`            | You're authenticated, but the operation isn't allowed. This includes a PAT whose scopes don't cover the operation, or an account without the permission.                                                     | Ask an administrator for the permission, or create a PAT with the required scope. Retrying won't help.                                              |
| `PatExchangeThrottled`   | `PAT_EXCHANGE_THROTTLED` | Too many PAT exchanges in a short time.                                                                                                                                                                      | Wait, then call `AuthenticateWithPersonalAccessTokenAsync` again. Reuse one authenticated `IAppCatBroker` instead of authenticating for every call. |
| `PatExchangeNotEntitled` | `PAT_NOT_ENTITLED`       | The PAT's company isn't entitled to use personal access tokens.                                                                                                                                              | Contact Patch My PC.                                                                                                                                |
| `OperationCancelled`     | `OPERATION_CANCELLED`    | You cancelled the call through its `CancellationToken`.                                                                                                                                                      | Nothing; treat it as a cancellation, not a failure.                                                                                                 |
| `UnexpectedError`        | `UNEXPECTED_ERROR`       | The service or the SDK failed in a way it couldn't classify, for example a server error.                                                                                                                     | Retry later. If it persists, contact Patch My PC support with the time of the failure and `Error.Message`.                                          |

The SDK can also return `NETWORK_ERROR`, which has no `BrokerErrorCodes` constant. It means the SDK couldn't reach the service, for example because of a DNS or connection failure. Check your network connection and proxy settings, then retry.

For the HTTP status codes behind these errors, see [Errors](../errors.md).

## Handle rate limits

When you exceed your account's rate limit, the result fails with `RATE_LIMITED`. Wait for the interval the service asks for, then retry:

```csharp
using pmpc.appcatbroker.sdk.Constants;
using pmpc.appcatbroker.sdk.Models;

static async Task<Result<T>> WithRetryAsync<T>(Func<Task<Result<T>>> call, int maxAttempts = 3)
{
    for (var attempt = 1; ; attempt++)
    {
        var result = await call();
        if (result.IsSuccess
            || result.Error.Code != BrokerErrorCodes.RateLimited
            || attempt == maxAttempts)
        {
            return result;
        }

        var waitSeconds = 30L;
        if (result.Error.Metadata.TryGetValue("retryAfterSeconds", out var retryAfter)
            && retryAfter is long seconds)
        {
            waitSeconds = seconds;
        }

        await Task.Delay(TimeSpan.FromSeconds(waitSeconds));
    }
}

var search = await WithRetryAsync(() => broker.SearchApplicationsAsync(new ProductFilterRequest()));
```

## Handle a feature that isn't enabled

Some operations need a feature enabled for your account. Until it is, they fail with `FEATURE_NOT_ENABLED`. Report it differently from a permission problem, because the fix is different:

```csharp
var templates = await broker.GetDeploymentTemplatesAsync();
if (templates.IsFailure)
{
    var message = templates.Error.Code switch
    {
        BrokerErrorCodes.FeatureNotEnabled => "Deployment templates aren't enabled for your account. Contact Patch My PC to enable them.",
        BrokerErrorCodes.AuthorizationFailed => "Your account doesn't have permission to read deployment templates.",
        _ => templates.Error.Message,
    };

    Console.WriteLine(message);
}
```

## Related pages

{% content-ref url="../errors.md" %}
[errors.md](../errors.md)
{% endcontent-ref %}

{% content-ref url="../rate-limits.md" %}
[rate-limits.md](../rate-limits.md)
{% endcontent-ref %}

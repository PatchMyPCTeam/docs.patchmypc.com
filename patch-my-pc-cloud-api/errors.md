---
description: >-
  HTTP status codes, problem details responses, and SDK and PowerShell module
  error codes returned by the Patch My PC Cloud Customer API.
noIndex: true
noRobotsIndex: true
---

# Errors

The Patch My PC Cloud Customer API uses standard HTTP status codes. The .NET SDK and PowerShell module translate each failure into a stable error code that you can branch on in code and scripts.

## Status codes

| Status                      | Meaning                                                                                                                                      | Retry?                                                                    |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `400 Bad Request`           | The request is invalid—for example a missing field, an invalid value, or a request that conflicts with the application's current state       | No. Fix the request.                                                      |
| `401 Unauthorized`          | Authentication is missing, expired, or was rejected                                                                                          | After you exchange your personal access token (PAT) again                 |
| `403 Forbidden`             | You're authenticated but not allowed to perform the operation, the PAT lacks a required scope, or the feature isn't enabled for your account | No. See [Forbidden responses](errors.md#understand-forbidden-responses).  |
| `404 Not Found`             | The application, deployment, or other resource doesn't exist in your account                                                                 | No                                                                        |
| `429 Too Many Requests`     | You exceeded a rate limit                                                                                                                    | Yes, after the `Retry-After` interval. See [Rate limits](rate-limits.md). |
| `500 Internal Server Error` | An unexpected failure occurred                                                                                                               | Yes, with backoff                                                         |
| `504 Gateway Timeout`       | The request took too long to complete                                                                                                        | Yes, with backoff. For searches, request fewer results at a time.         |

## Request problem details

By default, error bodies are kept simple for compatibility with existing clients: a `400` or `404` response returns a plain string that explains the problem, and most `401` and `403` responses have no body.

To receive structured errors, send `application/problem+json` in the `Accept` header. Error responses then use the problem details format ([RFC 9457](https://www.rfc-editor.org/rfc/rfc9457)):

```http
GET https://us.portal.patchmypc.com/v1/api/apps/{product-id}
Authorization: Bearer {access-token}
Accept: application/json, application/problem+json
```

The REST examples on this page use the US host. If your account is hosted in the EU, use `https://eu.portal.patchmypc.com` instead.

```json
{
  "title": "not_found",
  "status": 404,
  "detail": "{explanation}"
}
```

| Member        | Description                                                                                 |
| ------------- | ------------------------------------------------------------------------------------------- |
| `title`       | A stable, machine-readable code in lowercase with underscores. Branch on this value.        |
| `status`      | The HTTP status code                                                                        |
| `detail`      | A human-readable explanation. Don't parse it—the wording can change.                        |
| Other members | Structured context for specific errors, for example `retryAfterSeconds` on a `429` response |

Rate-limit (`429`), feature-not-enabled (`403`), and insufficient-scope (`403`) responses always use the problem details format, whether or not you ask for it.

The SDK requests problem details for you.

## Understand forbidden responses

A `403 Forbidden` response can mean three different things. With problem details, the `title` tells them apart.

| `title`               | Cause                                                                                                          | What to do                                                                                |
| --------------------- | -------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `forbidden`           | Your account doesn't have the permission the operation needs                                                   | Ask your administrator for the permission                                                 |
| `insufficient_scope`  | The PAT doesn't include the scope the operation needs. The response lists `requiredScope` and `grantedScopes`. | Create a new PAT with the required scope. See [Authentication](authentication.md#scopes). |
| `feature_not_enabled` | The operation is available, but not yet enabled for your account                                               | Contact Patch My PC                                                                       |

A feature-not-enabled response looks like this:

```json
{
  "title": "feature_not_enabled",
  "status": 403,
  "detail": "The '{feature}' feature is not enabled for this customer, and this endpoint requires it. Contact Patch My PC to have it enabled for your account.",
  "requiredFeature": "{feature}"
}
```

Retrying a `403` response doesn't help—the result is the same until the permission, scope, or feature changes.

## Error codes in the SDK and PowerShell module

SDK methods return a result instead of throwing. When `IsFailure` is `true`, `Error.Code` holds one of the codes below. The constants are defined on `BrokerErrorCodes`. The PowerShell module writes a non-terminating error record whose error ID is the same code.

| HTTP status and problem title             | Error code               | `BrokerErrorCodes` constant |
| ----------------------------------------- | ------------------------ | --------------------------- |
| `400` `validation_error`                  | `VALIDATION_ERROR`       | `ValidationError`           |
| `401` `unauthorized`                      | `AUTH_ERROR`             | `AuthenticationFailed`      |
| `403` `forbidden` or `insufficient_scope` | `AUTHZ_ERROR`            | `AuthorizationFailed`       |
| `403` `feature_not_enabled`               | `FEATURE_NOT_ENABLED`    | `FeatureNotEnabled`         |
| `404` `not_found`                         | `NOT_FOUND`              | `NotFound`                  |
| `409` `conflict`                          | `CONFLICT`               | `Conflict`                  |
| `429` `rate_limit_exceeded`               | `RATE_LIMITED`           | `RateLimited`               |
| `5xx` `internal_error`                    | `UNEXPECTED_ERROR`       | `UnexpectedError`           |
| `429` from the PAT exchange               | `PAT_EXCHANGE_THROTTLED` | `PatExchangeThrottled`      |
| `403` from the PAT exchange               | `PAT_NOT_ENTITLED`       | `PatExchangeNotEntitled`    |
| None—you canceled the operation           | `OPERATION_CANCELLED`    | `OperationCancelled`        |

The SDK can also report `NETWORK_ERROR` when it can't reach the service and `CONFIG_ERROR` when its configuration is incomplete.

For `RATE_LIMITED`, and for `PAT_EXCHANGE_THROTTLED` when the service sends a retry interval, `Error.Metadata` carries `retryAfterSeconds` so you can wait exactly as long as the service asks. In the PowerShell module, a rate-limit error has the category `LimitsExceeded`.

{% tabs %}
{% tab title="REST" %}
```http
POST https://us.portal.patchmypc.com/v1/api/apps/search
Authorization: Bearer {access-token}
Content-Type: application/json
Accept: application/json, application/problem+json

{ "displayNameSearchString": "{display-name}" }
```

Check the status code first. For a failure, read `title` from the problem details body.
{% endtab %}

{% tab title="C#" %}
{% code title="Program.cs" %}
```csharp
using pmpc.appcatbroker.sdk.Constants;

var result = await broker.GetCustomerInfoAsync();
if (result.IsFailure)
{
    switch (result.Error.Code)
    {
        case BrokerErrorCodes.FeatureNotEnabled:
            Console.WriteLine("Ask Patch My PC to enable this feature for your account.");
            break;
        case BrokerErrorCodes.RateLimited:
            result.Error.Metadata.TryGetValue("retryAfterSeconds", out var retryAfter);
            Console.WriteLine($"Rate limited. Retry after {retryAfter ?? 60} seconds.");
            break;
        default:
            Console.WriteLine($"{result.Error.Code}: {result.Error.Message}");
            break;
    }
}
```
{% endcode %}
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-PmpcCustomerInfo -ErrorAction SilentlyContinue -ErrorVariable failures
foreach ($failure in $failures) {
    switch ($failure.FullyQualifiedErrorId.Split(',')[0]) {
        'FEATURE_NOT_ENABLED' { 'Ask Patch My PC to enable this feature for your account.' }
        'RATE_LIMITED'        { 'Rate limited. Wait and try again.' }
        default               { $failure.Exception.Message }
    }
}
```
{% endtab %}
{% endtabs %}

## Related pages

* [Results and errors](sdk/results-and-errors.md)
* [Rate limits](rate-limits.md)
* [Authentication](authentication.md)

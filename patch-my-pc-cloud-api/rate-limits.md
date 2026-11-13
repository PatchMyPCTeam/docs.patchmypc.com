---
description: >-
  Request limits for the Patch My PC Cloud Customer API, the headers that report
  them, and how to retry after a 429 response.
noIndex: true
noRobotsIndex: true
---

# Rate limits

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

The Patch My PC Cloud Customer API limits how many requests your account can make in a time window. Limits apply per account, so every user, script, and personal access token (PAT) that works with the same account shares them.

## Limits

| Category | Limit        | Window     |
| -------- | ------------ | ---------- |
| Reads    | 120 requests | 60 seconds |
| Writes   | 20 requests  | 60 seconds |

Reads and writes have separate counters. Reaching the write limit doesn't stop your reads, and the other way around. Each window is fixed—the counter resets when the window ends, not gradually.

These are the default limits. Your account's limits can differ. The `RateLimit-Limit` header always reports the limit that applies to you.

## Reads and writes

An operation counts by what it does, not by its HTTP method.

| Category | Operations                                                                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Reads    | Get customer info, list connections, search applications, get application details and files, list deployments, get deployment details and dependency candidates, and list and get deployment templates |
| Writes   | Create, update, edit, and delete applications; create, edit, delete, redeploy, and sync deployments; pause and resume deployment sync; and create, update, and delete deployment templates             |

A search is a read even though it uses `POST`, because the criteria travel in the request body.

## Rate-limit headers

Responses include headers that show where you stand in the current window:

| Header                | Description                                               | Example                              |
| --------------------- | --------------------------------------------------------- | ------------------------------------ |
| `RateLimit-Limit`     | The limit, the window length in seconds, and the category | `120, 120;w=60;policy="tenant:read"` |
| `RateLimit-Remaining` | Requests left in the current window                       | `87`                                 |
| `RateLimit-Reset`     | Seconds until the window resets                           | `42`                                 |

The `policy` value is `tenant:read` for reads and `tenant:write` for writes.

## Handle a 429 response

When you exceed a limit, the Cloud Customer API returns `429 Too Many Requests` with a `Retry-After` header that gives the number of seconds to wait. The body always uses the problem details format:

```http
HTTP/1.1 429 Too Many Requests
Retry-After: 42
RateLimit-Limit: 20, 20;w=60;policy="tenant:write"
RateLimit-Remaining: 0
RateLimit-Reset: 42
Content-Type: application/problem+json
```

```json
{
  "title": "rate_limit_exceeded",
  "status": 429,
  "detail": "Request rate limit exceeded. Retry after the duration indicated by the Retry-After header.",
  "retryAfterSeconds": 42,
  "limit": 20,
  "remaining": 0,
  "resetSeconds": 42,
  "policy": "tenant:write"
}
```

The .NET SDK and PowerShell module report this as the error code `RATE_LIMITED`. In the SDK, `Error.Metadata` carries `retryAfterSeconds`, `limit`, `remaining`, `resetSeconds`, and `policy`.

## Retry with backoff

To retry well:

1. Wait at least the number of seconds in `Retry-After` before you send the request again.
2. If the retry is also rejected, wait longer each time—for example double the delay—and add a small random delay so that parallel jobs don't retry at the same moment.
3. Stop after a few attempts and report the failure.
4. Keep an eye on `RateLimit-Remaining` and slow down before it reaches zero, especially in bulk jobs that create or update many applications.

{% tabs %}
{% tab title="REST" %}
```powershell
$headers = @{ Authorization = "Bearer {access-token}"; Accept = 'application/json, application/problem+json' }
$uri = 'https://us.portal.patchmypc.com/v1/api/customer-info'

for ($attempt = 1; $attempt -le 5; $attempt++) {
    $response = Invoke-WebRequest -Uri $uri -Headers $headers -SkipHttpErrorCheck
    if ($response.StatusCode -ne 429) { break }

    $delay = [int]($response.Headers['Retry-After'] | Select-Object -First 1)
    $delay = [Math]::Max($delay, [Math]::Pow(2, $attempt)) + (Get-Random -Maximum 3)
    Start-Sleep -Seconds $delay
}
```

The example uses the US host. Use `https://eu.portal.patchmypc.com` for EU accounts or `https://uk.portal.patchmypc.com` for UK accounts.
{% endtab %}

{% tab title="C#" %}
{% code title="Program.cs" %}
```csharp
using PatchMyPC.Cloud.Constants;

for (var attempt = 1; attempt <= 5; attempt++)
{
    var result = await client.GetCustomerInfoAsync();
    if (result.IsSuccess || result.Error.Code != PmpcCloudErrorCodes.RateLimited)
    {
        break;
    }

    var retryAfter = result.Error.Metadata.TryGetValue("retryAfterSeconds", out var value)
        ? Convert.ToInt32(value)
        : 60;
    var delay = Math.Max(retryAfter, (int)Math.Pow(2, attempt)) + Random.Shared.Next(0, 3);
    await Task.Delay(TimeSpan.FromSeconds(delay));
}
```
{% endcode %}
{% endtab %}

{% tab title="PowerShell" %}
```powershell
for ($attempt = 1; $attempt -le 5; $attempt++) {
    $info = Get-PmpcCustomerInfo -ErrorAction SilentlyContinue -ErrorVariable failure
    if (-not $failure -or $failure[0].CategoryInfo.Category -ne 'LimitsExceeded') { break }

    Start-Sleep -Seconds ([Math]::Pow(2, $attempt) * 15 + (Get-Random -Maximum 3))
}
```
{% endtab %}
{% endtabs %}

## Personal access token exchange

Exchanging a PAT for an access token doesn't count against your account's read or write limits. The exchange has its own throttling, applied per network address. When it's throttled, the exchange returns `429 Too Many Requests`, and the SDK and PowerShell module report the error code `PAT_EXCHANGE_THROTTLED`.

Exchange a PAT once and reuse the access token until it's close to expiring, rather than exchanging before every request. See [Authentication](authentication.md#manage-token-lifetime).

## Related pages

* [Errors](errors.md)
* [Authentication](authentication.md)

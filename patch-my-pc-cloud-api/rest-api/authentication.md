---
description: >-
  Reference for the Authentication operations of the Patch My PC Cloud Customer
  API, with parameters, request and response schemas, and examples.
noIndex: true
noRobotsIndex: true
---

# Authentication

Operations that exchange a personal access token for an access token. For the base URL, authentication, rate limits, and errors that apply to every operation, see REST API reference.

The examples use the US host, `https://us.portal.patchmypc.com`. If your Patch My PC account is in the EU region, use `https://eu.portal.patchmypc.com` instead.

Each operation lists the scope a personal access token (PAT) needs to call it. Some operations must be enabled for your account before you can use them; those operations say so.

## Exchange a personal access token for an access token

Exchanges a personal access token, supplied in the `Authorization` header as a bearer credential, for an access token that's valid for 60 minutes. Send the access token on subsequent requests, and exchange the personal access token again when the access token expires.

Operation ID: `ExchangePatForToken`

```http
POST /v1/api/auth/token
```

**Authentication:** None. Send the PAT itself in the `Authorization` header.

**Responses**

| Status | Description           | Body                                                               |
| ------ | --------------------- | ------------------------------------------------------------------ |
| `200`  | OK                    | [`TokenExchangeResponse`](authentication.md#tokenexchangeresponse) |
| `400`  | Bad Request           | string                                                             |
| `401`  | Unauthorized          | None                                                               |
| `403`  | Forbidden             | None                                                               |
| `500`  | Internal Server Error | None                                                               |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/auth/token" \
  -H "Authorization: Bearer {personal-access-token}"
```

## Schemas

The types used by the operations on this page. Property names are case-sensitive in responses and case-insensitive in requests.

### TokenExchangeResponse

| Name         | Type            | Required | Description    |
| ------------ | --------------- | -------- | -------------- |
| `gatewayJwt` | string          | No       | Can be `null`. |
| `expiresIn`  | integer (int32) | No       |                |

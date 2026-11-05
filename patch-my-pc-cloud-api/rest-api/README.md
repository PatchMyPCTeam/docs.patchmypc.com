---
description: >-
  Overview of the Patch My PC Cloud Customer API REST operations, with the base
  URL, authentication, rate limits, errors, and an index of every operation.
noIndex: true
noRobotsIndex: true
---

# REST API reference

The Patch My PC Cloud Customer API is a REST API over HTTPS that you can use to search and manage your applications, deployments, and deployment templates. You can call it directly, or use the .NET SDK or the PowerShell module, which call the same operations for you.

The complete OpenAPI 3.0 description of the Cloud Customer API is in [openapi.json](<../../.gitbook/assets/openapi (1).json>). You can import it into an API client or a code generator.

## Base URL

Use the host for the region your Patch My PC account is in. Every operation path starts with `/v1/api`:

| Region        | Base URL                                 |
| ------------- | ---------------------------------------- |
| United States | `https://us.portal.patchmypc.com/v1/api` |
| Europe        | `https://eu.portal.patchmypc.com/v1/api` |

The examples in this reference use the US host. If your account is in the EU region, use `https://eu.portal.patchmypc.com` instead. Requests and responses use JSON (`application/json`).

## Authentication

Every operation except [Exchange a personal access token for an access token](authentication.md#exchange-a-personal-access-token-for-an-access-token) requires an access token, sent as a bearer token in the `Authorization` header:

```http
Authorization: Bearer {access-token}
```

To get an access token:

1. [Create a personal access token (PAT)](../create-a-personal-access-token.md) in the Patch My PC portal under **Settings** > **Access Tokens**, and choose the scopes your automation needs. A PAT is limited to the scopes it was created with, and never has more access than the user who created it.
2. Exchange the PAT at `POST /v1/api/auth/token` for an access token. The access token is valid for 60 minutes.
3. When a request returns `401 Unauthorized`, or the access token is close to expiring, exchange the PAT again.

Each operation in this reference lists the PAT scope it requires:

| Scope                        | Grants                                                                                          |
| ---------------------------- | ----------------------------------------------------------------------------------------------- |
| `appcatbroker:customer:read` | Read your account information.                                                                  |
| `appcatbroker:apps:read`     | Search and read applications, connections, and application files.                               |
| `appcatbroker:apps:write`    | Create, update, edit, and delete applications. Includes the access of `appcatbroker:apps:read`. |
| `appcatbroker:apps:deploy`   | Read and manage deployments and deployment templates.                                           |

For how to exchange a PAT and send the access token, see [Authentication](../authentication.md).

## Rate limits

Requests are rate limited per account, with separate counters for read and write operations. By default, you can make 120 read requests and 20 write requests every 60 seconds. When you exceed a limit, the Cloud Customer API returns `429 Too Many Requests`. Each operation in this reference says which limit it counts against. For details and retry guidance, see [Rate limits](../rate-limits.md).

## Errors

Errors are returned with a standard HTTP status code. A request that isn't valid returns `400 Bad Request`, a missing or expired token returns `401 Unauthorized`, and a token without the required permission returns `403 Forbidden`. Operations marked as requiring enablement return `403 Forbidden` with the problem title `feature_not_enabled` until they're enabled for your account. For the error format and the error codes the SDK and PowerShell module report, see [Errors](../errors.md).

## Operations

### Account and connections

| Method | Path                    | Operation                                                              | PAT scope                    | Requires enablement |
| ------ | ----------------------- | ---------------------------------------------------------------------- | ---------------------------- | ------------------- |
| `GET`  | `/v1/api/customer-info` | [Get customer info](applications.md#get-customer-info)                 | `appcatbroker:customer:read` | No                  |
| `GET`  | `/v1/api/connections`   | [Get available connections](applications.md#get-available-connections) | `appcatbroker:apps:read`     | Yes                 |

### Application management

| Method   | Path                             | Operation                                                                      | PAT scope                 | Requires enablement |
| -------- | -------------------------------- | ------------------------------------------------------------------------------ | ------------------------- | ------------------- |
| `POST`   | `/v1/api/apps/search`            | [Search applications](applications.md#search-applications)                     | `appcatbroker:apps:read`  | No                  |
| `GET`    | `/v1/api/apps/{productId}`       | [Get application details](applications.md#get-application-details)             | `appcatbroker:apps:read`  | No                  |
| `DELETE` | `/v1/api/apps/{productId}`       | [Delete an application](applications.md#delete-an-application)                 | `appcatbroker:apps:write` | Yes                 |
| `GET`    | `/v1/api/apps/{productId}/files` | [Get application files](applications.md#get-application-files)                 | `appcatbroker:apps:read`  | Yes                 |
| `POST`   | `/v1/api/apps/draft`             | [Create application draft](applications.md#create-application-draft)           | `appcatbroker:apps:write` | No                  |
| `POST`   | `/v1/api/apps/update-draft`      | [Create update draft](applications.md#create-update-draft)                     | `appcatbroker:apps:write` | No                  |
| `POST`   | `/v1/api/apps/complete`          | [Complete application creation](applications.md#complete-application-creation) | `appcatbroker:apps:write` | No                  |
| `PUT`    | `/v1/api/apps/complete`          | [Complete application update](applications.md#complete-application-update)     | `appcatbroker:apps:write` | No                  |
| `POST`   | `/v1/api/apps/edit-draft`        | [Create edit draft](applications.md#create-edit-draft)                         | `appcatbroker:apps:write` | Yes                 |
| `PUT`    | `/v1/api/apps/edit-complete`     | [Complete application edit](applications.md#complete-application-edit)         | `appcatbroker:apps:write` | Yes                 |

### Custom applications

| Method   | Path                                | Operation                                                                                    | PAT scope                 | Requires enablement |
| -------- | ----------------------------------- | -------------------------------------------------------------------------------------------- | ------------------------- | ------------------- |
| `GET`    | `/v1/api/apps/custom/{productId}`   | [Get custom application details](applications.md#get-custom-application-details)             | `appcatbroker:apps:read`  | Yes                 |
| `DELETE` | `/v1/api/apps/custom/{productId}`   | [Delete a custom application](applications.md#delete-a-custom-application)                   | `appcatbroker:apps:write` | Yes                 |
| `POST`   | `/v1/api/apps/custom/search`        | [Search custom applications](applications.md#search-custom-applications)                     | `appcatbroker:apps:read`  | Yes                 |
| `POST`   | `/v1/api/apps/custom/draft`         | [Create custom application draft](applications.md#create-custom-application-draft)           | `appcatbroker:apps:write` | Yes                 |
| `POST`   | `/v1/api/apps/custom/update-draft`  | [Create custom update draft](applications.md#create-custom-update-draft)                     | `appcatbroker:apps:write` | Yes                 |
| `POST`   | `/v1/api/apps/custom/complete`      | [Complete custom application creation](applications.md#complete-custom-application-creation) | `appcatbroker:apps:write` | Yes                 |
| `PUT`    | `/v1/api/apps/custom/complete`      | [Complete custom application update](applications.md#complete-custom-application-update)     | `appcatbroker:apps:write` | Yes                 |
| `POST`   | `/v1/api/apps/custom/edit-draft`    | [Create custom edit draft](applications.md#create-custom-edit-draft)                         | `appcatbroker:apps:write` | Yes                 |
| `PUT`    | `/v1/api/apps/custom/edit-complete` | [Complete custom application edit](applications.md#complete-custom-application-edit)         | `appcatbroker:apps:write` | Yes                 |

### Public catalog applications

| Method | Path                              | Operation                                                                        | PAT scope                | Requires enablement |
| ------ | --------------------------------- | -------------------------------------------------------------------------------- | ------------------------ | ------------------- |
| `GET`  | `/v1/api/apps/public/{productId}` | [Get public application details](applications.md#get-public-application-details) | `appcatbroker:apps:read` | Yes                 |
| `POST` | `/v1/api/apps/public/search`      | [Search public applications](applications.md#search-public-applications)         | `appcatbroker:apps:read` | Yes                 |

### Deployments

| Method   | Path                                                                       | Operation                                                                                                            | PAT scope                  | Requires enablement |
| -------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------- | ------------------- |
| `GET`    | `/v1/api/apps/{productId}/deployments`                                     | [Get application deployments](applications.md#get-application-deployments)                                           | `appcatbroker:apps:deploy` | Yes                 |
| `POST`   | `/v1/api/apps/{productId}/deployments`                                     | [Create application deployment](applications.md#create-application-deployment)                                       | `appcatbroker:apps:deploy` | Yes                 |
| `GET`    | `/v1/api/apps/{productId}/deployments/{deploymentId}`                      | [Get application deployment details](applications.md#get-application-deployment-details)                             | `appcatbroker:apps:deploy` | Yes                 |
| `PUT`    | `/v1/api/apps/{productId}/deployments/{deploymentId}`                      | [Edit application deployment](applications.md#edit-application-deployment)                                           | `appcatbroker:apps:deploy` | Yes                 |
| `DELETE` | `/v1/api/apps/{productId}/deployments/{deploymentId}`                      | [Delete application deployment](applications.md#delete-application-deployment)                                       | `appcatbroker:apps:deploy` | Yes                 |
| `GET`    | `/v1/api/apps/{productId}/deployments/dependency-candidates`               | [Get application deployment dependency candidates](applications.md#get-application-deployment-dependency-candidates) | `appcatbroker:apps:deploy` | Yes                 |
| `PUT`    | `/v1/api/apps/{productId}/deployments/{deploymentId}/redeploy`             | [Redeploy application deployment](applications.md#redeploy-application-deployment)                                   | `appcatbroker:apps:deploy` | Yes                 |
| `PUT`    | `/v1/api/apps/{productId}/deployments/{deploymentId}/sync`                 | [Sync application deployment](applications.md#sync-application-deployment)                                           | `appcatbroker:apps:deploy` | Yes                 |
| `PUT`    | `/v1/api/apps/{productId}/deployments/{deploymentId}/scheduled-sync-pause` | [Set application deployment sync pause status](applications.md#set-application-deployment-sync-pause-status)         | `appcatbroker:apps:deploy` | Yes                 |

### Deployment templates

| Method   | Path                                                   | Operation                                                                          | PAT scope                  | Requires enablement |
| -------- | ------------------------------------------------------ | ---------------------------------------------------------------------------------- | -------------------------- | ------------------- |
| `GET`    | `/v1/api/deployments/templates`                        | [Get deployment templates](applications.md#get-deployment-templates)               | `appcatbroker:apps:deploy` | Yes                 |
| `POST`   | `/v1/api/deployments/templates`                        | [Create deployment template](applications.md#create-deployment-template)           | `appcatbroker:apps:deploy` | Yes                 |
| `GET`    | `/v1/api/deployments/templates/{deploymentTemplateId}` | [Get deployment template details](applications.md#get-deployment-template-details) | `appcatbroker:apps:deploy` | Yes                 |
| `PUT`    | `/v1/api/deployments/templates/{deploymentTemplateId}` | [Update deployment template](applications.md#update-deployment-template)           | `appcatbroker:apps:deploy` | Yes                 |
| `DELETE` | `/v1/api/deployments/templates/{deploymentTemplateId}` | [Delete deployment template](applications.md#delete-deployment-template)           | `appcatbroker:apps:deploy` | Yes                 |

### Authentication

| Method | Path                 | Operation                                                                                                                      | PAT scope     | Requires enablement |
| ------ | -------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------- | ------------------- |
| `POST` | `/v1/api/auth/token` | [Exchange a personal access token for an access token](authentication.md#exchange-a-personal-access-token-for-an-access-token) | None required | No                  |

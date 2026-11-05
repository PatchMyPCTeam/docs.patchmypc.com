---
description: >-
  Reference for the Applications operations of the Patch My PC Cloud Customer
  API, with parameters, request and response schemas, and examples.
noIndex: true
noRobotsIndex: true
---

# Applications

Operations for your account, connections, applications, deployments, and deployment templates. For the base URL, authentication, rate limits, and errors that apply to every operation, see REST API reference.

The examples use the US host, `https://us.portal.patchmypc.com`. If your Patch My PC account is in the EU region, use `https://eu.portal.patchmypc.com` instead.

Each operation lists the scope a personal access token (PAT) needs to call it. Some operations must be enabled for your account before you can use them; those operations say so.

## Account and connections

### Get customer info

Retrieves information about your customer account, including its license and usage limits.

Operation ID: `GetCustomerInfo`

```http
GET /v1/api/customer-info
```

**Required PAT scope:** `appcatbroker:customer:read`

**Rate limit:** Counts against your read limit.

**Responses**

| Status | Description           | Body                                                 |
| ------ | --------------------- | ---------------------------------------------------- |
| `200`  | OK                    | [`CustomerInfoDto`](applications.md#customerinfodto) |
| `400`  | Bad Request           | string                                               |
| `401`  | Unauthorized          | None                                                 |
| `403`  | Forbidden             | None                                                 |
| `500`  | Internal Server Error | None                                                 |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/customer-info" \
  -H "Authorization: Bearer {access-token}"
```

### Get available connections

Lists the Intune connections available to the selected company. Use a connection's ID to scope application and deployment operations.

Operation ID: `GetConnections`

```http
GET /v1/api/connections
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:read`

**Rate limit:** Counts against your read limit.

**Responses**

| Status | Description           | Body                                                      |
| ------ | --------------------- | --------------------------------------------------------- |
| `200`  | OK                    | array of [`ConnectionDto`](applications.md#connectiondto) |
| `400`  | Bad Request           | string                                                    |
| `401`  | Unauthorized          | None                                                      |
| `403`  | Forbidden             | None                                                      |
| `500`  | Internal Server Error | None                                                      |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/connections" \
  -H "Authorization: Bearer {access-token}"
```

## Application management

### Search applications

Searches your custom applications using advanced filtering options. Any feed types in the request are ignored and replaced with `CUSTOMER`.

Operation ID: `SearchApplications`

```http
POST /v1/api/apps/search
```

**Required PAT scope:** `appcatbroker:apps:read`

**Rate limit:** Counts against your read limit.

**Request body**

Required. Content type `application/json`. Type: `ProductFilterRequest`.

| Name                      | Type                                                                          | Required | Description    |
| ------------------------- | ----------------------------------------------------------------------------- | -------- | -------------- |
| `vendorIds`               | array of string (uuid)                                                        | No       | Can be `null`. |
| `languages`               | array of string                                                               | No       | Can be `null`. |
| `architectures`           | array of [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | Can be `null`. |
| `osType`                  | [`OSType`](applications.md#ostype)                                            | No       | Can be `null`. |
| `feedTypes`               | array of [`CatalogFeedType`](applications.md#catalogfeedtype)                 | No       | Can be `null`. |
| `connectionId`            | string (uuid)                                                                 | No       | Can be `null`. |
| `lastModifiedFromUtc`     | string (date-time)                                                            | No       | Can be `null`. |
| `lastModifiedToUtc`       | string (date-time)                                                            | No       | Can be `null`. |
| `lastUpdatedFromUtc`      | string (date-time)                                                            | No       | Can be `null`. |
| `lastUpdatedToUtc`        | string (date-time)                                                            | No       | Can be `null`. |
| `displayNameSearchString` | string                                                                        | No       | Can be `null`. |
| `skip`                    | integer (int32)                                                               | No       |                |
| `limit`                   | integer (int32)                                                               | No       |                |
| `sortField`               | string                                                                        | No       | Can be `null`. |
| `ascending`               | boolean                                                                       | No       |                |
| `includeIconData`         | boolean                                                                       | No       |                |

**Responses**

| Status | Description           | Body                                                             |
| ------ | --------------------- | ---------------------------------------------------------------- |
| `200`  | OK                    | [`ProductFilterResponse`](applications.md#productfilterresponse) |
| `400`  | Bad Request           | string                                                           |
| `401`  | Unauthorized          | None                                                             |
| `403`  | Forbidden             | None                                                             |
| `500`  | Internal Server Error | None                                                             |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/search" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

### Get application details

Retrieves detailed information about an application in your custom application catalog by its product ID.

Operation ID: `GetApplicationDetails`

```http
GET /v1/api/apps/{productId}
```

**Required PAT scope:** `appcatbroker:apps:read`

**Rate limit:** Counts against your read limit.

**Parameters**

| Name        | In   | Type          | Required | Description |
| ----------- | ---- | ------------- | -------- | ----------- |
| `productId` | path | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body                                       |
| ------ | --------------------- | ------------------------------------------ |
| `200`  | OK                    | [`ProductDto`](applications.md#productdto) |
| `400`  | Bad Request           | string                                     |
| `401`  | Unauthorized          | None                                       |
| `403`  | Forbidden             | None                                       |
| `404`  | Not Found             | None                                       |
| `500`  | Internal Server Error | None                                       |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/apps/{productId}" \
  -H "Authorization: Bearer {access-token}"
```

### Delete an application

Deletes a custom application you own, freeing a slot against your custom application limit. Only your own custom applications can be deleted; public catalog applications are shared and can't be deleted. The request is rejected while the application's latest update is in a state that isn't safe to remove.

Operation ID: `DeleteApplication`

```http
DELETE /v1/api/apps/{productId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name        | In   | Type          | Required | Description |
| ----------- | ---- | ------------- | -------- | ----------- |
| `productId` | path | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body   |
| ------ | --------------------- | ------ |
| `200`  | OK                    | None   |
| `400`  | Bad Request           | string |
| `401`  | Unauthorized          | None   |
| `403`  | Forbidden             | None   |
| `404`  | Not Found             | None   |
| `500`  | Internal Server Error | None   |

**Example request**

```bash
curl -X DELETE "https://us.portal.patchmypc.com/v1/api/apps/{productId}" \
  -H "Authorization: Bearer {access-token}"
```

### Get application files

Lists the files of an application's current version, in exactly the shape the completion operations accept. An edit replaces the file list rather than merging it, so you must send the complete list back; use this operation to get it without rebuilding it from local state.

Operation ID: `GetApplicationFiles`

```http
GET /v1/api/apps/{productId}/files
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:read`

**Rate limit:** Counts against your read limit.

**Parameters**

| Name        | In   | Type          | Required | Description |
| ----------- | ---- | ------------- | -------- | ----------- |
| `productId` | path | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body                                                                |
| ------ | --------------------- | ------------------------------------------------------------------- |
| `200`  | OK                    | array of [`ApplicationFileDto`](applications.md#applicationfiledto) |
| `400`  | Bad Request           | string                                                              |
| `401`  | Unauthorized          | None                                                                |
| `403`  | Forbidden             | None                                                                |
| `404`  | Not Found             | None                                                                |
| `500`  | Internal Server Error | None                                                                |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/apps/{productId}/files" \
  -H "Authorization: Bearer {access-token}"
```

### Create application draft

Creates a new application draft.

Operation ID: `CreateApplicationDraft`

```http
POST /v1/api/apps/draft
```

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/draft" \
  -H "Authorization: Bearer {access-token}"
```

### Create update draft

Creates a new update draft for an existing application.

Operation ID: `CreateUpdateDraft`

```http
POST /v1/api/apps/update-draft
```

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationUpdateDraftRequest`.

| Name        | Type          | Required | Description |
| ----------- | ------------- | -------- | ----------- |
| `productId` | string (uuid) | No       |             |
| `updateId`  | string (uuid) | No       |             |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/update-draft" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
  "productId": "{productId}",
  "updateId": "{updateId}"
}'
```

### Complete application creation

Completes a new application creation process.

Operation ID: `CompleteApplication`

```http
POST /v1/api/apps/complete
```

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationCompletionRequest`.

| Name                      | Type                                                                 | Required | Description    |
| ------------------------- | -------------------------------------------------------------------- | -------- | -------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       |                |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       |                |
| `arpDisplayNameMatch`     | string                                                               | No       | Can be `null`. |
| `arpVersionMatch`         | string                                                               | No       | Can be `null`. |
| `conflictingProcesses`    | array of string                                                      | No       | Can be `null`. |
| `description`             | string                                                               | No       | Can be `null`. |
| `displayName`             | string                                                               | No       | Can be `null`. |
| `documentationURL`        | string                                                               | No       | Can be `null`. |
| `privacyURL`              | string                                                               | No       | Can be `null`. |
| `informationURL`          | string                                                               | No       | Can be `null`. |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       |                |
| `language`                | string                                                               | No       | Can be `null`. |
| `notes`                   | string                                                               | No       | Can be `null`. |
| `intuneNotes`             | string                                                               | No       | Can be `null`. |
| `publisher`               | string                                                               | No       | Can be `null`. |
| `developer`               | string                                                               | No       | Can be `null`. |
| `owner`                   | string                                                               | No       | Can be `null`. |
| `updateId`                | string (uuid)                                                        | No       |                |
| `productId`               | string (uuid)                                                        | No       |                |
| `msiProductCode`          | string (uuid)                                                        | No       | Can be `null`. |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Can be `null`. |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Can be `null`. |
| `revisionId`              | integer (int32)                                                      | No       |                |
| `iconUrl`                 | string                                                               | No       | Can be `null`. |
| `folderPath`              | string                                                               | No       | Can be `null`. |
| `primaryInstallerFile`    | string                                                               | No       | Can be `null`. |
| `cmdArguments`            | string                                                               | No       | Can be `null`. |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/complete" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

### Complete application update

Completes an existing application update process.

Operation ID: `CompleteUpdate`

```http
PUT /v1/api/apps/complete
```

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationCompletionRequest`.

| Name                      | Type                                                                 | Required | Description    |
| ------------------------- | -------------------------------------------------------------------- | -------- | -------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       |                |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       |                |
| `arpDisplayNameMatch`     | string                                                               | No       | Can be `null`. |
| `arpVersionMatch`         | string                                                               | No       | Can be `null`. |
| `conflictingProcesses`    | array of string                                                      | No       | Can be `null`. |
| `description`             | string                                                               | No       | Can be `null`. |
| `displayName`             | string                                                               | No       | Can be `null`. |
| `documentationURL`        | string                                                               | No       | Can be `null`. |
| `privacyURL`              | string                                                               | No       | Can be `null`. |
| `informationURL`          | string                                                               | No       | Can be `null`. |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       |                |
| `language`                | string                                                               | No       | Can be `null`. |
| `notes`                   | string                                                               | No       | Can be `null`. |
| `intuneNotes`             | string                                                               | No       | Can be `null`. |
| `publisher`               | string                                                               | No       | Can be `null`. |
| `developer`               | string                                                               | No       | Can be `null`. |
| `owner`                   | string                                                               | No       | Can be `null`. |
| `updateId`                | string (uuid)                                                        | No       |                |
| `productId`               | string (uuid)                                                        | No       |                |
| `msiProductCode`          | string (uuid)                                                        | No       | Can be `null`. |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Can be `null`. |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Can be `null`. |
| `revisionId`              | integer (int32)                                                      | No       |                |
| `iconUrl`                 | string                                                               | No       | Can be `null`. |
| `folderPath`              | string                                                               | No       | Can be `null`. |
| `primaryInstallerFile`    | string                                                               | No       | Can be `null`. |
| `cmdArguments`            | string                                                               | No       | Can be `null`. |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `404`  | Not Found             | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X PUT "https://us.portal.patchmypc.com/v1/api/apps/complete" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

### Create edit draft

Creates a draft for editing an existing version of an application in place. Unlike an update draft, this doesn't create a new version—it opens the existing version for revision, so you can correct metadata without publishing a new version number.

Operation ID: `CreateEditDraft`

```http
POST /v1/api/apps/edit-draft
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationUpdateDraftRequest`.

| Name        | Type          | Required | Description |
| ----------- | ------------- | -------- | ----------- |
| `productId` | string (uuid) | No       |             |
| `updateId`  | string (uuid) | No       |             |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `404`  | Not Found             | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/edit-draft" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
  "productId": "{productId}",
  "updateId": "{updateId}"
}'
```

### Complete application edit

Completes an in-place edit of an existing application version. Changes product metadata (display name, description, publisher, owner, developer, icon, and URLs) and update-level settings without creating a new version. To publish a new version instead, use `PUT /v1/api/apps/complete`.

Operation ID: `CompleteEdit`

```http
PUT /v1/api/apps/edit-complete
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationCompletionRequest`.

| Name                      | Type                                                                 | Required | Description    |
| ------------------------- | -------------------------------------------------------------------- | -------- | -------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       |                |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       |                |
| `arpDisplayNameMatch`     | string                                                               | No       | Can be `null`. |
| `arpVersionMatch`         | string                                                               | No       | Can be `null`. |
| `conflictingProcesses`    | array of string                                                      | No       | Can be `null`. |
| `description`             | string                                                               | No       | Can be `null`. |
| `displayName`             | string                                                               | No       | Can be `null`. |
| `documentationURL`        | string                                                               | No       | Can be `null`. |
| `privacyURL`              | string                                                               | No       | Can be `null`. |
| `informationURL`          | string                                                               | No       | Can be `null`. |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       |                |
| `language`                | string                                                               | No       | Can be `null`. |
| `notes`                   | string                                                               | No       | Can be `null`. |
| `intuneNotes`             | string                                                               | No       | Can be `null`. |
| `publisher`               | string                                                               | No       | Can be `null`. |
| `developer`               | string                                                               | No       | Can be `null`. |
| `owner`                   | string                                                               | No       | Can be `null`. |
| `updateId`                | string (uuid)                                                        | No       |                |
| `productId`               | string (uuid)                                                        | No       |                |
| `msiProductCode`          | string (uuid)                                                        | No       | Can be `null`. |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Can be `null`. |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Can be `null`. |
| `revisionId`              | integer (int32)                                                      | No       |                |
| `iconUrl`                 | string                                                               | No       | Can be `null`. |
| `folderPath`              | string                                                               | No       | Can be `null`. |
| `primaryInstallerFile`    | string                                                               | No       | Can be `null`. |
| `cmdArguments`            | string                                                               | No       | Can be `null`. |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `404`  | Not Found             | None                                                                         |
| `409`  | Conflict              | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X PUT "https://us.portal.patchmypc.com/v1/api/apps/edit-complete" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

## Custom applications

### Get custom application details

Retrieves detailed information about an application in your custom application catalog. Returns only the fields relevant to a custom application.

Operation ID: `GetCustomApplicationDetails`

```http
GET /v1/api/apps/custom/{productId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:read`

**Rate limit:** Counts against your read limit.

**Parameters**

| Name        | In   | Type          | Required | Description |
| ----------- | ---- | ------------- | -------- | ----------- |
| `productId` | path | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body                                                           |
| ------ | --------------------- | -------------------------------------------------------------- |
| `200`  | OK                    | [`CustomApplicationDto`](applications.md#customapplicationdto) |
| `400`  | Bad Request           | string                                                         |
| `401`  | Unauthorized          | None                                                           |
| `403`  | Forbidden             | None                                                           |
| `404`  | Not Found             | None                                                           |
| `500`  | Internal Server Error | None                                                           |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/apps/custom/{productId}" \
  -H "Authorization: Bearer {access-token}"
```

### Delete a custom application

Deletes a custom application you own, freeing a slot against your custom application limit. Only your own custom applications can be deleted; public catalog applications are shared and can't be deleted. The request is rejected while the application's latest update is in a state that isn't safe to remove.

Operation ID: `DeleteCustomApplication`

```http
DELETE /v1/api/apps/custom/{productId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name        | In   | Type          | Required | Description |
| ----------- | ---- | ------------- | -------- | ----------- |
| `productId` | path | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body   |
| ------ | --------------------- | ------ |
| `200`  | OK                    | None   |
| `400`  | Bad Request           | string |
| `401`  | Unauthorized          | None   |
| `403`  | Forbidden             | None   |
| `404`  | Not Found             | None   |
| `500`  | Internal Server Error | None   |

**Example request**

```bash
curl -X DELETE "https://us.portal.patchmypc.com/v1/api/apps/custom/{productId}" \
  -H "Authorization: Bearer {access-token}"
```

### Search custom applications

Searches your own custom applications. Any feed types in the request body are ignored and replaced with `CUSTOMER`.

Operation ID: `SearchCustomApplications`

```http
POST /v1/api/apps/custom/search
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:read`

**Rate limit:** Counts against your read limit.

**Request body**

Required. Content type `application/json`. Type: `ProductFilterRequest`.

| Name                      | Type                                                                          | Required | Description    |
| ------------------------- | ----------------------------------------------------------------------------- | -------- | -------------- |
| `vendorIds`               | array of string (uuid)                                                        | No       | Can be `null`. |
| `languages`               | array of string                                                               | No       | Can be `null`. |
| `architectures`           | array of [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | Can be `null`. |
| `osType`                  | [`OSType`](applications.md#ostype)                                            | No       | Can be `null`. |
| `feedTypes`               | array of [`CatalogFeedType`](applications.md#catalogfeedtype)                 | No       | Can be `null`. |
| `connectionId`            | string (uuid)                                                                 | No       | Can be `null`. |
| `lastModifiedFromUtc`     | string (date-time)                                                            | No       | Can be `null`. |
| `lastModifiedToUtc`       | string (date-time)                                                            | No       | Can be `null`. |
| `lastUpdatedFromUtc`      | string (date-time)                                                            | No       | Can be `null`. |
| `lastUpdatedToUtc`        | string (date-time)                                                            | No       | Can be `null`. |
| `displayNameSearchString` | string                                                                        | No       | Can be `null`. |
| `skip`                    | integer (int32)                                                               | No       |                |
| `limit`                   | integer (int32)                                                               | No       |                |
| `sortField`               | string                                                                        | No       | Can be `null`. |
| `ascending`               | boolean                                                                       | No       |                |
| `includeIconData`         | boolean                                                                       | No       |                |

**Responses**

| Status | Description           | Body                                                             |
| ------ | --------------------- | ---------------------------------------------------------------- |
| `200`  | OK                    | [`ProductFilterResponse`](applications.md#productfilterresponse) |
| `400`  | Bad Request           | string                                                           |
| `401`  | Unauthorized          | None                                                             |
| `403`  | Forbidden             | None                                                             |
| `500`  | Internal Server Error | None                                                             |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/custom/search" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

### Create custom application draft

Creates a new custom application draft.

Operation ID: `CreateCustomApplicationDraft`

```http
POST /v1/api/apps/custom/draft
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/custom/draft" \
  -H "Authorization: Bearer {access-token}"
```

### Create custom update draft

Creates a new update draft for an existing custom application.

Operation ID: `CreateCustomUpdateDraft`

```http
POST /v1/api/apps/custom/update-draft
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationUpdateDraftRequest`.

| Name        | Type          | Required | Description |
| ----------- | ------------- | -------- | ----------- |
| `productId` | string (uuid) | No       |             |
| `updateId`  | string (uuid) | No       |             |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/custom/update-draft" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
  "productId": "{productId}",
  "updateId": "{updateId}"
}'
```

### Complete custom application creation

Completes a new custom application creation process.

Operation ID: `CompleteCustomApplication`

```http
POST /v1/api/apps/custom/complete
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationCompletionRequest`.

| Name                      | Type                                                                 | Required | Description    |
| ------------------------- | -------------------------------------------------------------------- | -------- | -------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       |                |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       |                |
| `arpDisplayNameMatch`     | string                                                               | No       | Can be `null`. |
| `arpVersionMatch`         | string                                                               | No       | Can be `null`. |
| `conflictingProcesses`    | array of string                                                      | No       | Can be `null`. |
| `description`             | string                                                               | No       | Can be `null`. |
| `displayName`             | string                                                               | No       | Can be `null`. |
| `documentationURL`        | string                                                               | No       | Can be `null`. |
| `privacyURL`              | string                                                               | No       | Can be `null`. |
| `informationURL`          | string                                                               | No       | Can be `null`. |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       |                |
| `language`                | string                                                               | No       | Can be `null`. |
| `notes`                   | string                                                               | No       | Can be `null`. |
| `intuneNotes`             | string                                                               | No       | Can be `null`. |
| `publisher`               | string                                                               | No       | Can be `null`. |
| `developer`               | string                                                               | No       | Can be `null`. |
| `owner`                   | string                                                               | No       | Can be `null`. |
| `updateId`                | string (uuid)                                                        | No       |                |
| `productId`               | string (uuid)                                                        | No       |                |
| `msiProductCode`          | string (uuid)                                                        | No       | Can be `null`. |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Can be `null`. |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Can be `null`. |
| `revisionId`              | integer (int32)                                                      | No       |                |
| `iconUrl`                 | string                                                               | No       | Can be `null`. |
| `folderPath`              | string                                                               | No       | Can be `null`. |
| `primaryInstallerFile`    | string                                                               | No       | Can be `null`. |
| `cmdArguments`            | string                                                               | No       | Can be `null`. |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `409`  | Conflict              | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/custom/complete" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

### Complete custom application update

Completes an existing custom application update process.

Operation ID: `CompleteCustomUpdate`

```http
PUT /v1/api/apps/custom/complete
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationCompletionRequest`.

| Name                      | Type                                                                 | Required | Description    |
| ------------------------- | -------------------------------------------------------------------- | -------- | -------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       |                |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       |                |
| `arpDisplayNameMatch`     | string                                                               | No       | Can be `null`. |
| `arpVersionMatch`         | string                                                               | No       | Can be `null`. |
| `conflictingProcesses`    | array of string                                                      | No       | Can be `null`. |
| `description`             | string                                                               | No       | Can be `null`. |
| `displayName`             | string                                                               | No       | Can be `null`. |
| `documentationURL`        | string                                                               | No       | Can be `null`. |
| `privacyURL`              | string                                                               | No       | Can be `null`. |
| `informationURL`          | string                                                               | No       | Can be `null`. |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       |                |
| `language`                | string                                                               | No       | Can be `null`. |
| `notes`                   | string                                                               | No       | Can be `null`. |
| `intuneNotes`             | string                                                               | No       | Can be `null`. |
| `publisher`               | string                                                               | No       | Can be `null`. |
| `developer`               | string                                                               | No       | Can be `null`. |
| `owner`                   | string                                                               | No       | Can be `null`. |
| `updateId`                | string (uuid)                                                        | No       |                |
| `productId`               | string (uuid)                                                        | No       |                |
| `msiProductCode`          | string (uuid)                                                        | No       | Can be `null`. |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Can be `null`. |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Can be `null`. |
| `revisionId`              | integer (int32)                                                      | No       |                |
| `iconUrl`                 | string                                                               | No       | Can be `null`. |
| `folderPath`              | string                                                               | No       | Can be `null`. |
| `primaryInstallerFile`    | string                                                               | No       | Can be `null`. |
| `cmdArguments`            | string                                                               | No       | Can be `null`. |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `404`  | Not Found             | None                                                                         |
| `409`  | Conflict              | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X PUT "https://us.portal.patchmypc.com/v1/api/apps/custom/complete" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

### Create custom edit draft

Creates a draft for editing an existing version of a custom application in place. Unlike an update draft, this doesn't create a new version—it opens the existing version for revision, so you can correct metadata without publishing a new version number.

Operation ID: `CreateCustomEditDraft`

```http
POST /v1/api/apps/custom/edit-draft
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationUpdateDraftRequest`.

| Name        | Type          | Required | Description |
| ----------- | ------------- | -------- | ----------- |
| `productId` | string (uuid) | No       |             |
| `updateId`  | string (uuid) | No       |             |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `404`  | Not Found             | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/custom/edit-draft" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
  "productId": "{productId}",
  "updateId": "{updateId}"
}'
```

### Complete custom application edit

Completes an in-place edit of an existing custom application version. Changes product metadata (display name, description, publisher, owner, developer, icon, and URLs) and update-level settings without creating a new version.

Operation ID: `CompleteCustomEdit`

```http
PUT /v1/api/apps/custom/edit-complete
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:write`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `ApplicationCompletionRequest`.

| Name                      | Type                                                                 | Required | Description    |
| ------------------------- | -------------------------------------------------------------------- | -------- | -------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       |                |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       |                |
| `arpDisplayNameMatch`     | string                                                               | No       | Can be `null`. |
| `arpVersionMatch`         | string                                                               | No       | Can be `null`. |
| `conflictingProcesses`    | array of string                                                      | No       | Can be `null`. |
| `description`             | string                                                               | No       | Can be `null`. |
| `displayName`             | string                                                               | No       | Can be `null`. |
| `documentationURL`        | string                                                               | No       | Can be `null`. |
| `privacyURL`              | string                                                               | No       | Can be `null`. |
| `informationURL`          | string                                                               | No       | Can be `null`. |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       |                |
| `language`                | string                                                               | No       | Can be `null`. |
| `notes`                   | string                                                               | No       | Can be `null`. |
| `intuneNotes`             | string                                                               | No       | Can be `null`. |
| `publisher`               | string                                                               | No       | Can be `null`. |
| `developer`               | string                                                               | No       | Can be `null`. |
| `owner`                   | string                                                               | No       | Can be `null`. |
| `updateId`                | string (uuid)                                                        | No       |                |
| `productId`               | string (uuid)                                                        | No       |                |
| `msiProductCode`          | string (uuid)                                                        | No       | Can be `null`. |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Can be `null`. |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Can be `null`. |
| `revisionId`              | integer (int32)                                                      | No       |                |
| `iconUrl`                 | string                                                               | No       | Can be `null`. |
| `folderPath`              | string                                                               | No       | Can be `null`. |
| `primaryInstallerFile`    | string                                                               | No       | Can be `null`. |
| `cmdArguments`            | string                                                               | No       | Can be `null`. |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                                                         |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| `200`  | OK                    | [`ApplicationCreationResponse`](applications.md#applicationcreationresponse) |
| `400`  | Bad Request           | string                                                                       |
| `401`  | Unauthorized          | None                                                                         |
| `403`  | Forbidden             | None                                                                         |
| `404`  | Not Found             | None                                                                         |
| `409`  | Conflict              | None                                                                         |
| `500`  | Internal Server Error | None                                                                         |

**Example request**

```bash
curl -X PUT "https://us.portal.patchmypc.com/v1/api/apps/custom/edit-complete" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

## Public catalog applications

### Get public application details

Retrieves detailed information about an application in the public Patch My PC catalog. Returns only the fields relevant to a public catalog application. `connectionId` is required and identifies the Intune connection that scopes the lookup. `osType` is optional and defaults to `Windows`; `MacOS` requires your account to be entitled to macOS applications, otherwise the application is reported as not found.

Operation ID: `GetPublicApplicationDetails`

```http
GET /v1/api/apps/public/{productId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:read`

**Rate limit:** Counts against your read limit.

**Parameters**

| Name           | In    | Type                               | Required | Description |
| -------------- | ----- | ---------------------------------- | -------- | ----------- |
| `productId`    | path  | string (uuid)                      | Yes      |             |
| `connectionId` | query | string (uuid)                      | Yes      |             |
| `osType`       | query | [`OSType`](applications.md#ostype) | No       |             |

**Responses**

| Status | Description           | Body                                                           |
| ------ | --------------------- | -------------------------------------------------------------- |
| `200`  | OK                    | [`PublicApplicationDto`](applications.md#publicapplicationdto) |
| `400`  | Bad Request           | string                                                         |
| `401`  | Unauthorized          | None                                                           |
| `403`  | Forbidden             | None                                                           |
| `404`  | Not Found             | None                                                           |
| `500`  | Internal Server Error | None                                                           |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/apps/public/{productId}?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

### Search public applications

Searches the public Patch My PC catalog. Any feed types in the request body are ignored and replaced with `PMPC`. `connectionId` is required and identifies the Intune connection that scopes the search.

Operation ID: `SearchPublicApplications`

```http
POST /v1/api/apps/public/search
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:read`

**Rate limit:** Counts against your read limit.

**Request body**

Required. Content type `application/json`. Type: `ProductFilterRequest`.

| Name                      | Type                                                                          | Required | Description    |
| ------------------------- | ----------------------------------------------------------------------------- | -------- | -------------- |
| `vendorIds`               | array of string (uuid)                                                        | No       | Can be `null`. |
| `languages`               | array of string                                                               | No       | Can be `null`. |
| `architectures`           | array of [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | Can be `null`. |
| `osType`                  | [`OSType`](applications.md#ostype)                                            | No       | Can be `null`. |
| `feedTypes`               | array of [`CatalogFeedType`](applications.md#catalogfeedtype)                 | No       | Can be `null`. |
| `connectionId`            | string (uuid)                                                                 | No       | Can be `null`. |
| `lastModifiedFromUtc`     | string (date-time)                                                            | No       | Can be `null`. |
| `lastModifiedToUtc`       | string (date-time)                                                            | No       | Can be `null`. |
| `lastUpdatedFromUtc`      | string (date-time)                                                            | No       | Can be `null`. |
| `lastUpdatedToUtc`        | string (date-time)                                                            | No       | Can be `null`. |
| `displayNameSearchString` | string                                                                        | No       | Can be `null`. |
| `skip`                    | integer (int32)                                                               | No       |                |
| `limit`                   | integer (int32)                                                               | No       |                |
| `sortField`               | string                                                                        | No       | Can be `null`. |
| `ascending`               | boolean                                                                       | No       |                |
| `includeIconData`         | boolean                                                                       | No       |                |

**Responses**

| Status | Description           | Body                                                             |
| ------ | --------------------- | ---------------------------------------------------------------- |
| `200`  | OK                    | [`ProductFilterResponse`](applications.md#productfilterresponse) |
| `400`  | Bad Request           | string                                                           |
| `401`  | Unauthorized          | None                                                             |
| `403`  | Forbidden             | None                                                             |
| `500`  | Internal Server Error | None                                                             |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/public/search" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

## Deployments

### Get application deployments

Lists the Intune deployments that exist for an application under the given connection.

Operation ID: `GetApplicationDeployments`

```http
GET /v1/api/apps/{productId}/deployments
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your read limit.

**Parameters**

| Name           | In    | Type          | Required | Description |
| -------------- | ----- | ------------- | -------- | ----------- |
| `productId`    | path  | string (uuid) | Yes      |             |
| `connectionId` | query | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body                                                      |
| ------ | --------------------- | --------------------------------------------------------- |
| `200`  | OK                    | array of [`DeploymentDto`](applications.md#deploymentdto) |
| `400`  | Bad Request           | string                                                    |
| `401`  | Unauthorized          | None                                                      |
| `403`  | Forbidden             | None                                                      |
| `404`  | Not Found             | None                                                      |
| `500`  | Internal Server Error | None                                                      |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/apps/{productId}/deployments?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

### Create application deployment

Creates a new Intune deployment for an application under the given connection.

Operation ID: `CreateApplicationDeployment`

```http
POST /v1/api/apps/{productId}/deployments
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name        | In   | Type          | Required | Description |
| ----------- | ---- | ------------- | -------- | ----------- |
| `productId` | path | string (uuid) | Yes      |             |

**Request body**

Required. Content type `application/json`. Type: `CreateDeploymentRequest`.

| Name                  | Type                                                                                              | Required | Description    |
| --------------------- | ------------------------------------------------------------------------------------------------- | -------- | -------------- |
| `connectionId`        | string (uuid)                                                                                     | No       |                |
| `osType`              | [`OSType`](applications.md#ostype)                                                                | No       |                |
| `assignments`         | array of [`CreateDeploymentAssignmentRequest`](applications.md#createdeploymentassignmentrequest) | No       | Can be `null`. |
| `categoryIds`         | array of string                                                                                   | No       | Can be `null`. |
| `espProfileIds`       | array of string                                                                                   | No       | Can be `null`. |
| `parentDeploymentIds` | array of string                                                                                   | No       | Can be `null`. |
| `configuration`       | [`DeploymentConfigurationRequest`](applications.md#deploymentconfigurationrequest)                | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                             |
| ------ | --------------------- | ------------------------------------------------ |
| `200`  | OK                    | [`DeploymentDto`](applications.md#deploymentdto) |
| `400`  | Bad Request           | string                                           |
| `401`  | Unauthorized          | None                                             |
| `403`  | Forbidden             | None                                             |
| `404`  | Not Found             | None                                             |
| `500`  | Internal Server Error | None                                             |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/apps/{productId}/deployments" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
  "connectionId": "{connectionId}",
  "osType": "Windows",
  "assignments": [],
  "categoryIds": [],
  "espProfileIds": [],
  "parentDeploymentIds": [],
  "configuration": {}
}'
```

### Get application deployment details

Retrieves full detail for a single Intune deployment, including categories, Enrollment Status Page (ESP) profiles, and the dependency chain (parent and child deployments)—fields that the list operation doesn't return.

Operation ID: `GetApplicationDeploymentDetails`

```http
GET /v1/api/apps/{productId}/deployments/{deploymentId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your read limit.

**Parameters**

| Name           | In    | Type          | Required | Description |
| -------------- | ----- | ------------- | -------- | ----------- |
| `productId`    | path  | string (uuid) | Yes      |             |
| `deploymentId` | path  | string        | Yes      |             |
| `connectionId` | query | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body                                                         |
| ------ | --------------------- | ------------------------------------------------------------ |
| `200`  | OK                    | [`DeploymentDetailDto`](applications.md#deploymentdetaildto) |
| `400`  | Bad Request           | string                                                       |
| `401`  | Unauthorized          | None                                                         |
| `403`  | Forbidden             | None                                                         |
| `404`  | Not Found             | None                                                         |
| `500`  | Internal Server Error | None                                                         |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/apps/{productId}/deployments/{deploymentId}?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

### Edit application deployment

Edits an existing Intune deployment's name, group assignments, categories, ESP profiles, dependencies, and configuration—conflicting-process behavior, return codes, requirements, install parameters, application information overrides, and behavior settings. Any field you leave unset keeps its current value. Not supported for ring-enabled deployments.

Operation ID: `EditApplicationDeployment`

```http
PUT /v1/api/apps/{productId}/deployments/{deploymentId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name           | In   | Type          | Required | Description |
| -------------- | ---- | ------------- | -------- | ----------- |
| `productId`    | path | string (uuid) | Yes      |             |
| `deploymentId` | path | string        | Yes      |             |

**Request body**

Required. Content type `application/json`. Type: `EditDeploymentRequest`.

| Name                  | Type                                                                                              | Required | Description    |
| --------------------- | ------------------------------------------------------------------------------------------------- | -------- | -------------- |
| `connectionId`        | string (uuid)                                                                                     | No       |                |
| `name`                | string                                                                                            | No       | Can be `null`. |
| `assignments`         | array of [`CreateDeploymentAssignmentRequest`](applications.md#createdeploymentassignmentrequest) | No       | Can be `null`. |
| `configuration`       | [`DeploymentConfigurationRequest`](applications.md#deploymentconfigurationrequest)                | No       | Can be `null`. |
| `categoryIds`         | array of string                                                                                   | No       | Can be `null`. |
| `espProfileIds`       | array of string                                                                                   | No       | Can be `null`. |
| `parentDeploymentIds` | array of string                                                                                   | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                             |
| ------ | --------------------- | ------------------------------------------------ |
| `200`  | OK                    | [`DeploymentDto`](applications.md#deploymentdto) |
| `400`  | Bad Request           | string                                           |
| `401`  | Unauthorized          | None                                             |
| `403`  | Forbidden             | None                                             |
| `404`  | Not Found             | None                                             |
| `409`  | Conflict              | None                                             |
| `500`  | Internal Server Error | None                                             |

**Example request**

```bash
curl -X PUT "https://us.portal.patchmypc.com/v1/api/apps/{productId}/deployments/{deploymentId}" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
  "connectionId": "{connectionId}",
  "name": "{name}",
  "assignments": [],
  "configuration": {},
  "categoryIds": [],
  "espProfileIds": [],
  "parentDeploymentIds": []
}'
```

### Delete application deployment

Deletes an existing Intune deployment. Allowed only while the deployment isn't in progress or already being deleted.

Operation ID: `DeleteApplicationDeployment`

```http
DELETE /v1/api/apps/{productId}/deployments/{deploymentId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name           | In    | Type          | Required | Description |
| -------------- | ----- | ------------- | -------- | ----------- |
| `productId`    | path  | string (uuid) | Yes      |             |
| `deploymentId` | path  | string        | Yes      |             |
| `connectionId` | query | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body   |
| ------ | --------------------- | ------ |
| `200`  | OK                    | None   |
| `400`  | Bad Request           | string |
| `401`  | Unauthorized          | None   |
| `403`  | Forbidden             | None   |
| `404`  | Not Found             | None   |
| `500`  | Internal Server Error | None   |

**Example request**

```bash
curl -X DELETE "https://us.portal.patchmypc.com/v1/api/apps/{productId}/deployments/{deploymentId}?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

### Get application deployment dependency candidates

Lists the existing deployments in the given connection that you can pick as a dependency for a new or edited deployment. Every deployment in the connection is returned; filter the results on the client.

Operation ID: `GetApplicationDeploymentDependencyCandidates`

```http
GET /v1/api/apps/{productId}/deployments/dependency-candidates
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your read limit.

**Parameters**

| Name           | In    | Type          | Required | Description |
| -------------- | ----- | ------------- | -------- | ----------- |
| `productId`    | path  | string (uuid) | Yes      |             |
| `connectionId` | query | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body                                                                          |
| ------ | --------------------- | ----------------------------------------------------------------------------- |
| `200`  | OK                    | array of [`DeploymentDependencyDto`](applications.md#deploymentdependencydto) |
| `400`  | Bad Request           | string                                                                        |
| `401`  | Unauthorized          | None                                                                          |
| `403`  | Forbidden             | None                                                                          |
| `404`  | Not Found             | None                                                                          |
| `500`  | Internal Server Error | None                                                                          |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/apps/{productId}/deployments/dependency-candidates?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

### Redeploy application deployment

Forces a deployment to be recreated in Intune. Use it to troubleshoot a stuck or corrupted deployment; for routine version updates, use the sync operation instead.

Operation ID: `RedeployApplicationDeployment`

```http
PUT /v1/api/apps/{productId}/deployments/{deploymentId}/redeploy
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name           | In    | Type          | Required | Description |
| -------------- | ----- | ------------- | -------- | ----------- |
| `productId`    | path  | string (uuid) | Yes      |             |
| `deploymentId` | path  | string        | Yes      |             |
| `connectionId` | query | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body   |
| ------ | --------------------- | ------ |
| `200`  | OK                    | None   |
| `400`  | Bad Request           | string |
| `401`  | Unauthorized          | None   |
| `403`  | Forbidden             | None   |
| `404`  | Not Found             | None   |
| `500`  | Internal Server Error | None   |

**Example request**

```bash
curl -X PUT "https://us.portal.patchmypc.com/v1/api/apps/{productId}/deployments/{deploymentId}/redeploy?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

### Sync application deployment

Syncs a deployment to its latest pending version. Use it for routine version updates; to troubleshoot a stuck or corrupted deployment, use the redeploy operation instead.

Operation ID: `SyncApplicationDeployment`

```http
PUT /v1/api/apps/{productId}/deployments/{deploymentId}/sync
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name           | In    | Type          | Required | Description |
| -------------- | ----- | ------------- | -------- | ----------- |
| `productId`    | path  | string (uuid) | Yes      |             |
| `deploymentId` | path  | string        | Yes      |             |
| `connectionId` | query | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body   |
| ------ | --------------------- | ------ |
| `200`  | OK                    | None   |
| `400`  | Bad Request           | string |
| `401`  | Unauthorized          | None   |
| `403`  | Forbidden             | None   |
| `404`  | Not Found             | None   |
| `500`  | Internal Server Error | None   |

**Example request**

```bash
curl -X PUT "https://us.portal.patchmypc.com/v1/api/apps/{productId}/deployments/{deploymentId}/sync?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

### Set application deployment sync pause status

Pauses or resumes a deployment's scheduled sync.

Operation ID: `SetApplicationDeploymentSyncPauseStatus`

```http
PUT /v1/api/apps/{productId}/deployments/{deploymentId}/scheduled-sync-pause
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name           | In   | Type          | Required | Description |
| -------------- | ---- | ------------- | -------- | ----------- |
| `productId`    | path | string (uuid) | Yes      |             |
| `deploymentId` | path | string        | Yes      |             |

**Request body**

Required. Content type `application/json`. Type: `SetDeploymentSyncPauseRequest`.

| Name           | Type          | Required | Description |
| -------------- | ------------- | -------- | ----------- |
| `connectionId` | string (uuid) | No       |             |
| `pause`        | boolean       | No       |             |

**Responses**

| Status | Description           | Body   |
| ------ | --------------------- | ------ |
| `200`  | OK                    | None   |
| `400`  | Bad Request           | string |
| `401`  | Unauthorized          | None   |
| `403`  | Forbidden             | None   |
| `404`  | Not Found             | None   |
| `500`  | Internal Server Error | None   |

**Example request**

```bash
curl -X PUT "https://us.portal.patchmypc.com/v1/api/apps/{productId}/deployments/{deploymentId}/scheduled-sync-pause" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
  "connectionId": "{connectionId}",
  "pause": false
}'
```

## Deployment templates

### Get deployment templates

Lists the deployment templates configured for a connection, so you can find one and name it when you create a deployment. To author and change templates, use the create, update, and delete deployment template operations.

Operation ID: `GetDeploymentTemplates`

```http
GET /v1/api/deployments/templates
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your read limit.

**Parameters**

| Name           | In    | Type          | Required | Description |
| -------------- | ----- | ------------- | -------- | ----------- |
| `connectionId` | query | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body                                                                                    |
| ------ | --------------------- | --------------------------------------------------------------------------------------- |
| `200`  | OK                    | array of [`DeploymentTemplateSummaryDto`](applications.md#deploymenttemplatesummarydto) |
| `400`  | Bad Request           | string                                                                                  |
| `401`  | Unauthorized          | None                                                                                    |
| `403`  | Forbidden             | None                                                                                    |
| `500`  | Internal Server Error | None                                                                                    |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/deployments/templates?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

### Create deployment template

Creates a deployment template on a connection. Setting it as the default demotes the template that's currently the default.

Operation ID: `CreateDeploymentTemplate`

```http
POST /v1/api/deployments/templates
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your write limit.

**Request body**

Required. Content type `application/json`. Type: `DeploymentTemplateRequest`.

| Name                      | Type                                                                                                 | Required | Description    |
| ------------------------- | ---------------------------------------------------------------------------------------------------- | -------- | -------------- |
| `connectionId`            | string (uuid)                                                                                        | No       |                |
| `templateName`            | string                                                                                               | No       | Can be `null`. |
| `osType`                  | [`OSType`](applications.md#ostype)                                                                   | No       |                |
| `isDefault`               | boolean                                                                                              | No       |                |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                                     | No       |                |
| `allowAvailableUninstall` | boolean                                                                                              | No       |                |
| `removeDesktopShortcuts`  | boolean                                                                                              | No       |                |
| `appVersionsRetention`    | integer (int32)                                                                                      | No       |                |
| `customVendor`            | string                                                                                               | No       | Can be `null`. |
| `customDeveloper`         | string                                                                                               | No       | Can be `null`. |
| `customOwner`             | string                                                                                               | No       | Can be `null`. |
| `customNotes`             | string                                                                                               | No       | Can be `null`. |
| `copyForwardAssignments`  | boolean                                                                                              | No       |                |
| `categoryIds`             | array of string                                                                                      | No       | Can be `null`. |
| `espProfileIds`           | array of string                                                                                      | No       | Can be `null`. |
| `roleScopeTagIds`         | array of string                                                                                      | No       | Can be `null`. |
| `customRequirements`      | [`EditDeploymentCustomRequirementsRequest`](applications.md#editdeploymentcustomrequirementsrequest) | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                                             |
| ------ | --------------------- | ---------------------------------------------------------------- |
| `200`  | OK                    | [`DeploymentTemplateDto`](applications.md#deploymenttemplatedto) |
| `400`  | Bad Request           | string                                                           |
| `401`  | Unauthorized          | None                                                             |
| `403`  | Forbidden             | None                                                             |
| `500`  | Internal Server Error | None                                                             |

**Example request**

```bash
curl -X POST "https://us.portal.patchmypc.com/v1/api/deployments/templates" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

### Get deployment template details

Retrieves the settings that a deployment created from this template inherits.

Operation ID: `GetDeploymentTemplate`

```http
GET /v1/api/deployments/templates/{deploymentTemplateId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your read limit.

**Parameters**

| Name                   | In    | Type          | Required | Description |
| ---------------------- | ----- | ------------- | -------- | ----------- |
| `deploymentTemplateId` | path  | string        | Yes      |             |
| `connectionId`         | query | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body                                                             |
| ------ | --------------------- | ---------------------------------------------------------------- |
| `200`  | OK                    | [`DeploymentTemplateDto`](applications.md#deploymenttemplatedto) |
| `400`  | Bad Request           | string                                                           |
| `401`  | Unauthorized          | None                                                             |
| `403`  | Forbidden             | None                                                             |
| `404`  | Not Found             | None                                                             |
| `500`  | Internal Server Error | None                                                             |

**Example request**

```bash
curl "https://us.portal.patchmypc.com/v1/api/deployments/templates/{deploymentTemplateId}?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

### Update deployment template

Replaces the settings on an existing deployment template. Every field is stored as sent, so read the template first and change only what you need.

Operation ID: `UpdateDeploymentTemplate`

```http
PUT /v1/api/deployments/templates/{deploymentTemplateId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name                   | In   | Type   | Required | Description |
| ---------------------- | ---- | ------ | -------- | ----------- |
| `deploymentTemplateId` | path | string | Yes      |             |

**Request body**

Required. Content type `application/json`. Type: `DeploymentTemplateRequest`.

| Name                      | Type                                                                                                 | Required | Description    |
| ------------------------- | ---------------------------------------------------------------------------------------------------- | -------- | -------------- |
| `connectionId`            | string (uuid)                                                                                        | No       |                |
| `templateName`            | string                                                                                               | No       | Can be `null`. |
| `osType`                  | [`OSType`](applications.md#ostype)                                                                   | No       |                |
| `isDefault`               | boolean                                                                                              | No       |                |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                                     | No       |                |
| `allowAvailableUninstall` | boolean                                                                                              | No       |                |
| `removeDesktopShortcuts`  | boolean                                                                                              | No       |                |
| `appVersionsRetention`    | integer (int32)                                                                                      | No       |                |
| `customVendor`            | string                                                                                               | No       | Can be `null`. |
| `customDeveloper`         | string                                                                                               | No       | Can be `null`. |
| `customOwner`             | string                                                                                               | No       | Can be `null`. |
| `customNotes`             | string                                                                                               | No       | Can be `null`. |
| `copyForwardAssignments`  | boolean                                                                                              | No       |                |
| `categoryIds`             | array of string                                                                                      | No       | Can be `null`. |
| `espProfileIds`           | array of string                                                                                      | No       | Can be `null`. |
| `roleScopeTagIds`         | array of string                                                                                      | No       | Can be `null`. |
| `customRequirements`      | [`EditDeploymentCustomRequirementsRequest`](applications.md#editdeploymentcustomrequirementsrequest) | No       | Can be `null`. |

**Responses**

| Status | Description           | Body                                                             |
| ------ | --------------------- | ---------------------------------------------------------------- |
| `200`  | OK                    | [`DeploymentTemplateDto`](applications.md#deploymenttemplatedto) |
| `400`  | Bad Request           | string                                                           |
| `401`  | Unauthorized          | None                                                             |
| `403`  | Forbidden             | None                                                             |
| `404`  | Not Found             | None                                                             |
| `500`  | Internal Server Error | None                                                             |

**Example request**

```bash
curl -X PUT "https://us.portal.patchmypc.com/v1/api/deployments/templates/{deploymentTemplateId}" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d @request.json
```

### Delete deployment template

Deletes a deployment template. You can't delete the connection's default template—make another template the default first.

Operation ID: `DeleteDeploymentTemplate`

```http
DELETE /v1/api/deployments/templates/{deploymentTemplateId}
```

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

**Required PAT scope:** `appcatbroker:apps:deploy`

**Rate limit:** Counts against your write limit.

**Parameters**

| Name                   | In    | Type          | Required | Description |
| ---------------------- | ----- | ------------- | -------- | ----------- |
| `deploymentTemplateId` | path  | string        | Yes      |             |
| `connectionId`         | query | string (uuid) | Yes      |             |

**Responses**

| Status | Description           | Body   |
| ------ | --------------------- | ------ |
| `200`  | OK                    | None   |
| `400`  | Bad Request           | string |
| `401`  | Unauthorized          | None   |
| `403`  | Forbidden             | None   |
| `404`  | Not Found             | None   |
| `500`  | Internal Server Error | None   |

**Example request**

```bash
curl -X DELETE "https://us.portal.patchmypc.com/v1/api/deployments/templates/{deploymentTemplateId}?connectionId={connectionId}" \
  -H "Authorization: Bearer {access-token}"
```

## Schemas

The types used by the operations on this page. Property names are case-sensitive in responses and case-insensitive in requests.

### AdminConsentStatus

Type: string. One of the following values:

* `Unknown`
* `Pending`
* `Granted`
* `MissingPermissions`

### ApplicableArchitecture

Type: string. One of the following values:

* `None`
* `X86`
* `X64`
* `Arm`
* `Neutral`

### ApplicationCreationResponse

| Name                     | Type            | Required | Description    |
| ------------------------ | --------------- | -------- | -------------- |
| `updateId`               | string (uuid)   | No       |                |
| `revisionId`             | integer (int32) | No       |                |
| `productId`              | string (uuid)   | No       |                |
| `displayName`            | string          | No       | Can be `null`. |
| `customerId`             | string (uuid)   | No       |                |
| `fileUploadPath`         | string          | No       | Can be `null`. |
| `chunkedFileUploadPath`  | string          | No       | Can be `null`. |
| `fileCompleteUploadPath` | string          | No       | Can be `null`. |

### ApplicationFileDto

| Name         | Type                                               | Required | Description    |
| ------------ | -------------------------------------------------- | -------- | -------------- |
| `productId`  | string (uuid)                                      | No       |                |
| `fileName`   | string                                             | No       | Can be `null`. |
| `fileSize`   | integer (int64)                                    | No       |                |
| `fileType`   | [`UpdateFileType`](applications.md#updatefiletype) | No       |                |
| `sha1Hash`   | string                                             | No       | Can be `null`. |
| `sha256Hash` | string                                             | No       | Can be `null`. |

### AssignmentTargetType

Type: string. One of the following values:

* `AllUsers`
* `AllDevices`
* `Group`
* `NotSet`

### BlockingProcessMgmtPolicy

Type: string. One of the following values:

* `None`
* `Kill`
* `Skip`
* `Notify`

### BuiltInUpdate

Type: string. One of the following values:

* `NotAvailable`
* `Disable`
* `Enable`

### CatalogFeedType

Type: string. One of the following values:

* `Undefined`
* `PMPC`
* `SCAPPMAN`
* `CUSTOMER`
* `WSUS`
* `WINGET`

### ConnectionDto

| Name           | Type                                                       | Required | Description    |
| -------------- | ---------------------------------------------------------- | -------- | -------------- |
| `connectionId` | string (uuid)                                              | No       |                |
| `displayName`  | string                                                     | No       | Can be `null`. |
| `type`         | [`ConnectionType`](applications.md#connectiontype)         | No       |                |
| `adminConsent` | [`AdminConsentStatus`](applications.md#adminconsentstatus) | No       |                |

### ConnectionType

Type: string. One of the following values:

* `Unknown`
* `ConfigMgr`
* `Intune`
* `Publisher`

### CreateDeploymentAssignmentRequest

| Name         | Type                                                           | Required | Description    |
| ------------ | -------------------------------------------------------------- | -------- | -------------- |
| `groupId`    | string                                                         | No       | Can be `null`. |
| `intent`     | [`InstallationIntent`](applications.md#installationintent)     | No       |                |
| `targetType` | [`AssignmentTargetType`](applications.md#assignmenttargettype) | No       | Can be `null`. |

### CustomApplicationDetailsDto

| Name             | Type    | Required | Description               |
| ---------------- | ------- | -------- | ------------------------- |
| `isMigrationApp` | boolean | No       | Read-only. Can be `null`. |

### CustomApplicationDto

| Name                       | Type                                                                 | Required | Description               |
| -------------------------- | -------------------------------------------------------------------- | -------- | ------------------------- |
| `productId`                | string (uuid)                                                        | No       | Read-only.                |
| `type`                     | string                                                               | No       | Read-only. Can be `null`. |
| `displayName`              | string                                                               | No       | Read-only. Can be `null`. |
| `description`              | string                                                               | No       | Read-only. Can be `null`. |
| `language`                 | string                                                               | No       | Read-only. Can be `null`. |
| `vendorName`               | string                                                               | No       | Read-only. Can be `null`. |
| `updateVersion`            | string                                                               | No       | Read-only. Can be `null`. |
| `iconURL`                  | string                                                               | No       | Read-only. Can be `null`. |
| `iconBase64`               | string                                                               | No       | Read-only. Can be `null`. |
| `iconContentType`          | string                                                               | No       | Read-only. Can be `null`. |
| `privacyUrl`               | string                                                               | No       | Read-only. Can be `null`. |
| `informationUrl`           | string                                                               | No       | Read-only. Can be `null`. |
| `developer`                | string                                                               | No       | Read-only. Can be `null`. |
| `intuneNotes`              | string                                                               | No       | Read-only. Can be `null`. |
| `installerType`            | [`InstallerType`](applications.md#installertype)                     | No       | Read-only.                |
| `architecture`             | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | Read-only.                |
| `installContext`           | [`InstallationBehavior`](applications.md#installationbehavior)       | No       | Read-only. Can be `null`. |
| `actions`                  | array of string                                                      | No       | Read-only. Can be `null`. |
| `silentInstallArguments`   | string                                                               | No       | Read-only. Can be `null`. |
| `silentUninstallArguments` | string                                                               | No       | Read-only. Can be `null`. |
| `mainFile`                 | string                                                               | No       | Read-only. Can be `null`. |
| `conflictingProcessList`   | array of string                                                      | No       | Read-only. Can be `null`. |
| `detectionRules`           | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Read-only. Can be `null`. |
| `customRequirements`       | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Read-only. Can be `null`. |
| `arpDisplayNameMatch`      | string                                                               | No       | Read-only. Can be `null`. |
| `notes`                    | string                                                               | No       | Read-only. Can be `null`. |
| `owner`                    | string                                                               | No       | Read-only. Can be `null`. |
| `msiProductCode`           | string (uuid)                                                        | No       | Read-only. Can be `null`. |
| `isMigrationApp`           | boolean                                                              | No       | Read-only. Can be `null`. |

### CustomRequirementsDto

| Name                        | Type                                                                        | Required | Description    |
| --------------------------- | --------------------------------------------------------------------------- | -------- | -------------- |
| `applicableArchitectures`   | array of [`ApplicableArchitecture`](applications.md#applicablearchitecture) | No       | Can be `null`. |
| `minimumWindowsOSVersion`   | [`WindowsOSVersion`](applications.md#windowsosversion)                      | No       | Can be `null`. |
| `minimumNumberOfProcessors` | integer (int32)                                                             | No       | Can be `null`. |
| `minimumMemoryInMB`         | integer (int32)                                                             | No       | Can be `null`. |
| `minimumCpuSpeedInMHz`      | integer (int32)                                                             | No       | Can be `null`. |
| `requirementFileRules`      | array of [`FileRuleDto`](applications.md#fileruledto)                       | No       | Can be `null`. |
| `requirementRegistryRules`  | array of [`RegistryRuleDto`](applications.md#registryruledto)               | No       | Can be `null`. |
| `requirementsScriptRules`   | array of [`ScriptRuleDto`](applications.md#scriptruledto)                   | No       | Can be `null`. |

### CustomerInfoDto

| Name                       | Type                                                     | Required | Description               |
| -------------------------- | -------------------------------------------------------- | -------- | ------------------------- |
| `limits`                   | [`LimitDTO`](applications.md#limitdto)                   | No       | Read-only. Can be `null`. |
| `customerId`               | string (uuid)                                            | No       | Read-only.                |
| `customerName`             | string                                                   | No       | Read-only. Can be `null`. |
| `license`                  | [`GetLicenseDto`](applications.md#getlicensedto)         | No       | Read-only. Can be `null`. |
| `limitsProgress`           | [`CustomerLimitsDto`](applications.md#customerlimitsdto) | No       | Read-only. Can be `null`. |
| `macOSApplicationsEnabled` | boolean                                                  | No       | Read-only.                |

### CustomerLicense

Type: string. One of the following values:

* `None`
* `Basic`
* `Enterprise`
* `Enterprise_Plus`
* `Enterprise_Premium`
* `Intune`
* `Trial`
* `MSP`
* `MSP_Plus`

### CustomerLimitsDto

| Name                               | Type            | Required | Description |
| ---------------------------------- | --------------- | -------- | ----------- |
| `totalSizeMb`                      | number (double) | No       |             |
| `customAppsNumber`                 | integer (int64) | No       |             |
| `intuneDeploymentsWithFilesNumber` | integer (int64) | No       |             |

### CustomerType

Type: string. One of the following values:

* `None`
* `Customer`
* `Demo`
* `Donation`
* `NFR`
* `Trial`
* `PersonalLab`
* `LabTrial`

### DeferPolicy

Type: string. One of the following values:

* `Indefinitely`
* `Count`
* `Deadline`

### DeferPolicyDefaultAction

Type: string. One of the following values:

* `Snooze`
* `CloseAndUpdate`

### DeploymentAppInfoDto

| Name                   | Type    | Required | Description    |
| ---------------------- | ------- | -------- | -------------- |
| `customVendor`         | string  | No       | Can be `null`. |
| `customDeveloper`      | string  | No       | Can be `null`. |
| `customOwner`          | string  | No       | Can be `null`. |
| `customDescription`    | string  | No       | Can be `null`. |
| `customNotes`          | string  | No       | Can be `null`. |
| `customInformationUrl` | string  | No       | Can be `null`. |
| `customPrivacyUrl`     | string  | No       | Can be `null`. |
| `isFeatured`           | boolean | No       | Can be `null`. |

### DeploymentAssignmentDto

| Name         | Type                                                           | Required | Description    |
| ------------ | -------------------------------------------------------------- | -------- | -------------- |
| `groupId`    | string                                                         | No       | Can be `null`. |
| `groupName`  | string                                                         | No       | Can be `null`. |
| `targetType` | [`AssignmentTargetType`](applications.md#assignmenttargettype) | No       |                |
| `intent`     | [`InstallationIntent`](applications.md#installationintent)     | No       |                |

### DeploymentCategoryDto

| Name          | Type   | Required | Description    |
| ------------- | ------ | -------- | -------------- |
| `id`          | string | No       | Can be `null`. |
| `displayName` | string | No       | Can be `null`. |

### DeploymentConfigurationDto

| Name                      | Type                                                                                 | Required | Description    |
| ------------------------- | ------------------------------------------------------------------------------------ | -------- | -------------- |
| `additionalArgument`      | string                                                                               | No       | Can be `null`. |
| `installLoggingPath`      | string                                                                               | No       | Can be `null`. |
| `customRequirements`      | [`DeploymentCustomRequirementsDto`](applications.md#deploymentcustomrequirementsdto) | No       | Can be `null`. |
| `appInfo`                 | [`DeploymentAppInfoDto`](applications.md#deploymentappinfodto)                       | No       | Can be `null`. |
| `conflictingProcess`      | [`DeploymentConflictingProcessDto`](applications.md#deploymentconflictingprocessdto) | No       | Can be `null`. |
| `returnCodes`             | array of [`DeploymentReturnCodeDto`](applications.md#deploymentreturncodedto)        | No       | Can be `null`. |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                     | No       |                |
| `allowAvailableUninstall` | boolean                                                                              | No       |                |
| `removeDesktopShortcuts`  | boolean                                                                              | No       |                |
| `appVersionsRetention`    | integer (int32)                                                                      | No       |                |
| `roleScopeTags`           | array of [`DeploymentRoleScopeTagDto`](applications.md#deploymentrolescopetagdto)    | No       | Can be `null`. |

### DeploymentConfigurationRequest

| Name                      | Type                                                                                                 | Required | Description    |
| ------------------------- | ---------------------------------------------------------------------------------------------------- | -------- | -------------- |
| `additionalArgument`      | string                                                                                               | No       | Can be `null`. |
| `installLoggingPath`      | string                                                                                               | No       | Can be `null`. |
| `customRequirements`      | [`EditDeploymentCustomRequirementsRequest`](applications.md#editdeploymentcustomrequirementsrequest) | No       | Can be `null`. |
| `appInfo`                 | [`DeploymentAppInfoDto`](applications.md#deploymentappinfodto)                                       | No       | Can be `null`. |
| `conflictingProcess`      | [`DeploymentConflictingProcessDto`](applications.md#deploymentconflictingprocessdto)                 | No       | Can be `null`. |
| `returnCodes`             | array of [`DeploymentReturnCodeDto`](applications.md#deploymentreturncodedto)                        | No       | Can be `null`. |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                                     | No       | Can be `null`. |
| `allowAvailableUninstall` | boolean                                                                                              | No       | Can be `null`. |
| `removeDesktopShortcuts`  | boolean                                                                                              | No       | Can be `null`. |
| `appVersionsRetention`    | integer (int32)                                                                                      | No       | Can be `null`. |
| `roleScopeTagIds`         | array of string                                                                                      | No       | Can be `null`. |

### DeploymentConflictingProcessDto

| Name                               | Type                                                                             | Required | Description    |
| ---------------------------------- | -------------------------------------------------------------------------------- | -------- | -------------- |
| `policy`                           | [`BlockingProcessMgmtPolicy`](applications.md#blockingprocessmgmtpolicy)         | No       | Can be `null`. |
| `userAddedProcesses`               | array of string                                                                  | No       | Can be `null`. |
| `userDeletedProcesses`             | array of string                                                                  | No       | Can be `null`. |
| `preventConflictingProcessRestart` | boolean                                                                          | No       | Can be `null`. |
| `postDeploymentNotificationPolicy` | [`PostDeploymentNotification`](applications.md#postdeploymentnotification)       | No       | Can be `null`. |
| `snoozingNotificationDelaySeconds` | integer (int32)                                                                  | No       | Can be `null`. |
| `notification`                     | [`DeploymentUserNotificationDto`](applications.md#deploymentusernotificationdto) | No       | Can be `null`. |

### DeploymentCustomRequirementsDto

| Name                        | Type                                                                        | Required | Description    |
| --------------------------- | --------------------------------------------------------------------------- | -------- | -------------- |
| `disableArchitectures`      | array of [`ApplicableArchitecture`](applications.md#applicablearchitecture) | No       | Can be `null`. |
| `minimumWindowsOSVersion`   | [`WindowsOSVersion`](applications.md#windowsosversion)                      | No       | Can be `null`. |
| `minimumNumberOfProcessors` | integer (int32)                                                             | No       | Can be `null`. |
| `minimumMemoryInMB`         | integer (int32)                                                             | No       | Can be `null`. |
| `minimumCpuSpeedInMHz`      | integer (int32)                                                             | No       | Can be `null`. |
| `fileRules`                 | array of [`FileRuleDto`](applications.md#fileruledto)                       | No       | Can be `null`. |
| `registryRules`             | array of [`RegistryRuleDto`](applications.md#registryruledto)               | No       | Can be `null`. |
| `scriptRules`               | array of [`ScriptRuleDto`](applications.md#scriptruledto)                   | No       | Can be `null`. |

### DeploymentDeferralPolicyDto

| Name            | Type                                                                   | Required | Description    |
| --------------- | ---------------------------------------------------------------------- | -------- | -------------- |
| `policy`        | [`DeferPolicy`](applications.md#deferpolicy)                           | No       | Can be `null`. |
| `defaultAction` | [`DeferPolicyDefaultAction`](applications.md#deferpolicydefaultaction) | No       | Can be `null`. |
| `deferCount`    | integer (int32)                                                        | No       | Can be `null`. |
| `deadline`      | integer (int32)                                                        | No       | Can be `null`. |

### DeploymentDependencyDto

| Name              | Type                                                 | Required | Description    |
| ----------------- | ---------------------------------------------------- | -------- | -------------- |
| `id`              | string                                               | No       | Can be `null`. |
| `deploymentId`    | string                                               | No       | Can be `null`. |
| `name`            | string                                               | No       | Can be `null`. |
| `iconUrl`         | string                                               | No       | Can be `null`. |
| `catalogFeedType` | [`CatalogFeedType`](applications.md#catalogfeedtype) | No       |                |

### DeploymentDetailDto

| Name                | Type                                                                          | Required | Description    |
| ------------------- | ----------------------------------------------------------------------------- | -------- | -------------- |
| `deploymentId`      | string                                                                        | No       | Can be `null`. |
| `productId`         | string (uuid)                                                                 | No       |                |
| `displayName`       | string                                                                        | No       | Can be `null`. |
| `osType`            | [`OSType`](applications.md#ostype)                                            | No       |                |
| `status`            | [`DeploymentStatusType`](applications.md#deploymentstatustype)                | No       |                |
| `warningMessages`   | array of string                                                               | No       | Can be `null`. |
| `syncOnHold`        | boolean                                                                       | No       |                |
| `ringsEnabled`      | boolean                                                                       | No       |                |
| `actions`           | array of string                                                               | No       | Can be `null`. |
| `errorMessages`     | array of string                                                               | No       | Can be `null`. |
| `categories`        | array of [`DeploymentCategoryDto`](applications.md#deploymentcategorydto)     | No       | Can be `null`. |
| `espProfiles`       | array of [`DeploymentEspProfileDto`](applications.md#deploymentespprofiledto) | No       | Can be `null`. |
| `assignments`       | array of [`DeploymentAssignmentDto`](applications.md#deploymentassignmentdto) | No       | Can be `null`. |
| `parentDeployments` | array of [`DeploymentDependencyDto`](applications.md#deploymentdependencydto) | No       | Can be `null`. |
| `childDeployments`  | array of [`DeploymentDependencyDto`](applications.md#deploymentdependencydto) | No       | Can be `null`. |
| `version`           | string                                                                        | No       | Can be `null`. |
| `configuration`     | [`DeploymentConfigurationDto`](applications.md#deploymentconfigurationdto)    | No       | Can be `null`. |

### DeploymentDto

| Name              | Type                                                           | Required | Description    |
| ----------------- | -------------------------------------------------------------- | -------- | -------------- |
| `deploymentId`    | string                                                         | No       | Can be `null`. |
| `productId`       | string (uuid)                                                  | No       |                |
| `displayName`     | string                                                         | No       | Can be `null`. |
| `osType`          | [`OSType`](applications.md#ostype)                             | No       |                |
| `status`          | [`DeploymentStatusType`](applications.md#deploymentstatustype) | No       |                |
| `warningMessages` | array of string                                                | No       | Can be `null`. |
| `syncOnHold`      | boolean                                                        | No       |                |
| `ringsEnabled`    | boolean                                                        | No       |                |
| `actions`         | array of string                                                | No       | Can be `null`. |

### DeploymentEspProfileDto

| Name                | Type            | Required | Description    |
| ------------------- | --------------- | -------- | -------------- |
| `id`                | string          | No       | Can be `null`. |
| `displayName`       | string          | No       | Can be `null`. |
| `applicationsCount` | integer (int32) | No       | Can be `null`. |

### DeploymentReturnCodeDto

| Name   | Type                                               | Required | Description |
| ------ | -------------------------------------------------- | -------- | ----------- |
| `code` | integer (int32)                                    | No       |             |
| `type` | [`ReturnCodeType`](applications.md#returncodetype) | No       |             |

### DeploymentRoleScopeTagDto

| Name          | Type   | Required | Description    |
| ------------- | ------ | -------- | -------------- |
| `id`          | string | No       | Can be `null`. |
| `displayName` | string | No       | Can be `null`. |

### DeploymentStatusType

Type: string. One of the following values:

* `InProgress`
* `Retrying`
* `Failed`
* `Success`
* `Scheduled`
* `Deleting`
* `DeletingFailed`
* `Deleted`

### DeploymentTemplateDto

| Name                      | Type                                                                                 | Required | Description    |
| ------------------------- | ------------------------------------------------------------------------------------ | -------- | -------------- |
| `deploymentTemplateId`    | string                                                                               | No       | Can be `null`. |
| `templateName`            | string                                                                               | No       | Can be `null`. |
| `isDefault`               | boolean                                                                              | No       |                |
| `osType`                  | [`OSType`](applications.md#ostype)                                                   | No       |                |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                     | No       |                |
| `allowAvailableUninstall` | boolean                                                                              | No       |                |
| `removeDesktopShortcuts`  | boolean                                                                              | No       |                |
| `appVersionsRetention`    | integer (int32)                                                                      | No       |                |
| `customVendor`            | string                                                                               | No       | Can be `null`. |
| `customDeveloper`         | string                                                                               | No       | Can be `null`. |
| `customOwner`             | string                                                                               | No       | Can be `null`. |
| `customNotes`             | string                                                                               | No       | Can be `null`. |
| `customRequirements`      | [`DeploymentCustomRequirementsDto`](applications.md#deploymentcustomrequirementsdto) | No       | Can be `null`. |
| `categories`              | array of [`DeploymentCategoryDto`](applications.md#deploymentcategorydto)            | No       | Can be `null`. |
| `espProfiles`             | array of [`DeploymentEspProfileDto`](applications.md#deploymentespprofiledto)        | No       | Can be `null`. |
| `roleScopeTags`           | array of [`DeploymentRoleScopeTagDto`](applications.md#deploymentrolescopetagdto)    | No       | Can be `null`. |
| `copyForwardAssignments`  | boolean                                                                              | No       |                |
| `actions`                 | array of string                                                                      | No       | Can be `null`. |

### DeploymentTemplateSummaryDto

| Name                   | Type                               | Required | Description    |
| ---------------------- | ---------------------------------- | -------- | -------------- |
| `deploymentTemplateId` | string                             | No       | Can be `null`. |
| `templateName`         | string                             | No       | Can be `null`. |
| `isDefault`            | boolean                            | No       |                |
| `osType`               | [`OSType`](applications.md#ostype) | No       |                |
| `createdAt`            | string (date-time)                 | No       |                |
| `lastModifiedAt`       | string (date-time)                 | No       |                |
| `actions`              | array of string                    | No       | Can be `null`. |

### DeploymentUserNotificationDto

| Name                   | Type                                                                         | Required | Description    |
| ---------------------- | ---------------------------------------------------------------------------- | -------- | -------------- |
| `policy`               | [`NotificationPolicy`](applications.md#notificationpolicy)                   | No       | Can be `null`. |
| `timeOutSeconds`       | integer (int32)                                                              | No       | Can be `null`. |
| `timeOutUseMaxRuntime` | boolean                                                                      | No       | Can be `null`. |
| `focusAssistPolicy`    | [`FocusAssistPolicy`](applications.md#focusassistpolicy)                     | No       | Can be `null`. |
| `defer`                | [`DeploymentDeferralPolicyDto`](applications.md#deploymentdeferralpolicydto) | No       | Can be `null`. |

### DetectionRuleType

Type: string. One of the following values:

* `None`
* `PMPC`
* `Script`
* `Manual`

### DetectionRulesDto

| Name              | Type                                                          | Required | Description    |
| ----------------- | ------------------------------------------------------------- | -------- | -------------- |
| `rulesType`       | [`DetectionRuleType`](applications.md#detectionruletype)      | No       |                |
| `productCodeRule` | [`MsiDetectionRuleDto`](applications.md#msidetectionruledto)  | No       | Can be `null`. |
| `fileSystemRules` | array of [`FileRuleDto`](applications.md#fileruledto)         | No       | Can be `null`. |
| `registryRules`   | array of [`RegistryRuleDto`](applications.md#registryruledto) | No       | Can be `null`. |
| `scriptRule`      | [`ScriptRuleDto`](applications.md#scriptruledto)              | No       | Can be `null`. |

### EditDeploymentCustomRequirementsRequest

| Name                        | Type                                                                        | Required | Description    |
| --------------------------- | --------------------------------------------------------------------------- | -------- | -------------- |
| `disableArchitectures`      | array of [`ApplicableArchitecture`](applications.md#applicablearchitecture) | No       | Can be `null`. |
| `minimumWindowsOSVersion`   | [`WindowsOSVersion`](applications.md#windowsosversion)                      | No       | Can be `null`. |
| `minimumNumberOfProcessors` | integer (int32)                                                             | No       | Can be `null`. |
| `minimumMemoryInMB`         | integer (int32)                                                             | No       | Can be `null`. |
| `minimumCpuSpeedInMHz`      | integer (int32)                                                             | No       | Can be `null`. |
| `fileRules`                 | array of [`FileRuleDto`](applications.md#fileruledto)                       | No       | Can be `null`. |
| `registryRules`             | array of [`RegistryRuleDto`](applications.md#registryruledto)               | No       | Can be `null`. |
| `scriptRules`               | array of [`ScriptRuleDto`](applications.md#scriptruledto)                   | No       | Can be `null`. |

### FileRuleDto

| Name                   | Type                                                             | Required | Description    |
| ---------------------- | ---------------------------------------------------------------- | -------- | -------------- |
| `operator`             | [`RuleOperator`](applications.md#ruleoperator)                   | No       |                |
| `path`                 | string                                                           | No       | Can be `null`. |
| `fileOrFolderName`     | string                                                           | No       | Can be `null`. |
| `check32BitOn64System` | boolean                                                          | No       |                |
| `operationType`        | [`FileRuleOperationType`](applications.md#fileruleoperationtype) | No       |                |
| `comparisonValue`      | string                                                           | No       | Can be `null`. |

### FileRuleOperationType

Type: string. One of the following values:

* `NotConfigured`
* `Exists`
* `ModifiedDate`
* `CreatedDate`
* `Version`
* `SizeInMB`
* `DoesNotExist`
* `SizeInBytes`
* `AppVersion`
* `UnknownFutureValue`

### FocusAssistPolicy

Type: string. One of the following values:

* `DiscardNotification`
* `ShowNotification`
* `ShowIfLastChance`

### GetLicenseDto

| Name                      | Type                                                                | Required | Description    |
| ------------------------- | ------------------------------------------------------------------- | -------- | -------------- |
| `customerId`              | string (uuid)                                                       | No       | Can be `null`. |
| `licenseId`               | string                                                              | No       | Can be `null`. |
| `devicesCount`            | integer (int64)                                                     | No       |                |
| `expirationDate`          | string (date-time)                                                  | No       |                |
| `subscriptionLevel`       | [`CustomerLicense`](applications.md#customerlicense)                | No       |                |
| `type`                    | [`CustomerType`](applications.md#customertype)                      | No       |                |
| `isSuspended`             | boolean                                                             | No       | Can be `null`. |
| `inheritedFrom`           | string (uuid)                                                       | No       | Can be `null`. |
| `connectionId`            | string                                                              | No       | Can be `null`. |
| `fromPublisherConnection` | boolean                                                             | No       | Can be `null`. |
| `showCases`               | array of [`LicenseShowCaseDto`](applications.md#licenseshowcasedto) | No       | Can be `null`. |

### InstallationBehavior

Type: string. One of the following values:

* `User`
* `System`
* `Any`

### InstallationIntent

Type: string. One of the following values:

* `Unknown`
* `UpdateOnly`
* `Available`
* `Required`
* `Uninstall`
* `AvailableWithoutEnrollment`
* `NoAssignmentsInstall`
* `NoAssignmentsUpdate`

### InstallerType

Type: string. One of the following values:

* `EXE`
* `MSI`
* `MSP`
* `PKG`
* `DMG`
* `PS1`
* `BAT`
* `CMD`
* `VBS`

### LicenseShowCaseDto

| Name                 | Type                                                 | Required | Description    |
| -------------------- | ---------------------------------------------------- | -------- | -------------- |
| `showCaseId`         | string                                               | No       | Can be `null`. |
| `featureLicense`     | [`CustomerLicense`](applications.md#customerlicense) | No       |                |
| `expiredAt`          | string (date-time)                                   | No       |                |
| `featureUniqueNames` | array of string                                      | No       | Can be `null`. |

### LimitDTO

| Name                               | Type                            | Required | Description    |
| ---------------------------------- | ------------------------------- | -------- | -------------- |
| `customAppsNumber`                 | integer (int64)                 | No       |                |
| `customAppSizeMb`                  | number (double)                 | No       |                |
| `totalSizeMb`                      | number (double)                 | No       |                |
| `publisherConnectionsNumber`       | integer (int64)                 | No       |                |
| `intuneDeploymentsNumber`          | integer (int64)                 | No       |                |
| `intuneDeploymentsWithFilesNumber` | integer (int64)                 | No       |                |
| `macOSIntuneDeploymentsNumber`     | integer (int64)                 | No       |                |
| `rateLimits`                       | object (map of integer (int32)) | No       | Can be `null`. |

### MsiDetectionRuleDto

| Name             | Type                                           | Required | Description    |
| ---------------- | ---------------------------------------------- | -------- | -------------- |
| `operator`       | [`RuleOperator`](applications.md#ruleoperator) | No       |                |
| `productCode`    | string                                         | No       | Can be `null`. |
| `productVersion` | string                                         | No       | Can be `null`. |

### NotificationPolicy

Type: string. One of the following values:

* `AllowDefer`
* `AutoClose`

### OSType

Type: string. One of the following values:

* `Windows`
* `MacOS`

### PmpcApplicationDetailsDto

Type: object.

### PostDeploymentNotification

Type: string. One of the following values:

* `DoNotShow`
* `AlwaysShow`
* `ShowIfProcessClosed`

### ProductDto

| Name                       | Type                                                                         | Required | Description               |
| -------------------------- | ---------------------------------------------------------------------------- | -------- | ------------------------- |
| `productId`                | string (uuid)                                                                | No       | Read-only.                |
| `type`                     | string                                                                       | No       | Read-only. Can be `null`. |
| `pmpc`                     | [`PmpcApplicationDetailsDto`](applications.md#pmpcapplicationdetailsdto)     | No       | Read-only. Can be `null`. |
| `custom`                   | [`CustomApplicationDetailsDto`](applications.md#customapplicationdetailsdto) | No       | Read-only. Can be `null`. |
| `winget`                   | [`WingetApplicationDetailsDto`](applications.md#wingetapplicationdetailsdto) | No       | Read-only. Can be `null`. |
| `actions`                  | array of string                                                              | No       | Read-only. Can be `null`. |
| `displayName`              | string                                                                       | No       | Read-only. Can be `null`. |
| `description`              | string                                                                       | No       | Read-only. Can be `null`. |
| `language`                 | string                                                                       | No       | Read-only. Can be `null`. |
| `vendorName`               | string                                                                       | No       | Read-only. Can be `null`. |
| `silentInstallArguments`   | string                                                                       | No       | Read-only. Can be `null`. |
| `mainFile`                 | string                                                                       | No       | Read-only. Can be `null`. |
| `architecture`             | [`RequirementArchitecture`](applications.md#requirementarchitecture)         | No       | Read-only.                |
| `installerType`            | [`InstallerType`](applications.md#installertype)                             | No       | Read-only.                |
| `updateVersion`            | string                                                                       | No       | Read-only. Can be `null`. |
| `installContext`           | [`InstallationBehavior`](applications.md#installationbehavior)               | No       | Read-only. Can be `null`. |
| `conflictingProcessList`   | array of string                                                              | No       | Read-only. Can be `null`. |
| `notes`                    | string                                                                       | No       | Read-only. Can be `null`. |
| `detectionRules`           | [`DetectionRulesDto`](applications.md#detectionrulesdto)                     | No       | Read-only. Can be `null`. |
| `customRequirements`       | [`CustomRequirementsDto`](applications.md#customrequirementsdto)             | No       | Read-only. Can be `null`. |
| `arpDisplayNameMatch`      | string                                                                       | No       | Read-only. Can be `null`. |
| `msiProductCode`           | string (uuid)                                                                | No       | Read-only. Can be `null`. |
| `iconURL`                  | string                                                                       | No       | Read-only. Can be `null`. |
| `iconBase64`               | string                                                                       | No       | Read-only. Can be `null`. |
| `iconContentType`          | string                                                                       | No       | Read-only. Can be `null`. |
| `silentUninstallArguments` | string                                                                       | No       | Read-only. Can be `null`. |
| `privacyUrl`               | string                                                                       | No       | Read-only. Can be `null`. |
| `informationUrl`           | string                                                                       | No       | Read-only. Can be `null`. |
| `intuneNotes`              | string                                                                       | No       | Read-only. Can be `null`. |
| `developer`                | string                                                                       | No       | Read-only. Can be `null`. |
| `owner`                    | string                                                                       | No       | Read-only. Can be `null`. |

### ProductFilterResponse

| Name                  | Type                                                              | Required | Description    |
| --------------------- | ----------------------------------------------------------------- | -------- | -------------- |
| `totalAmount`         | integer (int64)                                                   | No       |                |
| `totalVariantsAmount` | integer (int64)                                                   | No       |                |
| `products`            | array of [`ProductSummaryDto`](applications.md#productsummarydto) | No       | Can be `null`. |

### ProductSummaryDto

| Name              | Type                                                                         | Required | Description               |
| ----------------- | ---------------------------------------------------------------------------- | -------- | ------------------------- |
| `id`              | string (uuid)                                                                | No       |                           |
| `productId`       | string (uuid)                                                                | No       |                           |
| `type`            | string                                                                       | No       | Can be `null`.            |
| `pmpc`            | [`PmpcApplicationDetailsDto`](applications.md#pmpcapplicationdetailsdto)     | No       | Can be `null`.            |
| `custom`          | [`CustomApplicationDetailsDto`](applications.md#customapplicationdetailsdto) | No       | Can be `null`.            |
| `winget`          | [`WingetApplicationDetailsDto`](applications.md#wingetapplicationdetailsdto) | No       | Can be `null`.            |
| `actions`         | array of string                                                              | No       | Can be `null`.            |
| `updateId`        | string (uuid)                                                                | No       |                           |
| `displayName`     | string                                                                       | No       | Can be `null`.            |
| `description`     | string                                                                       | No       | Can be `null`.            |
| `vendorName`      | string                                                                       | No       | Can be `null`.            |
| `language`        | string                                                                       | No       | Can be `null`.            |
| `iconURL`         | string                                                                       | No       | Can be `null`.            |
| `iconBase64`      | string                                                                       | No       | Can be `null`.            |
| `iconContentType` | string                                                                       | No       | Can be `null`.            |
| `state`           | [`UpdateState`](applications.md#updatestate)                                 | No       |                           |
| `lastUpdated`     | string (date-time)                                                           | No       |                           |
| `version`         | string                                                                       | No       | Read-only. Can be `null`. |

### PublicApplicationDto

| Name              | Type                                                                 | Required | Description               |
| ----------------- | -------------------------------------------------------------------- | -------- | ------------------------- |
| `productId`       | string (uuid)                                                        | No       | Read-only.                |
| `type`            | string                                                               | No       | Read-only. Can be `null`. |
| `displayName`     | string                                                               | No       | Read-only. Can be `null`. |
| `description`     | string                                                               | No       | Read-only. Can be `null`. |
| `language`        | string                                                               | No       | Read-only. Can be `null`. |
| `vendorName`      | string                                                               | No       | Read-only. Can be `null`. |
| `updateVersion`   | string                                                               | No       | Read-only. Can be `null`. |
| `iconURL`         | string                                                               | No       | Read-only. Can be `null`. |
| `iconBase64`      | string                                                               | No       | Read-only. Can be `null`. |
| `iconContentType` | string                                                               | No       | Read-only. Can be `null`. |
| `privacyUrl`      | string                                                               | No       | Read-only. Can be `null`. |
| `informationUrl`  | string                                                               | No       | Read-only. Can be `null`. |
| `developer`       | string                                                               | No       | Read-only. Can be `null`. |
| `intuneNotes`     | string                                                               | No       | Read-only. Can be `null`. |
| `installerType`   | [`InstallerType`](applications.md#installertype)                     | No       | Read-only.                |
| `architecture`    | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | Read-only.                |
| `installContext`  | [`InstallationBehavior`](applications.md#installationbehavior)       | No       | Read-only. Can be `null`. |
| `actions`         | array of string                                                      | No       | Read-only. Can be `null`. |

### RegistryRuleDto

| Name                   | Type                                                                     | Required | Description    |
| ---------------------- | ------------------------------------------------------------------------ | -------- | -------------- |
| `operator`             | [`RuleOperator`](applications.md#ruleoperator)                           | No       |                |
| `check32BitOn64System` | boolean                                                                  | No       |                |
| `keyPath`              | string                                                                   | No       | Can be `null`. |
| `valueName`            | string                                                                   | No       | Can be `null`. |
| `operationType`        | [`RegistryRuleOperationType`](applications.md#registryruleoperationtype) | No       |                |
| `comparisonValue`      | string                                                                   | No       | Can be `null`. |

### RegistryRuleOperationType

Type: string. One of the following values:

* `NotConfigured`
* `Exists`
* `DoesNotExist`
* `String`
* `Integer`
* `Version`
* `AppVersion`
* `UnknownFutureValue`

### RequirementArchitecture

Type: string. One of the following values:

* `Unspecified`
* `x64`
* `x86`
* `ARM`
* `Universal`

### ReturnCodeType

Type: string. One of the following values:

* `Success`
* `Retry`
* `HardReboot`
* `SoftReboot`
* `Failed`

### RuleOperator

Type: string. One of the following values:

* `NotConfigured`
* `Equal`
* `NotEqual`
* `GreaterThan`
* `GreaterThanOrEqual`
* `LessThan`
* `LessThanOrEqual`

### ScriptRuleDto

| Name                    | Type                                                                 | Required | Description    |
| ----------------------- | -------------------------------------------------------------------- | -------- | -------------- |
| `operator`              | [`RuleOperator`](applications.md#ruleoperator)                       | No       |                |
| `displayName`           | string                                                               | No       | Can be `null`. |
| `runAsAccount`          | boolean                                                              | No       | Can be `null`. |
| `comparisonValue`       | string                                                               | No       | Can be `null`. |
| `enforceSignatureCheck` | boolean                                                              | No       |                |
| `runAs32Bit`            | boolean                                                              | No       |                |
| `scriptContent`         | string                                                               | No       | Can be `null`. |
| `operationType`         | [`ScriptRuleOperationType`](applications.md#scriptruleoperationtype) | No       |                |

### ScriptRuleOperationType

Type: string. One of the following values:

* `NotConfigured`
* `String`
* `DateTime`
* `Integer`
* `Float`
* `Version`
* `Boolean`

### SqlSearchTarget

Type: string. One of the following values:

* `Target32Bit`
* `Target64Bit`
* `TargetDefault`

### UpdateFileType

Type: string. One of the following values:

* `Unspecified`
* `Installation`
* `Extra`
* `Zip`
* `MST`
* `AdditionalConfig`

### UpdateState

Type: string. One of the following values:

* `Undefined`
* `Uploading`
* `Uploaded`
* `UploadFailed`
* `HashMismatch`
* `Verified`
* `VerificationFailed`
* `Transferred`
* `TransferFailed`
* `Archived`
* `ArchiveFailed`
* `SuccessfullyCompleted`

### WindowsOSVersion

Type: string. One of the following values:

* `None`
* `V8_0`
* `V8_1`
* `V10_0`
* `Windows10_1607`
* `Windows10_1703`
* `Windows10_1709`
* `Windows10_1803`
* `Windows10_1809`
* `Windows10_1903`
* `Windows10_1909`
* `Windows10_2004`
* `Windows10_20H2`
* `Windows10_21H1`
* `Windows10_21H2`
* `Windows10_22H2`
* `Windows11_21H2`
* `Windows11_22H2`
* `Windows11_23H2`
* `Windows11_24H2`

### WingetApplicationDetailsDto

Type: object.

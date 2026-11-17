---
description: >-
  Reference for the Applications operations of the Patch My PC Cloud Customer
  API, with parameters, request and response schemas, and examples.
noIndex: true
noRobotsIndex: true
---

# Applications

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

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

| Name                      | Type                                                                          | Required | Description                                                                                                                                                                                                                                                                                                                    |
| ------------------------- | ----------------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `vendorIds`               | array of string (uuid)                                                        | No       | Return only applications from these publishers, identified by vendor ID. Can be `null`.                                                                                                                                                                                                                                        |
| `languages`               | array of string                                                               | No       | Return only applications in these languages, for example `en-US`. Can be `null`.                                                                                                                                                                                                                                               |
| `architectures`           | array of [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | Return only applications for these processor architectures. Can be `null`.                                                                                                                                                                                                                                                     |
| `osType`                  | [`OSType`](applications.md#ostype)                                            | No       | The operating system to search: `Windows` or `MacOS`. Defaults to `Windows`. macOS results from the Patch My PC catalog are returned only when your account has the macOS Applications feature; otherwise the search returns no results. Searches of your custom applications are not affected by this feature. Can be `null`. |
| `feedTypes`               | array of [`CatalogFeedType`](applications.md#catalogfeedtype)                 | No       | The catalog feeds to search. Each search endpoint sets this from its route, so any value you send is ignored: `/apps/search` and `/apps/custom/search` search your custom applications, and `/apps/public/search` searches the Patch My PC catalog. Can be `null`.                                                             |
| `connectionId`            | string (uuid)                                                                 | No       | The ID of the Intune connection that scopes the search. Required when searching the Patch My PC catalog; not needed when searching your custom applications. Can be `null`.                                                                                                                                                    |
| `lastModifiedFromUtc`     | string (date-time)                                                            | No       | The start of the last-modified date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                 |
| `lastModifiedToUtc`       | string (date-time)                                                            | No       | The end of the last-modified date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                   |
| `lastUpdatedFromUtc`      | string (date-time)                                                            | No       | The start of the last-updated date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                  |
| `lastUpdatedToUtc`        | string (date-time)                                                            | No       | The end of the last-updated date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                    |
| `displayNameSearchString` | string                                                                        | No       | Text to search for in application display names. Can be `null`.                                                                                                                                                                                                                                                                |
| `skip`                    | integer (int32)                                                               | No       | Number of matching products to skip before returning the page.                                                                                                                                                                                                                                                                 |
| `limit`                   | integer (int32)                                                               | No       | Maximum number of matching products to return. Defaults to 50.                                                                                                                                                                                                                                                                 |
| `sortField`               | string                                                                        | No       | The application property to sort matching results by, such as `DisplayName`. Defaults to `DisplayName`. Can be `null`.                                                                                                                                                                                                         |
| `ascending`               | boolean                                                                       | No       | Whether to sort results in ascending order. Defaults to `true`.                                                                                                                                                                                                                                                                |
| `includeIconData`         | boolean                                                                       | No       | Whether to include each application's icon image in `iconBase64` and `iconContentType`. Defaults to `false`. Including icons makes the search slower.                                                                                                                                                                          |

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

| Name        | Type          | Required | Description                                                                                                 |
| ----------- | ------------- | -------- | ----------------------------------------------------------------------------------------------------------- |
| `productId` | string (uuid) | No       | The ID of the application to create the draft for.                                                          |
| `updateId`  | string (uuid) | No       | The ID of the version (update) to edit. Used only when creating an edit draft; ignored for an update draft. |

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

| Name                      | Type                                                                 | Required | Description                                                                                                                                                                                                                   |
| ------------------------- | -------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | The processor architecture a device must have to install the application.                                                                                                                                                     |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       | Which registry architecture to search when detecting the installed application by its Add/Remove Programs (ARP) entry. `TargetDefault` searches all architectures.                                                            |
| `arpDisplayNameMatch`     | string                                                               | No       | A pattern that matches the application's display name in Add/Remove Programs (ARP), used to detect whether the application is installed. Required when creating an application. Can be `null`.                                |
| `arpVersionMatch`         | string                                                               | No       | The version of the application this draft publishes, as shown in its Add/Remove Programs (ARP) entry. Returned as `updateVersion` in the application details. Can be `null`.                                                  |
| `conflictingProcesses`    | array of string                                                      | No       | The names of processes that conflict with installing the application. Can be `null`.                                                                                                                                          |
| `description`             | string                                                               | No       | A description of the application. Can be `null`.                                                                                                                                                                              |
| `displayName`             | string                                                               | No       | The application's display name. Required when creating or editing an application. Can be `null`.                                                                                                                              |
| `documentationURL`        | string                                                               | No       | The URL of the application's documentation. Optional, and used only when creating an application. Can be `null`.                                                                                                              |
| `privacyURL`              | string                                                               | No       | The URL of the application's privacy policy. Optional. Can be `null`.                                                                                                                                                         |
| `informationURL`          | string                                                               | No       | The URL of a web page with more information about the application. Optional. Can be `null`.                                                                                                                                   |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       | The context the application installs in, for example `System` or `User`.                                                                                                                                                      |
| `language`                | string                                                               | No       | The application's language code, for example `en-US`. Can be `null`.                                                                                                                                                          |
| `notes`                   | string                                                               | No       | Notes about the application. Optional. Can be `null`.                                                                                                                                                                         |
| `intuneNotes`             | string                                                               | No       | Notes to include with the application in Microsoft Intune. Optional. Can be `null`.                                                                                                                                           |
| `publisher`               | string                                                               | No       | The name of the application's publisher. Required when creating or editing an application. It is matched against your existing publishers ignoring case, and a new publisher is created if none matches. Can be `null`.       |
| `developer`               | string                                                               | No       | The application's developer. Optional. Can be `null`.                                                                                                                                                                         |
| `owner`                   | string                                                               | No       | The application's owner. Optional. Can be `null`.                                                                                                                                                                             |
| `updateId`                | string (uuid)                                                        | No       | The ID of the version (update) to complete, as returned by the draft endpoint. Required.                                                                                                                                      |
| `productId`               | string (uuid)                                                        | No       | The application's ID, as returned by the draft endpoint. Required when adding a new version or editing an application.                                                                                                        |
| `msiProductCode`          | string (uuid)                                                        | No       | The MSI product code (a GUID) of the application's installer. When set, the application is treated as an MSI installer; when `null`, it is treated as an EXE installer. Can be `null`.                                        |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Custom rules that detect whether the application is installed. When `null`, detection is based on `msiProductCode`, `arpDisplayNameMatch` and `arpVersionMatch`. Can be `null`.                                               |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Custom requirement rules a device must meet before the application installs. When `null`, requirements are based on `requirementArchitecture` only. Can be `null`.                                                            |
| `revisionId`              | integer (int32)                                                      | No       | The revision ID returned by the draft endpoint.                                                                                                                                                                               |
| `iconUrl`                 | string                                                               | No       | The key of an uploaded icon file to use as the application's icon. Optional. Can be `null`.                                                                                                                                   |
| `folderPath`              | string                                                               | No       | The local folder that contains the application's files. Optional and informational only: the file paths in `files` and `primaryInstallerFile` are relative to this folder. Can be `null`.                                     |
| `primaryInstallerFile`    | string                                                               | No       | The path of the main installer file, relative to the application folder. Backslashes are converted to forward slashes, and the path is matched against the `fileName` values in `files`, ignoring case. Can be `null`.        |
| `cmdArguments`            | string                                                               | No       | The command-line arguments used to install the application silently. For an MSI installer, these are used as the MSI command line. Can be `null`.                                                                             |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Every file in the application version, including the main installer. When editing, this list replaces the existing files, so send the complete list. Requests that include restricted file names are rejected. Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | The command-line arguments used to uninstall the application silently. Optional. Can be `null`.                                                                                                                               |

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

| Name                      | Type                                                                 | Required | Description                                                                                                                                                                                                                   |
| ------------------------- | -------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | The processor architecture a device must have to install the application.                                                                                                                                                     |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       | Which registry architecture to search when detecting the installed application by its Add/Remove Programs (ARP) entry. `TargetDefault` searches all architectures.                                                            |
| `arpDisplayNameMatch`     | string                                                               | No       | A pattern that matches the application's display name in Add/Remove Programs (ARP), used to detect whether the application is installed. Required when creating an application. Can be `null`.                                |
| `arpVersionMatch`         | string                                                               | No       | The version of the application this draft publishes, as shown in its Add/Remove Programs (ARP) entry. Returned as `updateVersion` in the application details. Can be `null`.                                                  |
| `conflictingProcesses`    | array of string                                                      | No       | The names of processes that conflict with installing the application. Can be `null`.                                                                                                                                          |
| `description`             | string                                                               | No       | A description of the application. Can be `null`.                                                                                                                                                                              |
| `displayName`             | string                                                               | No       | The application's display name. Required when creating or editing an application. Can be `null`.                                                                                                                              |
| `documentationURL`        | string                                                               | No       | The URL of the application's documentation. Optional, and used only when creating an application. Can be `null`.                                                                                                              |
| `privacyURL`              | string                                                               | No       | The URL of the application's privacy policy. Optional. Can be `null`.                                                                                                                                                         |
| `informationURL`          | string                                                               | No       | The URL of a web page with more information about the application. Optional. Can be `null`.                                                                                                                                   |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       | The context the application installs in, for example `System` or `User`.                                                                                                                                                      |
| `language`                | string                                                               | No       | The application's language code, for example `en-US`. Can be `null`.                                                                                                                                                          |
| `notes`                   | string                                                               | No       | Notes about the application. Optional. Can be `null`.                                                                                                                                                                         |
| `intuneNotes`             | string                                                               | No       | Notes to include with the application in Microsoft Intune. Optional. Can be `null`.                                                                                                                                           |
| `publisher`               | string                                                               | No       | The name of the application's publisher. Required when creating or editing an application. It is matched against your existing publishers ignoring case, and a new publisher is created if none matches. Can be `null`.       |
| `developer`               | string                                                               | No       | The application's developer. Optional. Can be `null`.                                                                                                                                                                         |
| `owner`                   | string                                                               | No       | The application's owner. Optional. Can be `null`.                                                                                                                                                                             |
| `updateId`                | string (uuid)                                                        | No       | The ID of the version (update) to complete, as returned by the draft endpoint. Required.                                                                                                                                      |
| `productId`               | string (uuid)                                                        | No       | The application's ID, as returned by the draft endpoint. Required when adding a new version or editing an application.                                                                                                        |
| `msiProductCode`          | string (uuid)                                                        | No       | The MSI product code (a GUID) of the application's installer. When set, the application is treated as an MSI installer; when `null`, it is treated as an EXE installer. Can be `null`.                                        |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Custom rules that detect whether the application is installed. When `null`, detection is based on `msiProductCode`, `arpDisplayNameMatch` and `arpVersionMatch`. Can be `null`.                                               |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Custom requirement rules a device must meet before the application installs. When `null`, requirements are based on `requirementArchitecture` only. Can be `null`.                                                            |
| `revisionId`              | integer (int32)                                                      | No       | The revision ID returned by the draft endpoint.                                                                                                                                                                               |
| `iconUrl`                 | string                                                               | No       | The key of an uploaded icon file to use as the application's icon. Optional. Can be `null`.                                                                                                                                   |
| `folderPath`              | string                                                               | No       | The local folder that contains the application's files. Optional and informational only: the file paths in `files` and `primaryInstallerFile` are relative to this folder. Can be `null`.                                     |
| `primaryInstallerFile`    | string                                                               | No       | The path of the main installer file, relative to the application folder. Backslashes are converted to forward slashes, and the path is matched against the `fileName` values in `files`, ignoring case. Can be `null`.        |
| `cmdArguments`            | string                                                               | No       | The command-line arguments used to install the application silently. For an MSI installer, these are used as the MSI command line. Can be `null`.                                                                             |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Every file in the application version, including the main installer. When editing, this list replaces the existing files, so send the complete list. Requests that include restricted file names are rejected. Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | The command-line arguments used to uninstall the application silently. Optional. Can be `null`.                                                                                                                               |

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

| Name        | Type          | Required | Description                                                                                                 |
| ----------- | ------------- | -------- | ----------------------------------------------------------------------------------------------------------- |
| `productId` | string (uuid) | No       | The ID of the application to create the draft for.                                                          |
| `updateId`  | string (uuid) | No       | The ID of the version (update) to edit. Used only when creating an edit draft; ignored for an update draft. |

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

| Name                      | Type                                                                 | Required | Description                                                                                                                                                                                                                   |
| ------------------------- | -------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | The processor architecture a device must have to install the application.                                                                                                                                                     |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       | Which registry architecture to search when detecting the installed application by its Add/Remove Programs (ARP) entry. `TargetDefault` searches all architectures.                                                            |
| `arpDisplayNameMatch`     | string                                                               | No       | A pattern that matches the application's display name in Add/Remove Programs (ARP), used to detect whether the application is installed. Required when creating an application. Can be `null`.                                |
| `arpVersionMatch`         | string                                                               | No       | The version of the application this draft publishes, as shown in its Add/Remove Programs (ARP) entry. Returned as `updateVersion` in the application details. Can be `null`.                                                  |
| `conflictingProcesses`    | array of string                                                      | No       | The names of processes that conflict with installing the application. Can be `null`.                                                                                                                                          |
| `description`             | string                                                               | No       | A description of the application. Can be `null`.                                                                                                                                                                              |
| `displayName`             | string                                                               | No       | The application's display name. Required when creating or editing an application. Can be `null`.                                                                                                                              |
| `documentationURL`        | string                                                               | No       | The URL of the application's documentation. Optional, and used only when creating an application. Can be `null`.                                                                                                              |
| `privacyURL`              | string                                                               | No       | The URL of the application's privacy policy. Optional. Can be `null`.                                                                                                                                                         |
| `informationURL`          | string                                                               | No       | The URL of a web page with more information about the application. Optional. Can be `null`.                                                                                                                                   |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       | The context the application installs in, for example `System` or `User`.                                                                                                                                                      |
| `language`                | string                                                               | No       | The application's language code, for example `en-US`. Can be `null`.                                                                                                                                                          |
| `notes`                   | string                                                               | No       | Notes about the application. Optional. Can be `null`.                                                                                                                                                                         |
| `intuneNotes`             | string                                                               | No       | Notes to include with the application in Microsoft Intune. Optional. Can be `null`.                                                                                                                                           |
| `publisher`               | string                                                               | No       | The name of the application's publisher. Required when creating or editing an application. It is matched against your existing publishers ignoring case, and a new publisher is created if none matches. Can be `null`.       |
| `developer`               | string                                                               | No       | The application's developer. Optional. Can be `null`.                                                                                                                                                                         |
| `owner`                   | string                                                               | No       | The application's owner. Optional. Can be `null`.                                                                                                                                                                             |
| `updateId`                | string (uuid)                                                        | No       | The ID of the version (update) to complete, as returned by the draft endpoint. Required.                                                                                                                                      |
| `productId`               | string (uuid)                                                        | No       | The application's ID, as returned by the draft endpoint. Required when adding a new version or editing an application.                                                                                                        |
| `msiProductCode`          | string (uuid)                                                        | No       | The MSI product code (a GUID) of the application's installer. When set, the application is treated as an MSI installer; when `null`, it is treated as an EXE installer. Can be `null`.                                        |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Custom rules that detect whether the application is installed. When `null`, detection is based on `msiProductCode`, `arpDisplayNameMatch` and `arpVersionMatch`. Can be `null`.                                               |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Custom requirement rules a device must meet before the application installs. When `null`, requirements are based on `requirementArchitecture` only. Can be `null`.                                                            |
| `revisionId`              | integer (int32)                                                      | No       | The revision ID returned by the draft endpoint.                                                                                                                                                                               |
| `iconUrl`                 | string                                                               | No       | The key of an uploaded icon file to use as the application's icon. Optional. Can be `null`.                                                                                                                                   |
| `folderPath`              | string                                                               | No       | The local folder that contains the application's files. Optional and informational only: the file paths in `files` and `primaryInstallerFile` are relative to this folder. Can be `null`.                                     |
| `primaryInstallerFile`    | string                                                               | No       | The path of the main installer file, relative to the application folder. Backslashes are converted to forward slashes, and the path is matched against the `fileName` values in `files`, ignoring case. Can be `null`.        |
| `cmdArguments`            | string                                                               | No       | The command-line arguments used to install the application silently. For an MSI installer, these are used as the MSI command line. Can be `null`.                                                                             |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Every file in the application version, including the main installer. When editing, this list replaces the existing files, so send the complete list. Requests that include restricted file names are rejected. Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | The command-line arguments used to uninstall the application silently. Optional. Can be `null`.                                                                                                                               |

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

| Name                      | Type                                                                          | Required | Description                                                                                                                                                                                                                                                                                                                    |
| ------------------------- | ----------------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `vendorIds`               | array of string (uuid)                                                        | No       | Return only applications from these publishers, identified by vendor ID. Can be `null`.                                                                                                                                                                                                                                        |
| `languages`               | array of string                                                               | No       | Return only applications in these languages, for example `en-US`. Can be `null`.                                                                                                                                                                                                                                               |
| `architectures`           | array of [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | Return only applications for these processor architectures. Can be `null`.                                                                                                                                                                                                                                                     |
| `osType`                  | [`OSType`](applications.md#ostype)                                            | No       | The operating system to search: `Windows` or `MacOS`. Defaults to `Windows`. macOS results from the Patch My PC catalog are returned only when your account has the macOS Applications feature; otherwise the search returns no results. Searches of your custom applications are not affected by this feature. Can be `null`. |
| `feedTypes`               | array of [`CatalogFeedType`](applications.md#catalogfeedtype)                 | No       | The catalog feeds to search. Each search endpoint sets this from its route, so any value you send is ignored: `/apps/search` and `/apps/custom/search` search your custom applications, and `/apps/public/search` searches the Patch My PC catalog. Can be `null`.                                                             |
| `connectionId`            | string (uuid)                                                                 | No       | The ID of the Intune connection that scopes the search. Required when searching the Patch My PC catalog; not needed when searching your custom applications. Can be `null`.                                                                                                                                                    |
| `lastModifiedFromUtc`     | string (date-time)                                                            | No       | The start of the last-modified date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                 |
| `lastModifiedToUtc`       | string (date-time)                                                            | No       | The end of the last-modified date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                   |
| `lastUpdatedFromUtc`      | string (date-time)                                                            | No       | The start of the last-updated date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                  |
| `lastUpdatedToUtc`        | string (date-time)                                                            | No       | The end of the last-updated date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                    |
| `displayNameSearchString` | string                                                                        | No       | Text to search for in application display names. Can be `null`.                                                                                                                                                                                                                                                                |
| `skip`                    | integer (int32)                                                               | No       | Number of matching products to skip before returning the page.                                                                                                                                                                                                                                                                 |
| `limit`                   | integer (int32)                                                               | No       | Maximum number of matching products to return. Defaults to 50.                                                                                                                                                                                                                                                                 |
| `sortField`               | string                                                                        | No       | The application property to sort matching results by, such as `DisplayName`. Defaults to `DisplayName`. Can be `null`.                                                                                                                                                                                                         |
| `ascending`               | boolean                                                                       | No       | Whether to sort results in ascending order. Defaults to `true`.                                                                                                                                                                                                                                                                |
| `includeIconData`         | boolean                                                                       | No       | Whether to include each application's icon image in `iconBase64` and `iconContentType`. Defaults to `false`. Including icons makes the search slower.                                                                                                                                                                          |

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

| Name        | Type          | Required | Description                                                                                                 |
| ----------- | ------------- | -------- | ----------------------------------------------------------------------------------------------------------- |
| `productId` | string (uuid) | No       | The ID of the application to create the draft for.                                                          |
| `updateId`  | string (uuid) | No       | The ID of the version (update) to edit. Used only when creating an edit draft; ignored for an update draft. |

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

| Name                      | Type                                                                 | Required | Description                                                                                                                                                                                                                   |
| ------------------------- | -------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | The processor architecture a device must have to install the application.                                                                                                                                                     |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       | Which registry architecture to search when detecting the installed application by its Add/Remove Programs (ARP) entry. `TargetDefault` searches all architectures.                                                            |
| `arpDisplayNameMatch`     | string                                                               | No       | A pattern that matches the application's display name in Add/Remove Programs (ARP), used to detect whether the application is installed. Required when creating an application. Can be `null`.                                |
| `arpVersionMatch`         | string                                                               | No       | The version of the application this draft publishes, as shown in its Add/Remove Programs (ARP) entry. Returned as `updateVersion` in the application details. Can be `null`.                                                  |
| `conflictingProcesses`    | array of string                                                      | No       | The names of processes that conflict with installing the application. Can be `null`.                                                                                                                                          |
| `description`             | string                                                               | No       | A description of the application. Can be `null`.                                                                                                                                                                              |
| `displayName`             | string                                                               | No       | The application's display name. Required when creating or editing an application. Can be `null`.                                                                                                                              |
| `documentationURL`        | string                                                               | No       | The URL of the application's documentation. Optional, and used only when creating an application. Can be `null`.                                                                                                              |
| `privacyURL`              | string                                                               | No       | The URL of the application's privacy policy. Optional. Can be `null`.                                                                                                                                                         |
| `informationURL`          | string                                                               | No       | The URL of a web page with more information about the application. Optional. Can be `null`.                                                                                                                                   |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       | The context the application installs in, for example `System` or `User`.                                                                                                                                                      |
| `language`                | string                                                               | No       | The application's language code, for example `en-US`. Can be `null`.                                                                                                                                                          |
| `notes`                   | string                                                               | No       | Notes about the application. Optional. Can be `null`.                                                                                                                                                                         |
| `intuneNotes`             | string                                                               | No       | Notes to include with the application in Microsoft Intune. Optional. Can be `null`.                                                                                                                                           |
| `publisher`               | string                                                               | No       | The name of the application's publisher. Required when creating or editing an application. It is matched against your existing publishers ignoring case, and a new publisher is created if none matches. Can be `null`.       |
| `developer`               | string                                                               | No       | The application's developer. Optional. Can be `null`.                                                                                                                                                                         |
| `owner`                   | string                                                               | No       | The application's owner. Optional. Can be `null`.                                                                                                                                                                             |
| `updateId`                | string (uuid)                                                        | No       | The ID of the version (update) to complete, as returned by the draft endpoint. Required.                                                                                                                                      |
| `productId`               | string (uuid)                                                        | No       | The application's ID, as returned by the draft endpoint. Required when adding a new version or editing an application.                                                                                                        |
| `msiProductCode`          | string (uuid)                                                        | No       | The MSI product code (a GUID) of the application's installer. When set, the application is treated as an MSI installer; when `null`, it is treated as an EXE installer. Can be `null`.                                        |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Custom rules that detect whether the application is installed. When `null`, detection is based on `msiProductCode`, `arpDisplayNameMatch` and `arpVersionMatch`. Can be `null`.                                               |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Custom requirement rules a device must meet before the application installs. When `null`, requirements are based on `requirementArchitecture` only. Can be `null`.                                                            |
| `revisionId`              | integer (int32)                                                      | No       | The revision ID returned by the draft endpoint.                                                                                                                                                                               |
| `iconUrl`                 | string                                                               | No       | The key of an uploaded icon file to use as the application's icon. Optional. Can be `null`.                                                                                                                                   |
| `folderPath`              | string                                                               | No       | The local folder that contains the application's files. Optional and informational only: the file paths in `files` and `primaryInstallerFile` are relative to this folder. Can be `null`.                                     |
| `primaryInstallerFile`    | string                                                               | No       | The path of the main installer file, relative to the application folder. Backslashes are converted to forward slashes, and the path is matched against the `fileName` values in `files`, ignoring case. Can be `null`.        |
| `cmdArguments`            | string                                                               | No       | The command-line arguments used to install the application silently. For an MSI installer, these are used as the MSI command line. Can be `null`.                                                                             |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Every file in the application version, including the main installer. When editing, this list replaces the existing files, so send the complete list. Requests that include restricted file names are rejected. Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | The command-line arguments used to uninstall the application silently. Optional. Can be `null`.                                                                                                                               |

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

| Name                      | Type                                                                 | Required | Description                                                                                                                                                                                                                   |
| ------------------------- | -------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | The processor architecture a device must have to install the application.                                                                                                                                                     |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       | Which registry architecture to search when detecting the installed application by its Add/Remove Programs (ARP) entry. `TargetDefault` searches all architectures.                                                            |
| `arpDisplayNameMatch`     | string                                                               | No       | A pattern that matches the application's display name in Add/Remove Programs (ARP), used to detect whether the application is installed. Required when creating an application. Can be `null`.                                |
| `arpVersionMatch`         | string                                                               | No       | The version of the application this draft publishes, as shown in its Add/Remove Programs (ARP) entry. Returned as `updateVersion` in the application details. Can be `null`.                                                  |
| `conflictingProcesses`    | array of string                                                      | No       | The names of processes that conflict with installing the application. Can be `null`.                                                                                                                                          |
| `description`             | string                                                               | No       | A description of the application. Can be `null`.                                                                                                                                                                              |
| `displayName`             | string                                                               | No       | The application's display name. Required when creating or editing an application. Can be `null`.                                                                                                                              |
| `documentationURL`        | string                                                               | No       | The URL of the application's documentation. Optional, and used only when creating an application. Can be `null`.                                                                                                              |
| `privacyURL`              | string                                                               | No       | The URL of the application's privacy policy. Optional. Can be `null`.                                                                                                                                                         |
| `informationURL`          | string                                                               | No       | The URL of a web page with more information about the application. Optional. Can be `null`.                                                                                                                                   |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       | The context the application installs in, for example `System` or `User`.                                                                                                                                                      |
| `language`                | string                                                               | No       | The application's language code, for example `en-US`. Can be `null`.                                                                                                                                                          |
| `notes`                   | string                                                               | No       | Notes about the application. Optional. Can be `null`.                                                                                                                                                                         |
| `intuneNotes`             | string                                                               | No       | Notes to include with the application in Microsoft Intune. Optional. Can be `null`.                                                                                                                                           |
| `publisher`               | string                                                               | No       | The name of the application's publisher. Required when creating or editing an application. It is matched against your existing publishers ignoring case, and a new publisher is created if none matches. Can be `null`.       |
| `developer`               | string                                                               | No       | The application's developer. Optional. Can be `null`.                                                                                                                                                                         |
| `owner`                   | string                                                               | No       | The application's owner. Optional. Can be `null`.                                                                                                                                                                             |
| `updateId`                | string (uuid)                                                        | No       | The ID of the version (update) to complete, as returned by the draft endpoint. Required.                                                                                                                                      |
| `productId`               | string (uuid)                                                        | No       | The application's ID, as returned by the draft endpoint. Required when adding a new version or editing an application.                                                                                                        |
| `msiProductCode`          | string (uuid)                                                        | No       | The MSI product code (a GUID) of the application's installer. When set, the application is treated as an MSI installer; when `null`, it is treated as an EXE installer. Can be `null`.                                        |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Custom rules that detect whether the application is installed. When `null`, detection is based on `msiProductCode`, `arpDisplayNameMatch` and `arpVersionMatch`. Can be `null`.                                               |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Custom requirement rules a device must meet before the application installs. When `null`, requirements are based on `requirementArchitecture` only. Can be `null`.                                                            |
| `revisionId`              | integer (int32)                                                      | No       | The revision ID returned by the draft endpoint.                                                                                                                                                                               |
| `iconUrl`                 | string                                                               | No       | The key of an uploaded icon file to use as the application's icon. Optional. Can be `null`.                                                                                                                                   |
| `folderPath`              | string                                                               | No       | The local folder that contains the application's files. Optional and informational only: the file paths in `files` and `primaryInstallerFile` are relative to this folder. Can be `null`.                                     |
| `primaryInstallerFile`    | string                                                               | No       | The path of the main installer file, relative to the application folder. Backslashes are converted to forward slashes, and the path is matched against the `fileName` values in `files`, ignoring case. Can be `null`.        |
| `cmdArguments`            | string                                                               | No       | The command-line arguments used to install the application silently. For an MSI installer, these are used as the MSI command line. Can be `null`.                                                                             |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Every file in the application version, including the main installer. When editing, this list replaces the existing files, so send the complete list. Requests that include restricted file names are rejected. Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | The command-line arguments used to uninstall the application silently. Optional. Can be `null`.                                                                                                                               |

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

| Name        | Type          | Required | Description                                                                                                 |
| ----------- | ------------- | -------- | ----------------------------------------------------------------------------------------------------------- |
| `productId` | string (uuid) | No       | The ID of the application to create the draft for.                                                          |
| `updateId`  | string (uuid) | No       | The ID of the version (update) to edit. Used only when creating an edit draft; ignored for an update draft. |

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

| Name                      | Type                                                                 | Required | Description                                                                                                                                                                                                                   |
| ------------------------- | -------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `requirementArchitecture` | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | The processor architecture a device must have to install the application.                                                                                                                                                     |
| `architecture`            | [`SqlSearchTarget`](applications.md#sqlsearchtarget)                 | No       | Which registry architecture to search when detecting the installed application by its Add/Remove Programs (ARP) entry. `TargetDefault` searches all architectures.                                                            |
| `arpDisplayNameMatch`     | string                                                               | No       | A pattern that matches the application's display name in Add/Remove Programs (ARP), used to detect whether the application is installed. Required when creating an application. Can be `null`.                                |
| `arpVersionMatch`         | string                                                               | No       | The version of the application this draft publishes, as shown in its Add/Remove Programs (ARP) entry. Returned as `updateVersion` in the application details. Can be `null`.                                                  |
| `conflictingProcesses`    | array of string                                                      | No       | The names of processes that conflict with installing the application. Can be `null`.                                                                                                                                          |
| `description`             | string                                                               | No       | A description of the application. Can be `null`.                                                                                                                                                                              |
| `displayName`             | string                                                               | No       | The application's display name. Required when creating or editing an application. Can be `null`.                                                                                                                              |
| `documentationURL`        | string                                                               | No       | The URL of the application's documentation. Optional, and used only when creating an application. Can be `null`.                                                                                                              |
| `privacyURL`              | string                                                               | No       | The URL of the application's privacy policy. Optional. Can be `null`.                                                                                                                                                         |
| `informationURL`          | string                                                               | No       | The URL of a web page with more information about the application. Optional. Can be `null`.                                                                                                                                   |
| `installContext`          | [`InstallationBehavior`](applications.md#installationbehavior)       | No       | The context the application installs in, for example `System` or `User`.                                                                                                                                                      |
| `language`                | string                                                               | No       | The application's language code, for example `en-US`. Can be `null`.                                                                                                                                                          |
| `notes`                   | string                                                               | No       | Notes about the application. Optional. Can be `null`.                                                                                                                                                                         |
| `intuneNotes`             | string                                                               | No       | Notes to include with the application in Microsoft Intune. Optional. Can be `null`.                                                                                                                                           |
| `publisher`               | string                                                               | No       | The name of the application's publisher. Required when creating or editing an application. It is matched against your existing publishers ignoring case, and a new publisher is created if none matches. Can be `null`.       |
| `developer`               | string                                                               | No       | The application's developer. Optional. Can be `null`.                                                                                                                                                                         |
| `owner`                   | string                                                               | No       | The application's owner. Optional. Can be `null`.                                                                                                                                                                             |
| `updateId`                | string (uuid)                                                        | No       | The ID of the version (update) to complete, as returned by the draft endpoint. Required.                                                                                                                                      |
| `productId`               | string (uuid)                                                        | No       | The application's ID, as returned by the draft endpoint. Required when adding a new version or editing an application.                                                                                                        |
| `msiProductCode`          | string (uuid)                                                        | No       | The MSI product code (a GUID) of the application's installer. When set, the application is treated as an MSI installer; when `null`, it is treated as an EXE installer. Can be `null`.                                        |
| `detectionRules`          | [`DetectionRulesDto`](applications.md#detectionrulesdto)             | No       | Custom rules that detect whether the application is installed. When `null`, detection is based on `msiProductCode`, `arpDisplayNameMatch` and `arpVersionMatch`. Can be `null`.                                               |
| `customRequirements`      | [`CustomRequirementsDto`](applications.md#customrequirementsdto)     | No       | Custom requirement rules a device must meet before the application installs. When `null`, requirements are based on `requirementArchitecture` only. Can be `null`.                                                            |
| `revisionId`              | integer (int32)                                                      | No       | The revision ID returned by the draft endpoint.                                                                                                                                                                               |
| `iconUrl`                 | string                                                               | No       | The key of an uploaded icon file to use as the application's icon. Optional. Can be `null`.                                                                                                                                   |
| `folderPath`              | string                                                               | No       | The local folder that contains the application's files. Optional and informational only: the file paths in `files` and `primaryInstallerFile` are relative to this folder. Can be `null`.                                     |
| `primaryInstallerFile`    | string                                                               | No       | The path of the main installer file, relative to the application folder. Backslashes are converted to forward slashes, and the path is matched against the `fileName` values in `files`, ignoring case. Can be `null`.        |
| `cmdArguments`            | string                                                               | No       | The command-line arguments used to install the application silently. For an MSI installer, these are used as the MSI command line. Can be `null`.                                                                             |
| `files`                   | array of [`ApplicationFileDto`](applications.md#applicationfiledto)  | No       | Every file in the application version, including the main installer. When editing, this list replaces the existing files, so send the complete list. Requests that include restricted file names are rejected. Can be `null`. |
| `silentUninstallArg`      | string                                                               | No       | The command-line arguments used to uninstall the application silently. Optional. Can be `null`.                                                                                                                               |

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

Retrieves detailed information about an application in the public Patch My PC catalog, including the variants you can deploy for the requested operating system. Each variant has a `catalogEntryId` that identifies your selection when you create a deployment. `connectionId` is required and identifies the Intune connection that scopes the lookup. `osType` is optional and defaults to `Windows`; `MacOS` requires your account to be entitled to macOS applications, otherwise the application is reported as not found.

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

Searches the public Patch My PC catalog. Results describe the architecture, language, installer type and install context options for the requested operating system; not every combination can be deployed, so use the application details to see the exact variants. Any feed types in the request body are ignored and replaced with `PMPC`. `connectionId` is required and identifies the Intune connection that scopes the search.

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

| Name                      | Type                                                                          | Required | Description                                                                                                                                                                                                                                                                                                                    |
| ------------------------- | ----------------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `vendorIds`               | array of string (uuid)                                                        | No       | Return only applications from these publishers, identified by vendor ID. Can be `null`.                                                                                                                                                                                                                                        |
| `languages`               | array of string                                                               | No       | Return only applications in these languages, for example `en-US`. Can be `null`.                                                                                                                                                                                                                                               |
| `architectures`           | array of [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | Return only applications for these processor architectures. Can be `null`.                                                                                                                                                                                                                                                     |
| `osType`                  | [`OSType`](applications.md#ostype)                                            | No       | The operating system to search: `Windows` or `MacOS`. Defaults to `Windows`. macOS results from the Patch My PC catalog are returned only when your account has the macOS Applications feature; otherwise the search returns no results. Searches of your custom applications are not affected by this feature. Can be `null`. |
| `feedTypes`               | array of [`CatalogFeedType`](applications.md#catalogfeedtype)                 | No       | The catalog feeds to search. Each search endpoint sets this from its route, so any value you send is ignored: `/apps/search` and `/apps/custom/search` search your custom applications, and `/apps/public/search` searches the Patch My PC catalog. Can be `null`.                                                             |
| `connectionId`            | string (uuid)                                                                 | No       | The ID of the Intune connection that scopes the search. Required when searching the Patch My PC catalog; not needed when searching your custom applications. Can be `null`.                                                                                                                                                    |
| `lastModifiedFromUtc`     | string (date-time)                                                            | No       | The start of the last-modified date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                 |
| `lastModifiedToUtc`       | string (date-time)                                                            | No       | The end of the last-modified date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                   |
| `lastUpdatedFromUtc`      | string (date-time)                                                            | No       | The start of the last-updated date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                  |
| `lastUpdatedToUtc`        | string (date-time)                                                            | No       | The end of the last-updated date range to filter on, in UTC. Can be `null`.                                                                                                                                                                                                                                                    |
| `displayNameSearchString` | string                                                                        | No       | Text to search for in application display names. Can be `null`.                                                                                                                                                                                                                                                                |
| `skip`                    | integer (int32)                                                               | No       | Number of matching products to skip before returning the page.                                                                                                                                                                                                                                                                 |
| `limit`                   | integer (int32)                                                               | No       | Maximum number of matching products to return. Defaults to 50.                                                                                                                                                                                                                                                                 |
| `sortField`               | string                                                                        | No       | The application property to sort matching results by, such as `DisplayName`. Defaults to `DisplayName`. Can be `null`.                                                                                                                                                                                                         |
| `ascending`               | boolean                                                                       | No       | Whether to sort results in ascending order. Defaults to `true`.                                                                                                                                                                                                                                                                |
| `includeIconData`         | boolean                                                                       | No       | Whether to include each application's icon image in `iconBase64` and `iconContentType`. Defaults to `false`. Including icons makes the search slower.                                                                                                                                                                          |

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

Creates a new Intune deployment. Both custom and public applications require CatalogEntryId from details, identifying an entry for the route's product, connection and operating system. Public applications require an explicit variant selection. The broker resolves current deployment metadata without historical fallback or version pinning.

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

| Name                  | Type                                                                                              | Required | Description                                                                                                                                                                                                                                     |
| --------------------- | ------------------------------------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `connectionId`        | string (uuid)                                                                                     | No       | ID of the Intune connection (tenant) to create the deployment under. Required.                                                                                                                                                                  |
| `osType`              | [`OSType`](applications.md#ostype)                                                                | No       | Operating system the deployment targets, for example `Windows` or `MacOS`.                                                                                                                                                                      |
| `catalogEntryId`      | string (uuid)                                                                                     | Yes      | Selects the exact catalog entry to deploy, for a custom or public application. Required. Use the entry ID from the application's details for this operating system. It identifies a recipe, not a pinned version or revision.                   |
| `assignments`         | array of [`CreateDeploymentAssignmentRequest`](applications.md#createdeploymentassignmentrequest) | No       | Assignments for the deployment: who it targets and with what intent. At least one assignment is required. Can be `null`.                                                                                                                        |
| `categoryIds`         | array of string                                                                                   | No       | IDs of the Intune categories to assign to the deployment. Omit, or send an empty list, to assign no categories. Can be `null`.                                                                                                                  |
| `espProfileIds`       | array of string                                                                                   | No       | IDs of the Intune Enrollment Status Page (ESP) profiles to assign to the deployment. Omit, or send an empty list, to assign none. There is no endpoint to list ESP profiles, so get the profile ID from the Intune admin center. Can be `null`. |
| `parentDeploymentIds` | array of string                                                                                   | No       | IDs of existing deployments this deployment depends on. Those deployments must finish installing first. Omit, or send an empty list, for no dependencies. Use the dependency candidates endpoint to find eligible deployments. Can be `null`.   |
| `configuration`       | [`DeploymentConfigurationRequest`](applications.md#deploymentconfigurationrequest)                | No       | Optional deployment configuration: conflicting-process behavior, return codes, requirements, install parameters, app information overrides and behavior settings. Omit it to create the deployment with default settings. Can be `null`.        |

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
  "catalogEntryId": "{catalogEntryId}",
  "assignments": [
    {
      "groupId": "{groupId}",
      "intent": "Required",
      "targetType": "Group"
    }
  ],
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

| Name                  | Type                                                                                              | Required | Description                                                                                                                                                                                                                                                                                      |
| --------------------- | ------------------------------------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `connectionId`        | string (uuid)                                                                                     | No       | ID of the Intune connection (tenant) the deployment belongs to. Required.                                                                                                                                                                                                                        |
| `name`                | string                                                                                            | No       | New display name for the deployment. Must not match the name of another deployment in the connection for the same installer type; a duplicate name returns a 400 response. Omit it to keep the current name. Can be `null`.                                                                      |
| `assignments`         | array of [`CreateDeploymentAssignmentRequest`](applications.md#createdeploymentassignmentrequest) | No       | Complete set of assignments for the deployment, replacing all existing assignments. Omit it to keep the current assignments. An empty list is rejected, because a deployment needs at least one assignment. Can be `null`.                                                                       |
| `configuration`       | [`DeploymentConfigurationRequest`](applications.md#deploymentconfigurationrequest)                | No       | Configuration changes to apply: conflicting-process behavior, return codes, requirements, install parameters, app information overrides and behavior settings. Omit it, or omit any field inside it, to keep the current value. Can be `null`.                                                   |
| `categoryIds`         | array of string                                                                                   | No       | Complete set of Intune category IDs, replacing all existing categories. Omit it to keep the current categories, or send an empty list to remove them all. Can be `null`.                                                                                                                         |
| `espProfileIds`       | array of string                                                                                   | No       | Complete set of Enrollment Status Page (ESP) profile IDs, replacing all existing ESP profiles. Omit it to keep the current ESP profiles, or send an empty list to remove them all. There is no endpoint to list ESP profiles, so get the profile ID from the Intune admin center. Can be `null`. |
| `parentDeploymentIds` | array of string                                                                                   | No       | Complete set of IDs of the deployments this deployment depends on, replacing all existing dependencies. Omit it to keep the current dependencies, or send an empty list to remove them all. Use the dependency candidates endpoint to find eligible deployments. Can be `null`.                  |

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
  "assignments": [
    {
      "groupId": "{groupId}",
      "intent": "Required",
      "targetType": "Group"
    }
  ],
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

| Name           | Type          | Required | Description                                                               |
| -------------- | ------------- | -------- | ------------------------------------------------------------------------- |
| `connectionId` | string (uuid) | No       | ID of the Intune connection (tenant) the deployment belongs to. Required. |
| `pause`        | boolean       | No       | `true` to pause the deployment's scheduled sync, or `false` to resume it. |

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

| Name                      | Type                                                                                                 | Required | Description                                                                                                                                                                                    |
| ------------------------- | ---------------------------------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `connectionId`            | string (uuid)                                                                                        | No       | ID of the Intune connection (tenant) the template belongs to. Required.                                                                                                                        |
| `templateName`            | string                                                                                               | No       | Name of the template. Required. Can be `null`.                                                                                                                                                 |
| `osType`                  | [`OSType`](applications.md#ostype)                                                                   | No       | Operating system the template applies to, for example `Windows` or `MacOS`.                                                                                                                    |
| `isDefault`               | boolean                                                                                              | No       | Whether this template becomes the connection's default template. A connection has exactly one default, so setting this to `true` removes the default status from the current default template. |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                                     | No       | Whether the application's own built-in updater is enabled, disabled, or not available.                                                                                                         |
| `allowAvailableUninstall` | boolean                                                                                              | No       | Whether end users can uninstall the application themselves from the Company Portal.                                                                                                            |
| `removeDesktopShortcuts`  | boolean                                                                                              | No       | Whether desktop shortcuts created by the installer are removed after installation.                                                                                                             |
| `appVersionsRetention`    | integer (int32)                                                                                      | No       | Number of previous application versions to keep in Intune. `0` means previous versions are not kept.                                                                                           |
| `customVendor`            | string                                                                                               | No       | Publisher name shown in the Company Portal instead of the catalog value. Can be `null`.                                                                                                        |
| `customDeveloper`         | string                                                                                               | No       | Developer name shown in the Company Portal instead of the catalog value. Can be `null`.                                                                                                        |
| `customOwner`             | string                                                                                               | No       | Owner shown in the Company Portal for deployments created from this template. Can be `null`.                                                                                                   |
| `customNotes`             | string                                                                                               | No       | Free-text notes shown in the Company Portal for deployments created from this template. Can be `null`.                                                                                         |
| `copyForwardAssignments`  | boolean                                                                                              | No       | Whether a deployment created from this template inherits the template's assignments.                                                                                                           |
| `categoryIds`             | array of string                                                                                      | No       | IDs of the Intune categories to apply to deployments created from this template. Omit, or send an empty list, for no categories. Can be `null`.                                                |
| `espProfileIds`           | array of string                                                                                      | No       | IDs of the Enrollment Status Page (ESP) profiles to apply to deployments created from this template. Omit, or send an empty list, for none. Can be `null`.                                     |
| `roleScopeTagIds`         | array of string                                                                                      | No       | IDs of the Intune role scope tags to apply to deployments created from this template. Omit, or send an empty list, for none. Can be `null`.                                                    |
| `customRequirements`      | [`EditDeploymentCustomRequirementsRequest`](applications.md#editdeploymentcustomrequirementsrequest) | No       | Custom requirement rules to apply to deployments created from this template. Omit for no custom requirements. Can be `null`.                                                                   |

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

| Name                      | Type                                                                                                 | Required | Description                                                                                                                                                                                    |
| ------------------------- | ---------------------------------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `connectionId`            | string (uuid)                                                                                        | No       | ID of the Intune connection (tenant) the template belongs to. Required.                                                                                                                        |
| `templateName`            | string                                                                                               | No       | Name of the template. Required. Can be `null`.                                                                                                                                                 |
| `osType`                  | [`OSType`](applications.md#ostype)                                                                   | No       | Operating system the template applies to, for example `Windows` or `MacOS`.                                                                                                                    |
| `isDefault`               | boolean                                                                                              | No       | Whether this template becomes the connection's default template. A connection has exactly one default, so setting this to `true` removes the default status from the current default template. |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                                     | No       | Whether the application's own built-in updater is enabled, disabled, or not available.                                                                                                         |
| `allowAvailableUninstall` | boolean                                                                                              | No       | Whether end users can uninstall the application themselves from the Company Portal.                                                                                                            |
| `removeDesktopShortcuts`  | boolean                                                                                              | No       | Whether desktop shortcuts created by the installer are removed after installation.                                                                                                             |
| `appVersionsRetention`    | integer (int32)                                                                                      | No       | Number of previous application versions to keep in Intune. `0` means previous versions are not kept.                                                                                           |
| `customVendor`            | string                                                                                               | No       | Publisher name shown in the Company Portal instead of the catalog value. Can be `null`.                                                                                                        |
| `customDeveloper`         | string                                                                                               | No       | Developer name shown in the Company Portal instead of the catalog value. Can be `null`.                                                                                                        |
| `customOwner`             | string                                                                                               | No       | Owner shown in the Company Portal for deployments created from this template. Can be `null`.                                                                                                   |
| `customNotes`             | string                                                                                               | No       | Free-text notes shown in the Company Portal for deployments created from this template. Can be `null`.                                                                                         |
| `copyForwardAssignments`  | boolean                                                                                              | No       | Whether a deployment created from this template inherits the template's assignments.                                                                                                           |
| `categoryIds`             | array of string                                                                                      | No       | IDs of the Intune categories to apply to deployments created from this template. Omit, or send an empty list, for no categories. Can be `null`.                                                |
| `espProfileIds`           | array of string                                                                                      | No       | IDs of the Enrollment Status Page (ESP) profiles to apply to deployments created from this template. Omit, or send an empty list, for none. Can be `null`.                                     |
| `roleScopeTagIds`         | array of string                                                                                      | No       | IDs of the Intune role scope tags to apply to deployments created from this template. Omit, or send an empty list, for none. Can be `null`.                                                    |
| `customRequirements`      | [`EditDeploymentCustomRequirementsRequest`](applications.md#editdeploymentcustomrequirementsrequest) | No       | Custom requirement rules to apply to deployments created from this template. Omit for no custom requirements. Can be `null`.                                                                   |

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

| Name                     | Type            | Required | Description                                                                                                                                |
| ------------------------ | --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `updateId`               | string (uuid)   | No       | The ID of the application version (update) the draft or operation applies to. Pass it to the completion endpoint as `updateId`.            |
| `revisionId`             | integer (int32) | No       | The revision ID of the draft. Pass it to the completion endpoint as `revisionId`.                                                          |
| `productId`              | string (uuid)   | No       | The application's ID.                                                                                                                      |
| `displayName`            | string          | No       | The application's display name. Empty in draft responses. Can be `null`.                                                                   |
| `customerId`             | string (uuid)   | No       | The ID of the customer account that owns the application. Set when an operation completes; draft responses return an empty GUID.           |
| `fileUploadPath`         | string          | No       | The relative API path for uploading a small file in a single multipart/form-data request. Returned only in draft responses. Can be `null`. |
| `chunkedFileUploadPath`  | string          | No       | The relative API path for uploading a large file in chunks. Returned only in draft responses. Can be `null`.                               |
| `fileCompleteUploadPath` | string          | No       | The relative API path for completing a chunked file upload. Returned only in draft responses. Can be `null`.                               |

### ApplicationFileDto

| Name         | Type                                               | Required | Description                                                                                                                                                                                              |
| ------------ | -------------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `productId`  | string (uuid)                                      | No       | The ID of the application the file belongs to. Ignored when you send the file in a completion request.                                                                                                   |
| `fileName`   | string                                             | No       | The file's path relative to the application folder, using forward slashes (`/`). Can be `null`.                                                                                                          |
| `fileSize`   | integer (int64)                                    | No       | The file size, in bytes.                                                                                                                                                                                 |
| `fileType`   | [`UpdateFileType`](applications.md#updatefiletype) | No       | The file's role in the application, for example `Installation` for the main installer or `Extra` for a supporting file.                                                                                  |
| `sha1Hash`   | string                                             | No       | The SHA-1 hash of the file contents, as a hexadecimal string. Can be `null`.                                                                                                                             |
| `sha256Hash` | string                                             | No       | The SHA-256 hash of the file contents, as a hexadecimal string. Only the main installer file (`Installation`) uses it; for other files it is `null` in responses and ignored in requests. Can be `null`. |

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

| Name           | Type                                                       | Required | Description                                                                                       |
| -------------- | ---------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------- |
| `connectionId` | string (uuid)                                              | No       | Unique ID of the connection. Pass it as the connection for deployment operations.                 |
| `displayName`  | string                                                     | No       | Display name of the connection, or `null` if none is set. Can be `null`.                          |
| `type`         | [`ConnectionType`](applications.md#connectiontype)         | No       | The connection type. Only Intune connections are returned.                                        |
| `adminConsent` | [`AdminConsentStatus`](applications.md#adminconsentstatus) | No       | The admin consent status of the connection, such as `Granted`, `Pending` or `MissingPermissions`. |

### ConnectionType

Type: string. One of the following values:

* `Unknown`
* `ConfigMgr`
* `Intune`
* `Publisher`

### CreateDeploymentAssignmentRequest

| Name         | Type                                                           | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------ | -------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `groupId`    | string                                                         | No       | Microsoft Entra ID group ID, from your own tenant, to assign the deployment to. Required when `targetType` is `Group` (or omitted) and `intent` is `Required`, `Available`, `Uninstall` or `UpdateOnly`. Optional for `AvailableWithoutEnrollment`. Must be omitted for every other target type and for the no-assignment intents. To target all users or all devices, set `targetType` instead of passing a group ID. Can be `null`. |
| `intent`     | [`InstallationIntent`](applications.md#installationintent)     | No       | What Intune does with the app for this assignment, for example `Required`, `Available`, `Uninstall` or `UpdateOnly`. `Unknown` is not accepted. The no-assignment intents, `NoAssignmentsInstall` and `NoAssignmentsUpdate`, create a deployment that is assigned to nobody. For those, omit `targetType` (or set it to `NotSet`) and `groupId`; any other value is rejected with a 400 response.                                     |
| `targetType` | [`AssignmentTargetType`](applications.md#assignmenttargettype) | No       | Who the assignment targets. `Group` targets the group in `groupId`. `AllUsers` and `AllDevices` target the whole tenant and must not include a `groupId`. `NotSet` is valid only with the no-assignment intents. When omitted, the assignment targets a group, except with the no-assignment intents, where it targets nobody. Can be `null`.                                                                                         |

### CustomApplicationDetailsDto

| Name             | Type          | Required | Description                                                                                                                                                                                                                                    |
| ---------------- | ------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `productId`      | string (uuid) | No       | The ID of the application this entry belongs to. Included in application details; omitted from search results. Read-only. Can be `null`.                                                                                                       |
| `catalogEntryId` | string (uuid) | No       | The ID of the catalog entry for this custom application. Pass it as `catalogEntryId` when you create a deployment. Omitted from search results and when the entry ID is not available. Read-only. Can be `null`.                               |
| `updateId`       | string (uuid) | No       | The ID of the update associated with this custom application. Included in search and detail responses when available. It is not necessarily the update for the version shown in the result.                                                    |
| `isMigrationApp` | boolean       | No       | Whether the application was migrated from another source rather than created directly as a custom application. `null` when the value is not available, for example in search results; do not read `null` as `false`. Read-only. Can be `null`. |

### CustomApplicationDto

| Name                       | Type                                                                         | Required | Description                                                                                                                                                                                                                         |
| -------------------------- | ---------------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `productId`                | string (uuid)                                                                | No       | The application's ID. Read-only.                                                                                                                                                                                                    |
| `type`                     | string                                                                       | No       | The application type: `pmpc` for a Patch My PC catalog application, or `custom` for one of your custom applications. Read-only. Can be `null`.                                                                                      |
| `displayName`              | string                                                                       | No       | The application's display name. Read-only. Can be `null`.                                                                                                                                                                           |
| `description`              | string                                                                       | No       | A description of the application. Read-only. Can be `null`.                                                                                                                                                                         |
| `language`                 | string                                                                       | No       | The application's language code, for example `en-US`. Read-only. Can be `null`.                                                                                                                                                     |
| `vendorName`               | string                                                                       | No       | The name of the application's publisher (vendor). Read-only. Can be `null`.                                                                                                                                                         |
| `updateVersion`            | string                                                                       | No       | The version number of the application's latest version. Read-only. Can be `null`.                                                                                                                                                   |
| `iconURL`                  | string                                                                       | No       | A reference to the application's icon file. This is a key, not a download link; the icon image itself is returned in `iconBase64`. Read-only. Can be `null`.                                                                        |
| `iconBase64`               | string                                                                       | No       | The application's icon image, Base64-encoded. `null` when the application has no icon or the icon could not be retrieved. Read-only. Can be `null`.                                                                                 |
| `iconContentType`          | string                                                                       | No       | The MIME type of the icon in `iconBase64`, for example `image/png`. Set only when `iconBase64` is set. Read-only. Can be `null`.                                                                                                    |
| `privacyUrl`               | string                                                                       | No       | The URL of the application's privacy policy. Read-only. Can be `null`.                                                                                                                                                              |
| `informationUrl`           | string                                                                       | No       | The URL of a web page with more information about the application. Read-only. Can be `null`.                                                                                                                                        |
| `developer`                | string                                                                       | No       | The application's developer. Read-only. Can be `null`.                                                                                                                                                                              |
| `intuneNotes`              | string                                                                       | No       | Notes to include with the application in Microsoft Intune. Read-only. Can be `null`.                                                                                                                                                |
| `installerType`            | [`InstallerType`](applications.md#installertype)                             | No       | The type of installer the application uses, for example `MSI` or `EXE`. Read-only.                                                                                                                                                  |
| `architecture`             | [`RequirementArchitecture`](applications.md#requirementarchitecture)         | No       | The processor architecture a device must have to install the application. Read-only.                                                                                                                                                |
| `installContext`           | [`InstallationBehavior`](applications.md#installationbehavior)               | No       | The context the application installs in, for example `System` or `User`. Read-only. Can be `null`.                                                                                                                                  |
| `actions`                  | array of string                                                              | No       | The actions you can currently perform on this application. A custom application allows `deploy`, `update`, `edit`, `delete` and `download-files`; a Patch My PC catalog application allows `deploy` only. Read-only. Can be `null`. |
| `custom`                   | [`CustomApplicationDetailsDto`](applications.md#customapplicationdetailsdto) | No       | Identity details of this custom application, including the catalog entry ID needed to create a deployment. Omitted when not available. Read-only. Can be `null`.                                                                    |
| `silentInstallArguments`   | string                                                                       | No       | The command-line arguments used to install the application silently. For an MSI installer, this is the MSI command line. Read-only. Can be `null`.                                                                                  |
| `silentUninstallArguments` | string                                                                       | No       | The command-line arguments used to uninstall the application silently. Read-only. Can be `null`.                                                                                                                                    |
| `mainFile`                 | string                                                                       | No       | The file name of the application's main installer file. Read-only. Can be `null`.                                                                                                                                                   |
| `conflictingProcessList`   | array of string                                                              | No       | The names of processes that conflict with installing the application. Read-only. Can be `null`.                                                                                                                                     |
| `detectionRules`           | [`DetectionRulesDto`](applications.md#detectionrulesdto)                     | No       | Custom rules that detect whether the application is installed. `null` when none are set, in which case detection is based on `msiProductCode` or `arpDisplayNameMatch`. Read-only. Can be `null`.                                   |
| `customRequirements`       | [`CustomRequirementsDto`](applications.md#customrequirementsdto)             | No       | Custom requirement rules a device must meet before the application installs. Read-only. Can be `null`.                                                                                                                              |
| `arpDisplayNameMatch`      | string                                                                       | No       | A pattern that matches the application's display name in Add/Remove Programs (ARP), used to detect whether the application is installed. Read-only. Can be `null`.                                                                  |
| `notes`                    | string                                                                       | No       | Notes about the application. Read-only. Can be `null`.                                                                                                                                                                              |
| `owner`                    | string                                                                       | No       | The application's owner. Read-only. Can be `null`.                                                                                                                                                                                  |
| `msiProductCode`           | string (uuid)                                                                | No       | The MSI product code (a GUID) of the application's installer. `null` when the installer is not an MSI. Read-only. Can be `null`.                                                                                                    |
| `isMigrationApp`           | boolean                                                                      | No       | Whether the application was migrated from another source rather than created directly as a custom application. `null` when the value is not available. Read-only. Can be `null`.                                                    |

### CustomRequirementsDto

| Name                        | Type                                                                        | Required | Description                                                                                                                                    |
| --------------------------- | --------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `applicableArchitectures`   | array of [`ApplicableArchitecture`](applications.md#applicablearchitecture) | No       | Windows architectures the application can install on. When empty, the single architecture in `requirementArchitecture` applies. Can be `null`. |
| `minimumWindowsOSVersion`   | [`WindowsOSVersion`](applications.md#windowsosversion)                      | No       | Minimum Windows version the device must run. `null` when no minimum is set. Can be `null`.                                                     |
| `minimumNumberOfProcessors` | integer (int32)                                                             | No       | Minimum number of logical processors the device must have. Can be `null`.                                                                      |
| `minimumMemoryInMB`         | integer (int32)                                                             | No       | Minimum amount of physical memory the device must have, in MB. Can be `null`.                                                                  |
| `minimumCpuSpeedInMHz`      | integer (int32)                                                             | No       | Minimum processor speed the device must have, in MHz. Can be `null`.                                                                           |
| `requirementFileRules`      | array of [`FileRuleDto`](applications.md#fileruledto)                       | No       | File and folder requirement rules. Every rule must pass before the application installs. Can be `null`.                                        |
| `requirementRegistryRules`  | array of [`RegistryRuleDto`](applications.md#registryruledto)               | No       | Registry requirement rules. Every rule must pass before the application installs. Can be `null`.                                               |
| `requirementsScriptRules`   | array of [`ScriptRuleDto`](applications.md#scriptruledto)                   | No       | Script requirement rules. Every rule must pass before the application installs. Can be `null`.                                                 |

### CustomerInfoDto

| Name                       | Type                                                     | Required | Description                                                                                                                                                                                                  |
| -------------------------- | -------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `limits`                   | [`LimitDTO`](applications.md#limitdto)                   | No       | The limits that apply to the customer's account, such as the maximum number of custom applications, the maximum size of a single custom application and the total storage allowed. Read-only. Can be `null`. |
| `customerId`               | string (uuid)                                            | No       | Unique ID of the customer. Read-only.                                                                                                                                                                        |
| `customerName`             | string                                                   | No       | Name of the customer. Read-only. Can be `null`.                                                                                                                                                              |
| `license`                  | [`GetLicenseDto`](applications.md#getlicensedto)         | No       | Details of the customer's Patch My PC license. Read-only. Can be `null`.                                                                                                                                     |
| `limitsProgress`           | [`CustomerLimitsDto`](applications.md#customerlimitsdto) | No       | The customer's current usage of their custom applications, such as the number of custom applications and the storage they use. Compare these values with `limits`. Read-only. Can be `null`.                 |
| `macOSApplicationsEnabled` | boolean                                                  | No       | Whether the customer has access to macOS applications. When `false`, macOS applications are not returned, so an empty macOS result does not mean that no applications matched. Read-only.                    |

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

| Name                   | Type    | Required | Description                                                                                                                                       |
| ---------------------- | ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `customVendor`         | string  | No       | Publisher name shown in the Company Portal. Can be `null`.                                                                                        |
| `customDeveloper`      | string  | No       | Developer name shown in the Company Portal. Can be `null`.                                                                                        |
| `customOwner`          | string  | No       | Owner shown in the Company Portal. Can be `null`.                                                                                                 |
| `customDescription`    | string  | No       | Description shown in the Company Portal. Can be `null`.                                                                                           |
| `customNotes`          | string  | No       | Free-text notes shown in the Company Portal. Can be `null`.                                                                                       |
| `customInformationUrl` | string  | No       | Information URL shown in the Company Portal. Can be `null`.                                                                                       |
| `customPrivacyUrl`     | string  | No       | Privacy statement URL shown in the Company Portal. Can be `null`.                                                                                 |
| `isFeatured`           | boolean | No       | Whether the application is shown as a featured app in the Company Portal. When omitted on create, the application is not featured. Can be `null`. |

### DeploymentAssignmentDto

| Name         | Type                                                           | Required | Description                                                                                                                                                                                                                                                              |
| ------------ | -------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `groupId`    | string                                                         | No       | Microsoft Entra ID group ID the deployment is assigned to. `null` when the assignment does not target a specific group, for example when `targetType` is `AllUsers`, `AllDevices` or `NotSet`. Can be `null`.                                                            |
| `groupName`  | string                                                         | No       | Display name of the assigned group. May be `null`, for example when the assignment does not target a group or the name could not be resolved. Can be `null`.                                                                                                             |
| `targetType` | [`AssignmentTargetType`](applications.md#assignmenttargettype) | No       | Who the assignment targets. `Group` targets the group in `groupId`. `AllUsers` and `AllDevices` target the whole tenant. `NotSet` means the deployment is assigned to nobody, which is always the case for the `NoAssignmentsInstall` and `NoAssignmentsUpdate` intents. |
| `intent`     | [`InstallationIntent`](applications.md#installationintent)     | No       | What Intune does with the app for this assignment, for example `Required`, `Available`, `Uninstall` or `UpdateOnly`.                                                                                                                                                     |

### DeploymentCategoryDto

| Name          | Type   | Required | Description                                         |
| ------------- | ------ | -------- | --------------------------------------------------- |
| `id`          | string | No       | ID of the Intune category. Can be `null`.           |
| `displayName` | string | No       | Display name of the Intune category. Can be `null`. |

### DeploymentConfigurationDto

| Name                      | Type                                                                                 | Required | Description                                                                                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------ | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `additionalArgument`      | string                                                                               | No       | Additional command-line arguments passed to the installer, if any. Can be `null`.                                                                        |
| `installLoggingPath`      | string                                                                               | No       | Folder path the installation log is written to, if set. Can be `null`.                                                                                   |
| `customRequirements`      | [`DeploymentCustomRequirementsDto`](applications.md#deploymentcustomrequirementsdto) | No       | Custom requirement rules currently set on the deployment, such as minimum operating system, hardware, and file, registry or script rules. Can be `null`. |
| `appInfo`                 | [`DeploymentAppInfoDto`](applications.md#deploymentappinfodto)                       | No       | Overrides for the application information shown in the Company Portal. Can be `null`.                                                                    |
| `conflictingProcess`      | [`DeploymentConflictingProcessDto`](applications.md#deploymentconflictingprocessdto) | No       | How the deployment behaves when a conflicting process is running, and which processes count as conflicting. Can be `null`.                               |
| `returnCodes`             | array of [`DeploymentReturnCodeDto`](applications.md#deploymentreturncodedto)        | No       | Installer exit codes and how the deployment interprets each one. Can be `null`.                                                                          |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                     | No       | Whether the application's own built-in updater is enabled, disabled, or not available.                                                                   |
| `allowAvailableUninstall` | boolean                                                                              | No       | Whether end users can uninstall the application themselves from the Company Portal.                                                                      |
| `removeDesktopShortcuts`  | boolean                                                                              | No       | Whether desktop shortcuts created by the installer are removed after installation.                                                                       |
| `appVersionsRetention`    | integer (int32)                                                                      | No       | Number of previous application versions kept in Intune. `0` means previous versions are not kept.                                                        |
| `roleScopeTags`           | array of [`DeploymentRoleScopeTagDto`](applications.md#deploymentrolescopetagdto)    | No       | Intune role scope tags applied to the deployment. Can be `null`.                                                                                         |

### DeploymentConfigurationRequest

| Name                      | Type                                                                                                 | Required | Description                                                                                                                                                                                                                                                                        |
| ------------------------- | ---------------------------------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `additionalArgument`      | string                                                                                               | No       | Additional command-line arguments passed to the installer. When omitted on create, no additional arguments are passed. Can be `null`.                                                                                                                                              |
| `installLoggingPath`      | string                                                                                               | No       | Folder path the installation log is written to. When omitted on create, no log path is set. Can be `null`.                                                                                                                                                                         |
| `customRequirements`      | [`EditDeploymentCustomRequirementsRequest`](applications.md#editdeploymentcustomrequirementsrequest) | No       | Custom requirement rules: minimum operating system, memory, CPU speed and logical processors, excluded architectures, and file, registry and script rules. When omitted on create, the deployment has no custom requirements. Can be `null`.                                       |
| `appInfo`                 | [`DeploymentAppInfoDto`](applications.md#deploymentappinfodto)                                       | No       | Overrides for the application information shown in the Company Portal. When omitted on create, nothing is overridden and the catalog values are used. Can be `null`.                                                                                                               |
| `conflictingProcess`      | [`DeploymentConflictingProcessDto`](applications.md#deploymentconflictingprocessdto)                 | No       | How the deployment behaves when a conflicting process is running, and which processes count as conflicting. When omitted on create, the policy is `None`. Can be `null`.                                                                                                           |
| `returnCodes`             | array of [`DeploymentReturnCodeDto`](applications.md#deploymentreturncodedto)                        | No       | Installer exit codes and how the deployment interprets each one. The list replaces any existing return codes, so send the complete set. When omitted on create, the deployment has no custom return codes. Can be `null`.                                                          |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                                     | No       | Whether the application's own built-in updater is enabled, disabled, or not available. When omitted on create, the value is `NotAvailable`. Only meaningful for Patch My PC catalog applications; the Patch My PC portal does not offer it for custom applications. Can be `null`. |
| `allowAvailableUninstall` | boolean                                                                                              | No       | Whether end users can uninstall the application themselves from the Company Portal. When omitted on create, the value is `false`. Can be `null`.                                                                                                                                   |
| `removeDesktopShortcuts`  | boolean                                                                                              | No       | Whether desktop shortcuts created by the installer are removed after installation. When omitted on create, the value is `false`. Can be `null`.                                                                                                                                    |
| `appVersionsRetention`    | integer (int32)                                                                                      | No       | Number of previous application versions to keep in Intune. `0` means previous versions are not kept. When omitted on create, the value is `0`. Can be `null`.                                                                                                                      |
| `roleScopeTagIds`         | array of string                                                                                      | No       | IDs of the Intune role scope tags to apply to the deployment. When omitted on create, no scope tags are applied. There is no endpoint to list scope tags, so get the IDs from the Intune admin center. Can be `null`.                                                              |

### DeploymentConflictingProcessDto

| Name                               | Type                                                                             | Required | Description                                                                                                                                                                                                                                                     |
| ---------------------------------- | -------------------------------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `policy`                           | [`BlockingProcessMgmtPolicy`](applications.md#blockingprocessmgmtpolicy)         | No       | What happens when a conflicting process is running: `None` does nothing, `Kill` closes the process, `Skip` skips the installation, and `Notify` notifies the user. When omitted on create, the policy is `None`. Can be `null`.                                 |
| `userAddedProcesses`               | array of string                                                                  | No       | Process names to treat as conflicting, in addition to the application's default list of conflicting processes. Can be `null`.                                                                                                                                   |
| `userDeletedProcesses`             | array of string                                                                  | No       | Process names to remove from the application's default list of conflicting processes. Can be `null`.                                                                                                                                                            |
| `preventConflictingProcessRestart` | boolean                                                                          | No       | Whether a conflicting process that was closed is prevented from restarting after installation. When `policy` is `Notify` or `Kill` and this is omitted, it defaults to `false`. Can be `null`.                                                                  |
| `postDeploymentNotificationPolicy` | [`PostDeploymentNotification`](applications.md#postdeploymentnotification)       | No       | Whether the end user is shown a notification after the deployment completes. Must be `DoNotShow` when `policy` is `None`, or when `policy` is `Skip` with no `snoozingNotificationDelaySeconds` delay. Other values in those cases are rejected. Can be `null`. |
| `snoozingNotificationDelaySeconds` | integer (int32)                                                                  | No       | How long, in seconds, the installation is retried silently before the user is notified. `0` means the user is not notified. Only used when `policy` is `Skip`. Can be `null`.                                                                                   |
| `notification`                     | [`DeploymentUserNotificationDto`](applications.md#deploymentusernotificationdto) | No       | How the end user is notified and how long they can defer. Only used when `policy` is `Notify`. When `policy` is `Notify` and this is omitted, the Patch My PC portal's default notification settings are used. Can be `null`.                                   |

### DeploymentCustomRequirementsDto

| Name                        | Type                                                                        | Required | Description                                                                                                      |
| --------------------------- | --------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------- |
| `disableArchitectures`      | array of [`ApplicableArchitecture`](applications.md#applicablearchitecture) | No       | Processor architectures the deployment does not apply to. Empty when no architecture is excluded. Can be `null`. |
| `minimumWindowsOSVersion`   | [`WindowsOSVersion`](applications.md#windowsosversion)                      | No       | Minimum Windows version a device must run. `null` when not set. Can be `null`.                                   |
| `minimumNumberOfProcessors` | integer (int32)                                                             | No       | Minimum number of logical processors a device must have. `null` when not set. Can be `null`.                     |
| `minimumMemoryInMB`         | integer (int32)                                                             | No       | Minimum amount of system memory a device must have, in MB. `null` when not set. Can be `null`.                   |
| `minimumCpuSpeedInMHz`      | integer (int32)                                                             | No       | Minimum CPU speed a device must have, in MHz. `null` when not set. Can be `null`.                                |
| `fileRules`                 | array of [`FileRuleDto`](applications.md#fileruledto)                       | No       | File and folder requirement rules. Can be `null`.                                                                |
| `registryRules`             | array of [`RegistryRuleDto`](applications.md#registryruledto)               | No       | Registry requirement rules. Can be `null`.                                                                       |
| `scriptRules`               | array of [`ScriptRuleDto`](applications.md#scriptruledto)                   | No       | Script requirement rules. Can be `null`.                                                                         |

### DeploymentDeferralPolicyDto

| Name            | Type                                                                   | Required | Description                                                                                                           |
| --------------- | ---------------------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------- |
| `policy`        | [`DeferPolicy`](applications.md#deferpolicy)                           | No       | How deferral is limited: unlimited, by a number of deferrals (`Count`), or by a deadline (`Deadline`). Can be `null`. |
| `defaultAction` | [`DeferPolicyDefaultAction`](applications.md#deferpolicydefaultaction) | No       | What happens when the notification times out before the user makes a choice. Can be `null`.                           |
| `deferCount`    | integer (int32)                                                        | No       | Maximum number of times the user can defer. Only used when `policy` is `Count`. Can be `null`.                        |
| `deadline`      | integer (int32)                                                        | No       | Deferral deadline, in days. Only used when `policy` is `Deadline`. Can be `null`.                                     |

### DeploymentDependencyDto

| Name              | Type                                                 | Required | Description                                                                                                                                                |
| ----------------- | ---------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`              | string                                               | No       | ID of the referenced deployment. Same value as `deploymentId`. Can be `null`.                                                                              |
| `deploymentId`    | string                                               | No       | ID of the referenced deployment. Same value as `id`; prefer this field. Can be `null`.                                                                     |
| `name`            | string                                               | No       | Display name of the referenced deployment. Can be `null`.                                                                                                  |
| `iconUrl`         | string                                               | No       | URL of the icon for the referenced deployment's application. Can be `null`.                                                                                |
| `catalogFeedType` | [`CatalogFeedType`](applications.md#catalogfeedtype) | No       | Catalog the referenced deployment's application comes from, for example `PMPC` for the Patch My PC catalog or `CUSTOMER` for your own custom applications. |

### DeploymentDetailDto

| Name                | Type                                                                          | Required | Description                                                                                                                                                                                                                                                                                            |
| ------------------- | ----------------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `deploymentId`      | string                                                                        | No       | ID of the deployment. Can be `null`.                                                                                                                                                                                                                                                                   |
| `productId`         | string (uuid)                                                                 | No       | ID of the application the deployment was created for.                                                                                                                                                                                                                                                  |
| `catalogEntryId`    | string (uuid)                                                                 | No       | The stored AppCat category identifier, available on both list and detail responses. For public applications this identifies the selected variant; for custom applications it identifies the customer-owned catalog entry, not its ProductId. Null when the stored identifier is absent. Can be `null`. |
| `displayName`       | string                                                                        | No       | Display name of the deployment. Can be `null`.                                                                                                                                                                                                                                                         |
| `osType`            | [`OSType`](applications.md#ostype)                                            | No       | Operating system the deployment targets, for example `Windows` or `MacOS`.                                                                                                                                                                                                                             |
| `status`            | [`DeploymentStatusType`](applications.md#deploymentstatustype)                | No       | Current status of the deployment, for example `InProgress`, `Success`, `Failed` or `Retrying`. Create and edit requests return `InProgress` while the change is applied in Intune.                                                                                                                     |
| `warningMessages`   | array of string                                                               | No       | Warnings that did not stop the deployment, for example an ESP profile or role scope tag that could not be applied. Empty when there are no warnings. Can be `null`.                                                                                                                                    |
| `syncOnHold`        | boolean                                                                       | No       | Whether the deployment's scheduled sync is paused. `true` after you pause it, `false` after you resume it. New deployments start with `false`.                                                                                                                                                         |
| `ringsEnabled`      | boolean                                                                       | No       | Whether ring-based (phased) deployment is enabled. Ring-enabled deployments are managed in the Patch My PC portal and cannot be edited through this API.                                                                                                                                               |
| `actions`           | array of string                                                               | No       | Operations you can currently perform on this deployment, based on its state. Possible values are `edit`, `delete`, `redeploy`, `sync`, `pause-sync` and `resume-sync`. This reflects the deployment's state, not your permissions. Can be `null`.                                                      |
| `errorMessages`     | array of string                                                               | No       | Reasons the deployment last failed. Empty when the deployment has not failed. Check this when `status` stays at `Retrying`, to find out why the deployment cannot complete. Can be `null`.                                                                                                             |
| `categories`        | array of [`DeploymentCategoryDto`](applications.md#deploymentcategorydto)     | No       | Intune categories assigned to the deployment. Can be `null`.                                                                                                                                                                                                                                           |
| `espProfiles`       | array of [`DeploymentEspProfileDto`](applications.md#deploymentespprofiledto) | No       | Enrollment Status Page (ESP) profiles assigned to the deployment. Can be `null`.                                                                                                                                                                                                                       |
| `assignments`       | array of [`DeploymentAssignmentDto`](applications.md#deploymentassignmentdto) | No       | Assignments currently on the deployment: who it targets and with what intent. Empty, never `null`, when the deployment has no assignments. Can be `null`.                                                                                                                                              |
| `parentDeployments` | array of [`DeploymentDependencyDto`](applications.md#deploymentdependencydto) | No       | Deployments this deployment depends on. These must finish installing first. Can be `null`.                                                                                                                                                                                                             |
| `childDeployments`  | array of [`DeploymentDependencyDto`](applications.md#deploymentdependencydto) | No       | Deployments that depend on this deployment. Can be `null`.                                                                                                                                                                                                                                             |
| `version`           | string                                                                        | No       | Application version the deployment currently delivers, for example `1.0`. After a sync, this shows the version the deployment moved to. Can be `null`.                                                                                                                                                 |
| `configuration`     | [`DeploymentConfigurationDto`](applications.md#deploymentconfigurationdto)    | No       | The deployment's current configuration: conflicting-process behavior, return codes, requirements, install parameters, app information overrides and behavior settings. Can be `null`.                                                                                                                  |

### DeploymentDto

| Name              | Type                                                           | Required | Description                                                                                                                                                                                                                                                                                            |
| ----------------- | -------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `deploymentId`    | string                                                         | No       | ID of the deployment. Can be `null`.                                                                                                                                                                                                                                                                   |
| `productId`       | string (uuid)                                                  | No       | ID of the application the deployment was created for.                                                                                                                                                                                                                                                  |
| `catalogEntryId`  | string (uuid)                                                  | No       | The stored AppCat category identifier, available on both list and detail responses. For public applications this identifies the selected variant; for custom applications it identifies the customer-owned catalog entry, not its ProductId. Null when the stored identifier is absent. Can be `null`. |
| `displayName`     | string                                                         | No       | Display name of the deployment. Can be `null`.                                                                                                                                                                                                                                                         |
| `osType`          | [`OSType`](applications.md#ostype)                             | No       | Operating system the deployment targets, for example `Windows` or `MacOS`.                                                                                                                                                                                                                             |
| `status`          | [`DeploymentStatusType`](applications.md#deploymentstatustype) | No       | Current status of the deployment, for example `InProgress`, `Success`, `Failed` or `Retrying`. Create and edit requests return `InProgress` while the change is applied in Intune.                                                                                                                     |
| `warningMessages` | array of string                                                | No       | Warnings that did not stop the deployment, for example an ESP profile or role scope tag that could not be applied. Empty when there are no warnings. Can be `null`.                                                                                                                                    |
| `syncOnHold`      | boolean                                                        | No       | Whether the deployment's scheduled sync is paused. `true` after you pause it, `false` after you resume it. New deployments start with `false`.                                                                                                                                                         |
| `ringsEnabled`    | boolean                                                        | No       | Whether ring-based (phased) deployment is enabled. Ring-enabled deployments are managed in the Patch My PC portal and cannot be edited through this API.                                                                                                                                               |
| `actions`         | array of string                                                | No       | Operations you can currently perform on this deployment, based on its state. Possible values are `edit`, `delete`, `redeploy`, `sync`, `pause-sync` and `resume-sync`. This reflects the deployment's state, not your permissions. Can be `null`.                                                      |

### DeploymentEspProfileDto

| Name                | Type            | Required | Description                                                                  |
| ------------------- | --------------- | -------- | ---------------------------------------------------------------------------- |
| `id`                | string          | No       | ID of the ESP profile. Can be `null`.                                        |
| `displayName`       | string          | No       | Display name of the ESP profile. Can be `null`.                              |
| `applicationsCount` | integer (int32) | No       | Number of applications included in the ESP profile, if known. Can be `null`. |

### DeploymentReturnCodeDto

| Name   | Type                                               | Required | Description                                                                                  |
| ------ | -------------------------------------------------- | -------- | -------------------------------------------------------------------------------------------- |
| `code` | integer (int32)                                    | No       | Exit code returned by the installer, for example `3010`.                                     |
| `type` | [`ReturnCodeType`](applications.md#returncodetype) | No       | How the deployment treats `code`, for example as success, failure, retry or reboot required. |

### DeploymentRoleScopeTagDto

| Name          | Type   | Required | Description                                        |
| ------------- | ------ | -------- | -------------------------------------------------- |
| `id`          | string | No       | ID of the role scope tag. Can be `null`.           |
| `displayName` | string | No       | Display name of the role scope tag. Can be `null`. |

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

| Name                      | Type                                                                                 | Required | Description                                                                                                                                                  |
| ------------------------- | ------------------------------------------------------------------------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `deploymentTemplateId`    | string                                                                               | No       | ID of the deployment template. Can be `null`.                                                                                                                |
| `templateName`            | string                                                                               | No       | Name of the template. Can be `null`.                                                                                                                         |
| `isDefault`               | boolean                                                                              | No       | Whether this is the connection's default template. A connection has exactly one default template, and it cannot be deleted.                                  |
| `osType`                  | [`OSType`](applications.md#ostype)                                                   | No       | Operating system the template applies to, for example `Windows` or `MacOS`.                                                                                  |
| `builtInUpdate`           | [`BuiltInUpdate`](applications.md#builtinupdate)                                     | No       | Whether the application's own built-in updater is enabled, disabled, or not available.                                                                       |
| `allowAvailableUninstall` | boolean                                                                              | No       | Whether end users can uninstall the application themselves from the Company Portal.                                                                          |
| `removeDesktopShortcuts`  | boolean                                                                              | No       | Whether desktop shortcuts created by the installer are removed after installation.                                                                           |
| `appVersionsRetention`    | integer (int32)                                                                      | No       | Number of previous application versions kept in Intune. `0` means previous versions are not kept.                                                            |
| `customVendor`            | string                                                                               | No       | Publisher name shown in the Company Portal instead of the catalog value. Can be `null`.                                                                      |
| `customDeveloper`         | string                                                                               | No       | Developer name shown in the Company Portal instead of the catalog value. Can be `null`.                                                                      |
| `customOwner`             | string                                                                               | No       | Owner shown in the Company Portal for deployments created from this template. Can be `null`.                                                                 |
| `customNotes`             | string                                                                               | No       | Free-text notes shown in the Company Portal for deployments created from this template. Can be `null`.                                                       |
| `customRequirements`      | [`DeploymentCustomRequirementsDto`](applications.md#deploymentcustomrequirementsdto) | No       | Custom requirement rules applied to deployments created from this template. A device must meet them before the application installs on it. Can be `null`.    |
| `categories`              | array of [`DeploymentCategoryDto`](applications.md#deploymentcategorydto)            | No       | Intune categories applied to deployments created from this template. Can be `null`.                                                                          |
| `espProfiles`             | array of [`DeploymentEspProfileDto`](applications.md#deploymentespprofiledto)        | No       | Enrollment Status Page (ESP) profiles applied to deployments created from this template. Can be `null`.                                                      |
| `roleScopeTags`           | array of [`DeploymentRoleScopeTagDto`](applications.md#deploymentrolescopetagdto)    | No       | Intune role scope tags applied to deployments created from this template. Can be `null`.                                                                     |
| `copyForwardAssignments`  | boolean                                                                              | No       | Whether a deployment created from this template inherits the template's assignments.                                                                         |
| `actions`                 | array of string                                                                      | No       | Operations you can currently perform on this template: `edit` and `delete`. The default template cannot be deleted, so it only offers `edit`. Can be `null`. |

### DeploymentTemplateSummaryDto

| Name                   | Type                               | Required | Description                                                                                                                                                  |
| ---------------------- | ---------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `deploymentTemplateId` | string                             | No       | ID of the deployment template. Can be `null`.                                                                                                                |
| `templateName`         | string                             | No       | Name of the template. Can be `null`.                                                                                                                         |
| `isDefault`            | boolean                            | No       | Whether this is the connection's default template. A connection has exactly one default template, and it cannot be deleted.                                  |
| `osType`               | [`OSType`](applications.md#ostype) | No       | Operating system the template applies to, for example `Windows` or `MacOS`.                                                                                  |
| `createdAt`            | string (date-time)                 | No       | Date and time the template was created.                                                                                                                      |
| `lastModifiedAt`       | string (date-time)                 | No       | Date and time the template was last modified.                                                                                                                |
| `actions`              | array of string                    | No       | Operations you can currently perform on this template: `edit` and `delete`. The default template cannot be deleted, so it only offers `edit`. Can be `null`. |

### DeploymentUserNotificationDto

| Name                   | Type                                                                         | Required | Description                                                                                                                                                                                                     |
| ---------------------- | ---------------------------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `policy`               | [`NotificationPolicy`](applications.md#notificationpolicy)                   | No       | Whether the user can defer the installation, or the conflicting application is closed automatically. Can be `null`.                                                                                             |
| `timeOutSeconds`       | integer (int32)                                                              | No       | How long, in seconds, the notification is shown before the default action is taken. Must be between `60` (1 minute) and `82800` (23 hours). The Patch My PC portal default is `300` (5 minutes). Can be `null`. |
| `timeOutUseMaxRuntime` | boolean                                                                      | No       | Whether the notification timeout follows the deployment's maximum run time instead of `timeOutSeconds`. Can be `null`.                                                                                          |
| `focusAssistPolicy`    | [`FocusAssistPolicy`](applications.md#focusassistpolicy)                     | No       | What happens to the notification while Windows Focus Assist is suppressing notifications. Can be `null`.                                                                                                        |
| `defer`                | [`DeploymentDeferralPolicyDto`](applications.md#deploymentdeferralpolicydto) | No       | How many times, or for how long, the user can defer. Only used when `policy` allows deferral. Can be `null`.                                                                                                    |

### DetectionRuleType

Type: string. One of the following values:

* `None`
* `PMPC`
* `Script`
* `Manual`

### DetectionRulesDto

| Name              | Type                                                          | Required | Description                                                                                                                                                                                                                                                                    |
| ----------------- | ------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `rulesType`       | [`DetectionRuleType`](applications.md#detectionruletype)      | No       | The detection method the application uses. `PMPC` detects the application by its MSI product code, set in `productCodeRule`. `Manual` uses your own file and registry rules, set in `fileSystemRules` and `registryRules`. `Script` runs the detection script in `scriptRule`. |
| `productCodeRule` | [`MsiDetectionRuleDto`](applications.md#msidetectionruledto)  | No       | MSI product code detection rule. Used when `rulesType` selects MSI product code detection. Can be `null`.                                                                                                                                                                      |
| `fileSystemRules` | array of [`FileRuleDto`](applications.md#fileruledto)         | No       | File and folder detection rules. Can be `null`.                                                                                                                                                                                                                                |
| `registryRules`   | array of [`RegistryRuleDto`](applications.md#registryruledto) | No       | Registry detection rules. Can be `null`.                                                                                                                                                                                                                                       |
| `scriptRule`      | [`ScriptRuleDto`](applications.md#scriptruledto)              | No       | Script detection rule. An application has at most one detection script. Can be `null`.                                                                                                                                                                                         |

### EditDeploymentCustomRequirementsRequest

| Name                        | Type                                                                        | Required | Description                                                                                                                                                                         |
| --------------------------- | --------------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `disableArchitectures`      | array of [`ApplicableArchitecture`](applications.md#applicablearchitecture) | No       | Processor architectures the deployment does not apply to. When editing, omit it to keep the current value. Can be `null`.                                                           |
| `minimumWindowsOSVersion`   | [`WindowsOSVersion`](applications.md#windowsosversion)                      | No       | Minimum Windows version a device must run. When editing, omit it to keep the current value. Can be `null`.                                                                          |
| `minimumNumberOfProcessors` | integer (int32)                                                             | No       | Minimum number of logical processors a device must have. When editing, omit it to keep the current value. Can be `null`.                                                            |
| `minimumMemoryInMB`         | integer (int32)                                                             | No       | Minimum amount of system memory a device must have, in MB. When editing, omit it to keep the current value. Can be `null`.                                                          |
| `minimumCpuSpeedInMHz`      | integer (int32)                                                             | No       | Minimum CPU speed a device must have, in MHz. When editing, omit it to keep the current value. Can be `null`.                                                                       |
| `fileRules`                 | array of [`FileRuleDto`](applications.md#fileruledto)                       | No       | Complete set of file and folder requirement rules. A list you send, even an empty one, replaces the existing rules. When editing, omit it to keep the current rules. Can be `null`. |
| `registryRules`             | array of [`RegistryRuleDto`](applications.md#registryruledto)               | No       | Complete set of registry requirement rules. A list you send, even an empty one, replaces the existing rules. When editing, omit it to keep the current rules. Can be `null`.        |
| `scriptRules`               | array of [`ScriptRuleDto`](applications.md#scriptruledto)                   | No       | Complete set of script requirement rules. A list you send, even an empty one, replaces the existing rules. When editing, omit it to keep the current rules. Can be `null`.          |

### FileRuleDto

| Name                   | Type                                                             | Required | Description                                                                                                                              |
| ---------------------- | ---------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `operator`             | [`RuleOperator`](applications.md#ruleoperator)                   | No       | How the detected value is compared with `comparisonValue`.                                                                               |
| `path`                 | string                                                           | No       | Full path of the folder that contains the file or folder to check, for example `C:\Program Files\Contoso`. Can be `null`.                |
| `fileOrFolderName`     | string                                                           | No       | Name of the file or folder to check within `path`. Can be `null`.                                                                        |
| `check32BitOn64System` | boolean                                                          | No       | When `true`, checks the 32-bit locations on a 64-bit system.                                                                             |
| `operationType`        | [`FileRuleOperationType`](applications.md#fileruleoperationtype) | No       | What to check about the file or folder, such as whether it exists, its version, its size, or its created or modified date.               |
| `comparisonValue`      | string                                                           | No       | The value the detected value is compared with. Required when `operationType` compares a value, such as a version or size. Can be `null`. |

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

| Name             | Type                                           | Required | Description                                                                                                     |
| ---------------- | ---------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------- |
| `operator`       | [`RuleOperator`](applications.md#ruleoperator) | No       | How the installed product version is compared with `productVersion`. Applies only when `productVersion` is set. |
| `productCode`    | string                                         | No       | The MSI product code (a GUID) that identifies the installed application. Can be `null`.                         |
| `productVersion` | string                                         | No       | Optional product version to compare with the installed version, using `operator`. Can be `null`.                |

### NotificationPolicy

Type: string. One of the following values:

* `AllowDefer`
* `AutoClose`

### OSType

Type: string. One of the following values:

* `Windows`
* `MacOS`

### PmpcApplicationDetailsDto

| Name              | Type                                                                          | Required | Description                                                                   |
| ----------------- | ----------------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------- |
| `architectures`   | array of [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | Architectures available for the requested operating system. Can be `null`.    |
| `languages`       | array of string                                                               | No       | Languages available for the requested operating system. Can be `null`.        |
| `installerTypes`  | array of [`InstallerType`](applications.md#installertype)                     | No       | Installer types available for the requested operating system. Can be `null`.  |
| `installContexts` | array of [`InstallationBehavior`](applications.md#installationbehavior)       | No       | Install contexts available for the requested operating system. Can be `null`. |

### PostDeploymentNotification

Type: string. One of the following values:

* `DoNotShow`
* `AlwaysShow`
* `ShowIfProcessClosed`

### ProductDto

| Name                       | Type                                                                         | Required | Description                                                                                                                                                                                                                         |
| -------------------------- | ---------------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `productId`                | string (uuid)                                                                | No       | The application's ID. Read-only.                                                                                                                                                                                                    |
| `type`                     | string                                                                       | No       | The application type: `pmpc` for a Patch My PC catalog application, `custom` for one of your custom applications, or `winget` for a Winget application. Treat any other value as an unknown type. Read-only. Can be `null`.         |
| `pmpc`                     | [`PmpcApplicationDetailsDto`](applications.md#pmpcapplicationdetailsdto)     | No       | Details specific to a Patch My PC catalog application. Present only when `type` is `pmpc`. Read-only. Can be `null`.                                                                                                                |
| `custom`                   | [`CustomApplicationDetailsDto`](applications.md#customapplicationdetailsdto) | No       | Details specific to a custom application. Present only when `type` is `custom`. Read-only. Can be `null`.                                                                                                                           |
| `winget`                   | [`WingetApplicationDetailsDto`](applications.md#wingetapplicationdetailsdto) | No       | Details specific to a Winget application. Present only when `type` is `winget`. Read-only. Can be `null`.                                                                                                                           |
| `actions`                  | array of string                                                              | No       | The actions you can currently perform on this application. A custom application allows `deploy`, `update`, `edit`, `delete` and `download-files`; a Patch My PC catalog application allows `deploy` only. Read-only. Can be `null`. |
| `displayName`              | string                                                                       | No       | The application's display name. Read-only. Can be `null`.                                                                                                                                                                           |
| `description`              | string                                                                       | No       | A description of the application. Read-only. Can be `null`.                                                                                                                                                                         |
| `language`                 | string                                                                       | No       | The application's language code, for example `en-US`. Read-only. Can be `null`.                                                                                                                                                     |
| `vendorName`               | string                                                                       | No       | The name of the application's publisher (vendor). Read-only. Can be `null`.                                                                                                                                                         |
| `silentInstallArguments`   | string                                                                       | No       | The command-line arguments used to install the application silently. For an MSI installer, this is the MSI command line. Read-only. Can be `null`.                                                                                  |
| `mainFile`                 | string                                                                       | No       | The file name of the application's main installer file. Read-only. Can be `null`.                                                                                                                                                   |
| `architecture`             | [`RequirementArchitecture`](applications.md#requirementarchitecture)         | No       | The processor architecture a device must have to install the application. Read-only.                                                                                                                                                |
| `installerType`            | [`InstallerType`](applications.md#installertype)                             | No       | The type of installer the application uses, for example `MSI` or `EXE`. Read-only.                                                                                                                                                  |
| `updateVersion`            | string                                                                       | No       | The version number of the application's latest version. Read-only. Can be `null`.                                                                                                                                                   |
| `installContext`           | [`InstallationBehavior`](applications.md#installationbehavior)               | No       | The context the application installs in, for example `System` or `User`. Read-only. Can be `null`.                                                                                                                                  |
| `conflictingProcessList`   | array of string                                                              | No       | The names of processes that conflict with installing the application. Read-only. Can be `null`.                                                                                                                                     |
| `notes`                    | string                                                                       | No       | Notes about the application. Read-only. Can be `null`.                                                                                                                                                                              |
| `detectionRules`           | [`DetectionRulesDto`](applications.md#detectionrulesdto)                     | No       | Custom rules that detect whether the application is installed. `null` when none are set, and always `null` for a Patch My PC catalog application. Read-only. Can be `null`.                                                         |
| `customRequirements`       | [`CustomRequirementsDto`](applications.md#customrequirementsdto)             | No       | Custom requirement rules a device must meet before the application installs. Read-only. Can be `null`.                                                                                                                              |
| `arpDisplayNameMatch`      | string                                                                       | No       | A pattern that matches the application's display name in Add/Remove Programs (ARP), used to detect whether the application is installed. Read-only. Can be `null`.                                                                  |
| `msiProductCode`           | string (uuid)                                                                | No       | The MSI product code (a GUID) of the application's installer. `null` when the installer is not an MSI, and always `null` for a Patch My PC catalog application. Read-only. Can be `null`.                                           |
| `iconURL`                  | string                                                                       | No       | A reference to the application's icon file. This is a key, not a download link; the icon image itself is returned in `iconBase64`. Read-only. Can be `null`.                                                                        |
| `iconBase64`               | string                                                                       | No       | The application's icon image, Base64-encoded. `null` when the application has no icon or the icon could not be retrieved. Read-only. Can be `null`.                                                                                 |
| `iconContentType`          | string                                                                       | No       | The MIME type of the icon in `iconBase64`, for example `image/png`. Set only when `iconBase64` is set. Read-only. Can be `null`.                                                                                                    |
| `silentUninstallArguments` | string                                                                       | No       | The command-line arguments used to uninstall the application silently. Read-only. Can be `null`.                                                                                                                                    |
| `privacyUrl`               | string                                                                       | No       | The URL of the application's privacy policy. Read-only. Can be `null`.                                                                                                                                                              |
| `informationUrl`           | string                                                                       | No       | The URL of a web page with more information about the application. Read-only. Can be `null`.                                                                                                                                        |
| `intuneNotes`              | string                                                                       | No       | Notes to include with the application in Microsoft Intune. Read-only. Can be `null`.                                                                                                                                                |
| `developer`                | string                                                                       | No       | The application's developer. Read-only. Can be `null`.                                                                                                                                                                              |
| `owner`                    | string                                                                       | No       | The application's owner. Read-only. Can be `null`.                                                                                                                                                                                  |

### ProductFilterResponse

| Name                  | Type                                                              | Required | Description                                                                                                               |
| --------------------- | ----------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------- |
| `totalAmount`         | integer (int64)                                                   | No       | Total number of products matching the filters, before applying `Skip` and `Limit`.                                        |
| `totalVariantsAmount` | integer (int64)                                                   | No       | The total number of matching application variants across all pages, where one application can have more than one variant. |
| `products`            | array of [`ProductSummaryDto`](applications.md#productsummarydto) | No       | The applications on this page of results. Can be `null`.                                                                  |

### ProductSummaryDto

| Name              | Type                                                                         | Required | Description                                                                                                                                                                                                                                                                                                |
| ----------------- | ---------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`              | string (uuid)                                                                | No       | The application's ID. Contains the same value as `productId`; use `productId` in new integrations.                                                                                                                                                                                                         |
| `productId`       | string (uuid)                                                                | No       | The application's ID.                                                                                                                                                                                                                                                                                      |
| `type`            | string                                                                       | No       | The application type: `pmpc` for a Patch My PC catalog application, `custom` for one of your custom applications, or `winget` for a Winget application. Treat any other value as an unknown type. Can be `null`.                                                                                           |
| `pmpc`            | [`PmpcApplicationDetailsDto`](applications.md#pmpcapplicationdetailsdto)     | No       | Details specific to a Patch My PC catalog application. Present only when `type` is `pmpc`. Can be `null`.                                                                                                                                                                                                  |
| `custom`          | [`CustomApplicationDetailsDto`](applications.md#customapplicationdetailsdto) | No       | Details specific to a custom application. Present only when `type` is `custom`. Can be `null`.                                                                                                                                                                                                             |
| `winget`          | [`WingetApplicationDetailsDto`](applications.md#wingetapplicationdetailsdto) | No       | Details specific to a Winget application. Present only when `type` is `winget`. Can be `null`.                                                                                                                                                                                                             |
| `actions`         | array of string                                                              | No       | The actions you can currently perform on this application. A custom application allows `deploy`, `update`, `edit`, `delete` and `download-files`; a Patch My PC catalog application allows `deploy` only. Can be `null`.                                                                                   |
| `updateId`        | string (uuid)                                                                | No       | Deprecated: a custom application's update identifier, retained for compatibility with existing clients. Use `custom.updateId` instead.                                                                                                                                                                     |
| `displayName`     | string                                                                       | No       | The application's display name. Can be `null`.                                                                                                                                                                                                                                                             |
| `description`     | string                                                                       | No       | A description of the application. Can be `null`.                                                                                                                                                                                                                                                           |
| `vendorName`      | string                                                                       | No       | The name of the application's publisher (vendor). Can be `null`.                                                                                                                                                                                                                                           |
| `language`        | string                                                                       | No       | The application's language code, for example `en-US`. Can be `null`.                                                                                                                                                                                                                                       |
| `iconURL`         | string                                                                       | No       | A reference to the application's icon file. This is a key, not a download link; to get the icon image, set `includeIconData` in the search request. Can be `null`.                                                                                                                                         |
| `iconBase64`      | string                                                                       | No       | The application's icon image, Base64-encoded. Set only when the search request sets `includeIconData` to `true` and the icon could be retrieved. Can be `null`.                                                                                                                                            |
| `iconContentType` | string                                                                       | No       | The MIME type of the icon in `iconBase64`, for example `image/png`. Set only when `iconBase64` is set. Can be `null`.                                                                                                                                                                                      |
| `state`           | [`UpdateState`](applications.md#updatestate)                                 | No       | The current state of the application version.                                                                                                                                                                                                                                                              |
| `lastUpdated`     | string (date-time)                                                           | No       | When the application was last updated, as an ISO 8601 date and time with a UTC offset.                                                                                                                                                                                                                     |
| `version`         | string                                                                       | No       | The application's latest version number for the searched operating system. An empty string when no version is available for that operating system. For a Patch My PC catalog application this is not a specific selectable variant; use the variants in the application details. Read-only. Can be `null`. |

### PublicApplicationDto

| Name              | Type                                                                                  | Required | Description                                                                                                                                                                                                                                                                                                          |
| ----------------- | ------------------------------------------------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `productId`       | string (uuid)                                                                         | No       | The application's ID. Read-only.                                                                                                                                                                                                                                                                                     |
| `type`            | string                                                                                | No       | The application type: `pmpc` for a Patch My PC catalog application, or `custom` for one of your custom applications. Read-only. Can be `null`.                                                                                                                                                                       |
| `displayName`     | string                                                                                | No       | The application's display name. Read-only. Can be `null`.                                                                                                                                                                                                                                                            |
| `description`     | string                                                                                | No       | A description of the application. Read-only. Can be `null`.                                                                                                                                                                                                                                                          |
| `language`        | string                                                                                | No       | The application's language code, for example `en-US`. Read-only. Can be `null`.                                                                                                                                                                                                                                      |
| `vendorName`      | string                                                                                | No       | The name of the application's publisher (vendor). Read-only. Can be `null`.                                                                                                                                                                                                                                          |
| `updateVersion`   | string                                                                                | No       | The version number of the application's latest version. Read-only. Can be `null`.                                                                                                                                                                                                                                    |
| `iconURL`         | string                                                                                | No       | A reference to the application's icon file. This is a key, not a download link; the icon image itself is returned in `iconBase64`. Read-only. Can be `null`.                                                                                                                                                         |
| `iconBase64`      | string                                                                                | No       | The application's icon image, Base64-encoded. `null` when the application has no icon or the icon could not be retrieved. Read-only. Can be `null`.                                                                                                                                                                  |
| `iconContentType` | string                                                                                | No       | The MIME type of the icon in `iconBase64`, for example `image/png`. Set only when `iconBase64` is set. Read-only. Can be `null`.                                                                                                                                                                                     |
| `privacyUrl`      | string                                                                                | No       | The URL of the application's privacy policy. Read-only. Can be `null`.                                                                                                                                                                                                                                               |
| `informationUrl`  | string                                                                                | No       | The URL of a web page with more information about the application. Read-only. Can be `null`.                                                                                                                                                                                                                         |
| `developer`       | string                                                                                | No       | The application's developer. Read-only. Can be `null`.                                                                                                                                                                                                                                                               |
| `intuneNotes`     | string                                                                                | No       | Notes to include with the application in Microsoft Intune. Read-only. Can be `null`.                                                                                                                                                                                                                                 |
| `installerType`   | [`InstallerType`](applications.md#installertype)                                      | No       | The type of installer the application uses, for example `MSI` or `EXE`. Read-only.                                                                                                                                                                                                                                   |
| `architecture`    | [`RequirementArchitecture`](applications.md#requirementarchitecture)                  | No       | The processor architecture a device must have to install the application. Read-only.                                                                                                                                                                                                                                 |
| `installContext`  | [`InstallationBehavior`](applications.md#installationbehavior)                        | No       | The context the application installs in, for example `System` or `User`. Read-only. Can be `null`.                                                                                                                                                                                                                   |
| `actions`         | array of string                                                                       | No       | The actions you can currently perform on this application. A custom application allows `deploy`, `update`, `edit`, `delete` and `download-files`; a Patch My PC catalog application allows `deploy` only. Read-only. Can be `null`.                                                                                  |
| `variants`        | array of [`PublicApplicationVariantDto`](applications.md#publicapplicationvariantdto) | No       | Deployable variants for the requested operating system. Each variant contains its own language, version, installer type, architecture, and install context. Its pmpc.appcatbroker.api.DTOs.PublicApplicationVariantDto.CatalogEntryId can be supplied as `CatalogEntryId` when creating a deployment. Can be `null`. |

### PublicApplicationVariantDto

| Name             | Type                                                                 | Required | Description                                                                                         |
| ---------------- | -------------------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------- |
| `productId`      | string (uuid)                                                        | No       | Owning product identifier, retaining context when this variant is selected independently.           |
| `catalogEntryId` | string (uuid)                                                        | No       | Stable variant identifier, corresponding to the AppCat category ID used when creating a deployment. |
| `osType`         | [`OSType`](applications.md#ostype)                                   | No       | Operating system this variant can be deployed to.                                                   |
| `architecture`   | [`RequirementArchitecture`](applications.md#requirementarchitecture) | No       | CPU architecture of this variant.                                                                   |
| `installerType`  | [`InstallerType`](applications.md#installertype)                     | No       | Installer type used by this variant.                                                                |
| `installContext` | [`InstallationBehavior`](applications.md#installationbehavior)       | No       | Installation context, when applicable. Can be `null`.                                               |
| `language`       | string                                                               | No       | Language of this variant. Can be `null`.                                                            |
| `updateVersion`  | string                                                               | No       | Version currently available for deployment. Can be `null`.                                          |
| `revisionId`     | integer (int32)                                                      | No       | Revision of the available update.                                                                   |

### RegistryRuleDto

| Name                   | Type                                                                     | Required | Description                                                                                                                                         |
| ---------------------- | ------------------------------------------------------------------------ | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operator`             | [`RuleOperator`](applications.md#ruleoperator)                           | No       | How the detected value is compared with `comparisonValue`.                                                                                          |
| `check32BitOn64System` | boolean                                                                  | No       | When `true`, checks the 32-bit registry view (WOW6432Node) on a 64-bit system.                                                                      |
| `keyPath`              | string                                                                   | No       | Full path of the registry key to check. Can be `null`.                                                                                              |
| `valueName`            | string                                                                   | No       | Name of the registry value to check within `keyPath`. Omit to check the key itself. Can be `null`.                                                  |
| `operationType`        | [`RegistryRuleOperationType`](applications.md#registryruleoperationtype) | No       | What to check about the registry key or value, such as whether it exists, or its string, integer or version value.                                  |
| `comparisonValue`      | string                                                                   | No       | The value the detected value is compared with. Required when `operationType` compares a value, such as a string, integer or version. Can be `null`. |

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

| Name                    | Type                                                                 | Required | Description                                                                                                                                   |
| ----------------------- | -------------------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `operator`              | [`RuleOperator`](applications.md#ruleoperator)                       | No       | How the script's output is compared with `comparisonValue`.                                                                                   |
| `displayName`           | string                                                               | No       | Display name for the script rule. Can be `null`.                                                                                              |
| `runAsAccount`          | boolean                                                              | No       | Set to `true` to run the script as the signed-in user instead of the system account. When `null`, the default account is used. Can be `null`. |
| `comparisonValue`       | string                                                               | No       | The value the script's output is compared with. Required when `operationType` compares a value. Can be `null`.                                |
| `enforceSignatureCheck` | boolean                                                              | No       | When `true`, the script must have a valid digital signature before it runs.                                                                   |
| `runAs32Bit`            | boolean                                                              | No       | When `true`, the script runs in a 32-bit process on 64-bit systems.                                                                           |
| `scriptContent`         | string                                                               | No       | The full text of the script to run. Supply the script content, not a path to a script file. Can be `null`.                                    |
| `operationType`         | [`ScriptRuleOperationType`](applications.md#scriptruleoperationtype) | No       | The data type the script's output is read as, such as string, integer, version or boolean.                                                    |

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

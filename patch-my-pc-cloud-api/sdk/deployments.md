---
description: >-
  SDK methods that list, create, edit, delete, redeploy, sync, and pause
  deployments of an application to Microsoft Intune.
noIndex: true
noRobotsIndex: true
---

# Deployments

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

A deployment publishes an application to Microsoft Intune through one of your connections, with group assignments and optional configuration. These methods manage the deployments of a single application.

Every method on this page needs a selected company and a selected connection. If no connection is selected, the method fails with `VALIDATION_ERROR` before it calls the Patch My PC Cloud Customer API. To select one, see [`SetSelectedConnectionAsync`](customer-and-connections.md#setselectedconnectionasync). With a personal access token (PAT), these methods need the `appcatbroker:apps:deploy` scope.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

Every method on this page requires the feature described above.

## Models

The deployment models are in the `PatchMyPC.Cloud.Client` namespace.

### Deployment

`DeploymentDto` is the summary of a deployment that list, create, and edit methods return.

| Property          | Type                   | Description                                                                                                                                                                  |
| ----------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `DeploymentId`    | `string`               | The deployment ID. Pass it to the other methods on this page.                                                                                                                |
| `ProductId`       | `Guid`                 | The application the deployment publishes.                                                                                                                                    |
| `DisplayName`     | `string`               | The deployment name.                                                                                                                                                         |
| `OsType`          | `OSType`               | The target operating system.                                                                                                                                                 |
| `Status`          | `DeploymentStatusType` | The current status of the deployment.                                                                                                                                        |
| `WarningMessages` | collection of `string` | Non-fatal warnings, for example a profile or scope tag that couldn't be applied. Empty when there's nothing to report.                                                       |
| `SyncOnHold`      | `bool`                 | Whether scheduled sync is paused.                                                                                                                                            |
| `RingsEnabled`    | `bool`                 | Whether the deployment uses deployment rings. Ring-enabled deployments can't be edited with the SDK.                                                                         |
| `Actions`         | collection of `string` | The operations currently valid for the deployment's state: `edit`, `delete`, `redeploy`, `sync`, `pause-sync`, and `resume-sync`. These reflect state, not your permissions. |

### Deployment details

`DeploymentDetailDto` has every property of `DeploymentDto`, plus these.

| Property            | Type                                                                       | Description                                                                                                                                                                  |
| ------------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Version`           | `string?`                                                                  | The application version the deployment is publishing.                                                                                                                        |
| `ErrorMessages`     | collection of `string`                                                     | Why the deployment last failed. Empty when it hasn't failed.                                                                                                                 |
| `Assignments`       | collection of assignments                                                  | The groups or targets the deployment is assigned to. Each has `GroupId`, `GroupName`, `TargetType`, and `Intent`. `GroupId` is `null` for All Users and All Devices targets. |
| `Categories`        | collection                                                                 | Company Portal categories, each with `Id` and `DisplayName`.                                                                                                                 |
| `EspProfiles`       | collection                                                                 | Enrollment Status Page (ESP) profiles, each with `Id`, `DisplayName`, and `ApplicationsCount`.                                                                               |
| `ParentDeployments` | collection of [dependency candidates](deployments.md#dependency-candidate) | Deployments this one depends on.                                                                                                                                             |
| `ChildDeployments`  | collection of [dependency candidates](deployments.md#dependency-candidate) | Deployments that depend on this one.                                                                                                                                         |
| `Configuration`     | object                                                                     | The deployment's stored configuration.                                                                                                                                       |

### Dependency candidate

`DeploymentDependencyDto` identifies a deployment that another deployment can depend on.

| Property          | Type              | Description                                                                    |
| ----------------- | ----------------- | ------------------------------------------------------------------------------ |
| `DeploymentId`    | `string`          | The deployment ID. Use this value in `ParentDeploymentIds`.                    |
| `Id`              | `string`          | The same value as `DeploymentId`. Prefer `DeploymentId`.                       |
| `Name`            | `string?`         | The deployment name.                                                           |
| `IconUrl`         | `string?`         | The application's icon URL.                                                    |
| `CatalogFeedType` | `CatalogFeedType` | Whether the application is from the public catalog or is a custom application. |

### Create deployment request

`CreateDeploymentRequest` describes a new deployment.

| Property              | Type                                      | Description                                                                                                                                                    |
| --------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `OsType`              | `OSType`                                  | Required. The target operating system.                                                                                                                         |
| `Assignments`         | `List<CreateDeploymentAssignmentRequest>` | Required. The [assignments](deployments.md#assignment).                                                                                                        |
| `CategoryIds`         | `List<string>?`                           | Optional. Company Portal category IDs.                                                                                                                         |
| `EspProfileIds`       | `List<string>?`                           | Optional. ESP profile IDs. You need to know these IDs already; the SDK has no method to list them.                                                             |
| `ParentDeploymentIds` | `List<string>?`                           | Optional. Deployments this one depends on. Use [`GetDeploymentDependencyCandidatesAsync`](deployments.md#getdeploymentdependencycandidatesasync) to find them. |
| `Configuration`       | `DeploymentConfigurationRequest?`         | Optional. The [deployment configuration](deployments.md#deployment-configuration). `null` uses the defaults.                                                   |
| `ConnectionId`        | `Guid`                                    | Set automatically to your selected connection. Any value you set is replaced.                                                                                  |

### Edit deployment request

`EditDeploymentRequest` describes changes to a deployment. A `null` property leaves the current value unchanged.

| Property                                              | Type                                       | Description                                                                                                                                             |
| ----------------------------------------------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Name`                                                | `string?`                                  | A new name. It must be unique on the connection; a duplicate fails with `VALIDATION_ERROR`.                                                             |
| `Assignments`                                         | `List<CreateDeploymentAssignmentRequest>?` | The complete set of [assignments](deployments.md#assignment). Replaces all existing assignments.                                                        |
| `CategoryIds`, `EspProfileIds`, `ParentDeploymentIds` | `List<string>?`                            | The complete set of each. Replaces the existing set; an empty list clears it.                                                                           |
| `Configuration`                                       | `DeploymentConfigurationRequest?`          | [Configuration](deployments.md#deployment-configuration) changes. Within it, a `null` member keeps the current value and an empty collection clears it. |
| `ConnectionId`                                        | `Guid`                                     | Set automatically to your selected connection. Any value you set is replaced.                                                                           |

### Assignment

`CreateDeploymentAssignmentRequest` pairs an installation intent with a target.

| Property     | Type                    | Description                                                                                                                                                                                                                                   |
| ------------ | ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Intent`     | `InstallationIntent`    | Required. `Required`, `Available`, `Uninstall`, `UpdateOnly`, `NoAssignmentsInstall`, or `NoAssignmentsUpdate`.                                                                                                                               |
| `GroupId`    | `string?`               | The Microsoft Entra ID group to target. Required when the assignment targets a group.                                                                                                                                                         |
| `TargetType` | `AssignmentTargetType?` | `null` or `Group` targets `GroupId`. `AllUsers` and `AllDevices` target everyone and take no group. `NotSet` is required for the `NoAssignmentsInstall` and `NoAssignmentsUpdate` intents, which deploy the application without assigning it. |

### Deployment configuration

`DeploymentConfigurationRequest` holds optional settings. Every member is optional; `null` uses the default for a new deployment.

| Property                  | Type                               | Description                                                                                                                                                                                                    |
| ------------------------- | ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `AdditionalArgument`      | `string?`                          | Extra command-line arguments for the installer.                                                                                                                                                                |
| `InstallLoggingPath`      | `string?`                          | The folder the installation log is written to.                                                                                                                                                                 |
| `CustomRequirements`      | object                             | Requirement rules, for example minimum operating system version, memory, or processor.                                                                                                                         |
| `AppInfo`                 | `DeploymentAppInfoDto?`            | Overrides for the information shown in the Company Portal: `CustomVendor`, `CustomDeveloper`, `CustomOwner`, `CustomDescription`, `CustomNotes`, `CustomInformationUrl`, `CustomPrivacyUrl`, and `IsFeatured`. |
| `ConflictingProcess`      | `DeploymentConflictingProcessDto?` | What happens when a conflicting process is running, including the policy, added or removed processes, and user notifications.                                                                                  |
| `ReturnCodes`             | `List<DeploymentReturnCodeDto>?`   | Installer exit codes, each with `Code` and `Type`.                                                                                                                                                             |
| `BuiltInUpdate`           | `BuiltInUpdate?`                   | Whether the application's own updater is enabled or disabled.                                                                                                                                                  |
| `AllowAvailableUninstall` | `bool?`                            | Whether users can uninstall the application from the Company Portal. Defaults to `false`.                                                                                                                      |
| `RemoveDesktopShortcuts`  | `bool?`                            | Whether to remove desktop shortcuts after installation. Defaults to `false`.                                                                                                                                   |
| `AppVersionsRetention`    | `int?`                             | How many previous versions to keep in Intune. Defaults to `0`, which turns retention off.                                                                                                                      |
| `RoleScopeTagIds`         | `List<string>?`                    | Intune scope tag IDs to apply.                                                                                                                                                                                 |

## Methods

### GetDeploymentsAsync

Lists the deployments of an application on the selected connection.

```csharp
Task<Result<IReadOnlyList<DeploymentDto>>> GetDeploymentsAsync(
    Guid productId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                   |
| ------------------- | ------------------- | ----------------------------- |
| `productId`         | `Guid`              | Required. The application ID. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.   |

**Returns:** a list of [`DeploymentDto`](deployments.md#deployment). The list leaves out assignments, categories, profiles, and dependencies; use [`GetDeploymentDetailsAsync`](deployments.md#getdeploymentdetailsasync) for those.

```csharp
var deployments = await client.GetDeploymentsAsync(productId);
if (deployments.IsFailure)
{
    Console.WriteLine($"Couldn't list deployments: {deployments.Error.Code} {deployments.Error.Message}");
    return;
}

foreach (var deployment in deployments.Value)
{
    Console.WriteLine($"{deployment.DeploymentId} {deployment.DisplayName} {deployment.Status} paused={deployment.SyncOnHold}");
}
```

**See also:** [Get-PmpcDeployment](../powershell/get-pmpcdeployment.md) and [Get application deployments](../rest-api/applications.md#get-application-deployments).

### GetDeploymentDetailsAsync

Gets one deployment in full, including its assignments, categories, profiles, dependencies, and configuration.

```csharp
Task<Result<DeploymentDetailDto>> GetDeploymentDetailsAsync(
    Guid productId,
    string deploymentId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                   |
| ------------------- | ------------------- | ----------------------------- |
| `productId`         | `Guid`              | Required. The application ID. |
| `deploymentId`      | `string`            | Required. The deployment ID.  |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.   |

**Returns:** a [`DeploymentDetailDto`](deployments.md#deployment-details). If the deployment doesn't exist, the error code is `NOT_FOUND`.

```csharp
var details = await client.GetDeploymentDetailsAsync(productId, deploymentId);
if (details.IsFailure)
{
    Console.WriteLine($"Couldn't read the deployment: {details.Error.Code} {details.Error.Message}");
    return;
}

Console.WriteLine($"{details.Value.DisplayName} publishes version {details.Value.Version}");
foreach (var error in details.Value.ErrorMessages)
{
    Console.WriteLine($"Last failure: {error}");
}
```

**See also:** [Get-PmpcDeployment](../powershell/get-pmpcdeployment.md) and [Get application deployment details](../rest-api/applications.md#get-application-deployment-details).

### GetDeploymentDependencyCandidatesAsync

Lists the deployments that a deployment can depend on.

```csharp
Task<Result<IReadOnlyList<DeploymentDependencyDto>>> GetDeploymentDependencyCandidatesAsync(
    Guid productId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                                                    |
| ------------------- | ------------------- | -------------------------------------------------------------- |
| `productId`         | `Guid`              | Required. The application you're configuring dependencies for. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.                                    |

**Returns:** a list of [`DeploymentDependencyDto`](deployments.md#dependency-candidate).

The list covers every deployment on the selected connection, not only those related to `productId`; the application ID isn't used to filter the results.

```csharp
var candidates = await client.GetDeploymentDependencyCandidatesAsync(productId);
if (candidates.IsFailure)
{
    Console.WriteLine($"Couldn't list candidates: {candidates.Error.Code} {candidates.Error.Message}");
    return;
}

foreach (var candidate in candidates.Value)
{
    Console.WriteLine($"{candidate.DeploymentId} {candidate.Name}");
}
```

**See also:** [Get-PmpcDeploymentDependencyCandidate](../powershell/get-pmpcdeploymentdependencycandidate.md) and [Get application deployment dependency candidates](../rest-api/applications.md#get-application-deployment-dependency-candidates).

### CreateDeploymentAsync

Creates a deployment of an application on the selected connection.

```csharp
Task<Result<DeploymentDto>> CreateDeploymentAsync(
    Guid productId,
    CreateDeploymentRequest request,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                                                                  | Description                             |
| ------------------- | --------------------------------------------------------------------- | --------------------------------------- |
| `productId`         | `Guid`                                                                | Required. The application to deploy.    |
| `request`           | [`CreateDeploymentRequest`](deployments.md#create-deployment-request) | Required. The assignments and settings. |
| `cancellationToken` | `CancellationToken`                                                   | Optional. Cancels the call.             |

**Returns:** the new [`DeploymentDto`](deployments.md#deployment).

```csharp
using PatchMyPC.Cloud.Client;

var created = await client.CreateDeploymentAsync(productId, new CreateDeploymentRequest
{
    OsType = OSType.Windows,
    Assignments = new List<CreateDeploymentAssignmentRequest>
    {
        new CreateDeploymentAssignmentRequest
        {
            GroupId = "{group-id}",
            Intent = InstallationIntent.Required
        }
    },
    Configuration = new DeploymentConfigurationRequest
    {
        AllowAvailableUninstall = true
    }
});

if (created.IsFailure)
{
    Console.WriteLine($"Create failed: {created.Error.Code} {created.Error.Message}");
    return;
}

Console.WriteLine($"Created {created.Value.DeploymentId} ({created.Value.Status})");
```

**See also:** [New-PmpcDeployment](../powershell/new-pmpcdeployment.md) and [Create application deployment](../rest-api/applications.md#create-application-deployment).

### EditDeploymentAsync

Changes an existing deployment.

```csharp
Task<Result<DeploymentDto>> EditDeploymentAsync(
    Guid productId,
    string deploymentId,
    EditDeploymentRequest request,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                                                              | Description                                                  |
| ------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------ |
| `productId`         | `Guid`                                                            | Required. The application ID.                                |
| `deploymentId`      | `string`                                                          | Required. The deployment to change.                          |
| `request`           | [`EditDeploymentRequest`](deployments.md#edit-deployment-request) | Required. The changes. `null` properties are left unchanged. |
| `cancellationToken` | `CancellationToken`                                               | Optional. Cancels the call.                                  |

**Returns:** the updated [`DeploymentDto`](deployments.md#deployment).

Deployments that use deployment rings can't be edited with this method. When you set `Assignments`, the list replaces every existing assignment, so include the ones you want to keep.

```csharp
var edited = await client.EditDeploymentAsync(productId, deploymentId, new EditDeploymentRequest
{
    Name = "{new-deployment-name}",
    CategoryIds = new List<string>()
});

if (edited.IsFailure)
{
    Console.WriteLine($"Edit failed: {edited.Error.Code} {edited.Error.Message}");
    return;
}

Console.WriteLine($"Renamed to {edited.Value.DisplayName}");
```

**See also:** [Set-PmpcDeployment](../powershell/set-pmpcdeployment.md) and [Edit application deployment](../rest-api/applications.md#edit-application-deployment).

### DeleteDeploymentAsync

Deletes a deployment.

```csharp
Task<Result> DeleteDeploymentAsync(
    Guid productId,
    string deploymentId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                         |
| ------------------- | ------------------- | ----------------------------------- |
| `productId`         | `Guid`              | Required. The application ID.       |
| `deploymentId`      | `string`            | Required. The deployment to delete. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.         |

**Returns:** a `Result` that indicates success or failure.

You can delete a deployment only when it isn't in progress or already being deleted. Check for `delete` in the deployment's `Actions` first.

```csharp
var delete = await client.DeleteDeploymentAsync(productId, deploymentId);
if (delete.IsFailure)
{
    Console.WriteLine($"Delete failed: {delete.Error.Code} {delete.Error.Message}");
    return;
}
```

**See also:** [Remove-PmpcDeployment](../powershell/remove-pmpcdeployment.md) and [Delete application deployment](../rest-api/applications.md#delete-application-deployment).

### RedeployDeploymentAsync

Re-creates a deployment in Microsoft Intune.

```csharp
Task<Result> RedeployDeploymentAsync(
    Guid productId,
    string deploymentId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                           |
| ------------------- | ------------------- | ------------------------------------- |
| `productId`         | `Guid`              | Required. The application ID.         |
| `deploymentId`      | `string`            | Required. The deployment to redeploy. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.           |

**Returns:** a `Result` that indicates success or failure.

Use this method to troubleshoot a deployment that's in a bad state in Intune.

```csharp
var redeploy = await client.RedeployDeploymentAsync(productId, deploymentId);
if (redeploy.IsFailure)
{
    Console.WriteLine($"Redeploy failed: {redeploy.Error.Code} {redeploy.Error.Message}");
}
```

**See also:** [Restart-PmpcDeployment](../powershell/restart-pmpcdeployment.md) and [Redeploy application deployment](../rest-api/applications.md#redeploy-application-deployment).

### SyncDeploymentAsync

Updates a deployment to the latest available version of its application.

```csharp
Task<Result> SyncDeploymentAsync(
    Guid productId,
    string deploymentId,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                       |
| ------------------- | ------------------- | --------------------------------- |
| `productId`         | `Guid`              | Required. The application ID.     |
| `deploymentId`      | `string`            | Required. The deployment to sync. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.       |

**Returns:** a `Result` that indicates success or failure.

```csharp
var sync = await client.SyncDeploymentAsync(productId, deploymentId);
if (sync.IsFailure)
{
    Console.WriteLine($"Sync failed: {sync.Error.Code} {sync.Error.Message}");
}
```

**See also:** [Sync-PmpcDeployment](../powershell/sync-pmpcdeployment.md) and [Sync application deployment](../rest-api/applications.md#sync-application-deployment).

### SetDeploymentSyncPauseStatusAsync

Pauses or resumes scheduled sync for a deployment.

```csharp
Task<Result> SetDeploymentSyncPauseStatusAsync(
    Guid productId,
    string deploymentId,
    bool pause,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                                                 |
| ------------------- | ------------------- | ----------------------------------------------------------- |
| `productId`         | `Guid`              | Required. The application ID.                               |
| `deploymentId`      | `string`            | Required. The deployment.                                   |
| `pause`             | `bool`              | Required. `true` pauses scheduled sync; `false` resumes it. |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call.                                 |

**Returns:** a `Result` that indicates success or failure.

The paused state appears as `SyncOnHold` on the [deployment](deployments.md#deployment). Resuming doesn't push a new version; to update right away, call [`SyncDeploymentAsync`](deployments.md#syncdeploymentasync).

```csharp
var pause = await client.SetDeploymentSyncPauseStatusAsync(productId, deploymentId, pause: true);
if (pause.IsFailure)
{
    Console.WriteLine($"Couldn't pause sync: {pause.Error.Code} {pause.Error.Message}");
}
```

**See also:** [Suspend-PmpcDeployment](../powershell/suspend-pmpcdeployment.md), [Resume-PmpcDeployment](../powershell/resume-pmpcdeployment.md), and [Set application deployment sync pause status](../rest-api/applications.md#set-application-deployment-sync-pause-status).

---
description: >-
  SDK methods that list, read, create, update, and delete deployment templates
  on the selected connection.
noIndex: true
noRobotsIndex: true
---

# Deployment templates

A deployment template is a named set of deployment settings stored on a connection, such as requirements, Company Portal information, categories, and update behavior. Use templates to keep your deployments consistent.

Every method on this page needs a selected company and a selected connection; templates belong to the selected connection. If no connection is selected, the method fails with `VALIDATION_ERROR`. To select one, see [`SetSelectedConnectionAsync`](customer-and-connections.md#setselectedconnectionasync). With a personal access token (PAT), these methods need the `appcatbroker:apps:deploy` scope.

{% hint style="info" %}
This feature must be enabled for your account. Until it is, requests return `403 Forbidden` with the problem title `feature_not_enabled`, and the SDK and PowerShell module report the error code `FEATURE_NOT_ENABLED`.
{% endhint %}

Every method on this page requires the feature described above.

[`CreateDeploymentAsync`](deployments.md#createdeploymentasync) doesn't take a template. To start a deployment from a template, read the template with [`GetDeploymentTemplateAsync`](deployment-templates.md#getdeploymenttemplateasync) and copy the settings you want into your [create deployment request](deployments.md#create-deployment-request). Template settings for custom scripts, the PowerShell App Deployment Toolkit (PSADT), and deployment rings aren't available through the SDK.

## Models

The template models are in the `pmpc.appcatbroker.client` namespace.

### Deployment template request

`DeploymentTemplateRequest` describes a template to create or the complete replacement for an existing one.

| Property                                                        | Type                                       | Description                                                                                                                        |
| --------------------------------------------------------------- | ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| `TemplateName`                                                  | `string`                                   | Required. The template name.                                                                                                       |
| `OsType`                                                        | `OSType`                                   | Required. The operating system the template applies to. A template belongs to one operating system.                                |
| `IsDefault`                                                     | `bool`                                     | Whether this is the connection's default template. A connection has exactly one default; setting this demotes the current default. |
| `BuiltInUpdate`                                                 | `BuiltInUpdate`                            | Whether the application's own updater is enabled or disabled.                                                                      |
| `AllowAvailableUninstall`                                       | `bool`                                     | Whether users can uninstall the application from the Company Portal.                                                               |
| `RemoveDesktopShortcuts`                                        | `bool`                                     | Whether to remove desktop shortcuts after installation.                                                                            |
| `AppVersionsRetention`                                          | `int`                                      | How many previous versions to keep in Intune. `0` turns retention off.                                                             |
| `CustomVendor`, `CustomDeveloper`, `CustomOwner`, `CustomNotes` | `string?`                                  | Company Portal information for deployments created from the template.                                                              |
| `CopyForwardAssignments`                                        | `bool`                                     | Whether deployments created from the template inherit its assignments.                                                             |
| `CategoryIds`, `EspProfileIds`, `RoleScopeTagIds`               | `List<string>?`                            | Company Portal categories, Enrollment Status Page (ESP) profiles, and Intune scope tags.                                           |
| `CustomRequirements`                                            | `EditDeploymentCustomRequirementsRequest?` | Requirement rules, for example `MinimumWindowsOSVersion` and `MinimumMemoryInMB`.                                                  |
| `ConnectionId`                                                  | `Guid`                                     | Set automatically to your selected connection. Any value you set is replaced.                                                      |

### Deployment template summary

`DeploymentTemplateSummaryDto` is the list form of a template.

| Property                      | Type                   | Description                                                                                                        |
| ----------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `DeploymentTemplateId`        | `string`               | The template ID.                                                                                                   |
| `TemplateName`                | `string`               | The template name.                                                                                                 |
| `IsDefault`                   | `bool`                 | Whether this is the connection's default template.                                                                 |
| `OsType`                      | `OSType`               | The operating system the template applies to.                                                                      |
| `CreatedAt`, `LastModifiedAt` | `DateTimeOffset`       | When the template was created and last changed.                                                                    |
| `Actions`                     | collection of `string` | The operations currently valid for the template: `edit` and `delete`. The default template doesn't offer `delete`. |

### Deployment template

`DeploymentTemplateDto` is the full template. It has `DeploymentTemplateId`, `TemplateName`, `IsDefault`, `OsType`, `Actions`, and the settings described in the [deployment template request](deployment-templates.md#deployment-template-request). Categories, ESP profiles, and scope tags are returned as `Categories`, `EspProfiles`, and `RoleScopeTags`, each a collection of objects with `Id` and `DisplayName`, rather than as ID lists.

## Methods

### GetDeploymentTemplatesAsync

Lists the deployment templates on the selected connection.

```csharp
Task<Result<IReadOnlyList<DeploymentTemplateSummaryDto>>> GetDeploymentTemplatesAsync(
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                | Description                 |
| ------------------- | ------------------- | --------------------------- |
| `cancellationToken` | `CancellationToken` | Optional. Cancels the call. |

**Returns:** a list of [`DeploymentTemplateSummaryDto`](deployment-templates.md#deployment-template-summary).

```csharp
var templates = await broker.GetDeploymentTemplatesAsync();
if (templates.IsFailure)
{
    Console.WriteLine($"Couldn't list templates: {templates.Error.Code} {templates.Error.Message}");
    return;
}

foreach (var template in templates.Value)
{
    var marker = template.IsDefault ? " (default)" : string.Empty;
    Console.WriteLine($"{template.DeploymentTemplateId} {template.TemplateName}{marker}");
}
```

**See also:** [Get-PmpcDeploymentTemplate](../powershell/get-pmpcdeploymenttemplate.md) and [Get deployment templates](../rest-api/applications.md#get-deployment-templates).

### GetDeploymentTemplateAsync

Gets the full settings of one deployment template.

```csharp
Task<Result<DeploymentTemplateDto>> GetDeploymentTemplateAsync(
    string deploymentTemplateId,
    CancellationToken cancellationToken = default);
```

| Parameter              | Type                | Description                 |
| ---------------------- | ------------------- | --------------------------- |
| `deploymentTemplateId` | `string`            | Required. The template ID.  |
| `cancellationToken`    | `CancellationToken` | Optional. Cancels the call. |

**Returns:** a [`DeploymentTemplateDto`](deployment-templates.md#deployment-template). If the template doesn't exist, the error code is `NOT_FOUND`.

```csharp
var template = await broker.GetDeploymentTemplateAsync(templateId);
if (template.IsFailure)
{
    Console.WriteLine($"Couldn't read the template: {template.Error.Code} {template.Error.Message}");
    return;
}

Console.WriteLine($"{template.Value.TemplateName}: retention {template.Value.AppVersionsRetention}");
```

**See also:** [Get-PmpcDeploymentTemplate](../powershell/get-pmpcdeploymenttemplate.md) and [Get deployment template details](../rest-api/applications.md#get-deployment-template-details).

### CreateDeploymentTemplateAsync

Creates a deployment template on the selected connection.

```csharp
Task<Result<DeploymentTemplateDto>> CreateDeploymentTemplateAsync(
    DeploymentTemplateRequest request,
    CancellationToken cancellationToken = default);
```

| Parameter           | Type                                                                               | Description                      |
| ------------------- | ---------------------------------------------------------------------------------- | -------------------------------- |
| `request`           | [`DeploymentTemplateRequest`](deployment-templates.md#deployment-template-request) | Required. The template settings. |
| `cancellationToken` | `CancellationToken`                                                                | Optional. Cancels the call.      |

**Returns:** the new [`DeploymentTemplateDto`](deployment-templates.md#deployment-template).

```csharp
using pmpc.appcatbroker.client;

var created = await broker.CreateDeploymentTemplateAsync(new DeploymentTemplateRequest
{
    TemplateName = "{template-name}",
    OsType = OSType.Windows,
    IsDefault = false,
    AllowAvailableUninstall = true,
    CustomRequirements = new EditDeploymentCustomRequirementsRequest
    {
        MinimumWindowsOSVersion = WindowsOSVersion.Windows11_21H2,
        MinimumMemoryInMB = 4096
    }
});

if (created.IsFailure)
{
    Console.WriteLine($"Create failed: {created.Error.Code} {created.Error.Message}");
    return;
}

Console.WriteLine($"Created template {created.Value.DeploymentTemplateId}");
```

**See also:** [New-PmpcDeploymentTemplate](../powershell/new-pmpcdeploymenttemplate.md) and [Create deployment template](../rest-api/applications.md#create-deployment-template).

### UpdateDeploymentTemplateAsync

Replaces the settings of an existing deployment template.

```csharp
Task<Result<DeploymentTemplateDto>> UpdateDeploymentTemplateAsync(
    string deploymentTemplateId,
    DeploymentTemplateRequest request,
    CancellationToken cancellationToken = default);
```

| Parameter              | Type                                                                               | Description                          |
| ---------------------- | ---------------------------------------------------------------------------------- | ------------------------------------ |
| `deploymentTemplateId` | `string`                                                                           | Required. The template to update.    |
| `request`              | [`DeploymentTemplateRequest`](deployment-templates.md#deployment-template-request) | Required. The complete new settings. |
| `cancellationToken`    | `CancellationToken`                                                                | Optional. Cancels the call.          |

**Returns:** the updated [`DeploymentTemplateDto`](deployment-templates.md#deployment-template).

Every setting is stored exactly as you send it, so a property you leave out is cleared or reset. Read the template first with [`GetDeploymentTemplateAsync`](deployment-templates.md#getdeploymenttemplateasync) and send back the settings you want to keep.

```csharp
var current = await broker.GetDeploymentTemplateAsync(templateId);
if (current.IsFailure)
{
    Console.WriteLine($"Couldn't read the template: {current.Error.Code} {current.Error.Message}");
    return;
}

var t = current.Value;
var updated = await broker.UpdateDeploymentTemplateAsync(templateId, new DeploymentTemplateRequest
{
    TemplateName = t.TemplateName,
    OsType = t.OsType,
    IsDefault = t.IsDefault,
    BuiltInUpdate = t.BuiltInUpdate,
    AllowAvailableUninstall = t.AllowAvailableUninstall,
    RemoveDesktopShortcuts = t.RemoveDesktopShortcuts,
    AppVersionsRetention = 3,
    CustomVendor = t.CustomVendor,
    CustomDeveloper = t.CustomDeveloper,
    CustomOwner = t.CustomOwner,
    CustomNotes = t.CustomNotes,
    CopyForwardAssignments = t.CopyForwardAssignments,
    CategoryIds = t.Categories.Select(c => c.Id).ToList(),
    EspProfileIds = t.EspProfiles.Select(p => p.Id).ToList(),
    RoleScopeTagIds = t.RoleScopeTags.Select(s => s.Id).ToList()
});

if (updated.IsFailure)
{
    Console.WriteLine($"Update failed: {updated.Error.Code} {updated.Error.Message}");
}
```

This example doesn't copy `CustomRequirements`, so the update clears them. Copy them too if you want to keep them.

**See also:** [Set-PmpcDeploymentTemplate](../powershell/set-pmpcdeploymenttemplate.md) and [Update deployment template](../rest-api/applications.md#update-deployment-template).

### DeleteDeploymentTemplateAsync

Deletes a deployment template.

```csharp
Task<Result> DeleteDeploymentTemplateAsync(
    string deploymentTemplateId,
    CancellationToken cancellationToken = default);
```

| Parameter              | Type                | Description                       |
| ---------------------- | ------------------- | --------------------------------- |
| `deploymentTemplateId` | `string`            | Required. The template to delete. |
| `cancellationToken`    | `CancellationToken` | Optional. Cancels the call.       |

**Returns:** a `Result` that indicates success or failure.

You can't delete the connection's default template; make another template the default first. Deleting a template doesn't change deployments that were created from it.

```csharp
var delete = await broker.DeleteDeploymentTemplateAsync(templateId);
if (delete.IsFailure)
{
    Console.WriteLine($"Delete failed: {delete.Error.Code} {delete.Error.Message}");
}
```

**See also:** [Remove-PmpcDeploymentTemplate](../powershell/remove-pmpcdeploymenttemplate.md) and [Delete deployment template](../rest-api/applications.md#delete-deployment-template).

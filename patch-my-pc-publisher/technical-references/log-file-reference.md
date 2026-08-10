# Log File Reference for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Patch My PC (PMPC) Publisher creates various log files to record its activities, including synchronization, publishing, service, and cloud operations, etc.

These logs are used when troubleshooting Publisher behavior or when collecting information for support.

{% hint style="info" %}
**Note**

See [Customize Content Download and Log Save Location](../manage/advanced-tab/customize-content-download-log-save-location.md) for details on how to configure logging-related options in Publisher&#x20;
{% endhint %}

## PatchMyPC.log

The primary Publisher log is **PatchMyPC.log**.&#x20;

In older versions, this log is located in the root of the Publisher installation folder, i.e.

`%ProgramFiles%\Patch My PC\Patch My PC Publishing Service`

In newer versions, this log is located in the **Logs** subfolder.

## Log Naming Guidance

Publisher component logs are named to help identify the area of the product that generated the log.

_Controller_ logs generally record communication between the Publisher user interface and the related background service or component. These logs are useful when an action is initiated by Publisher, and you need to confirm how the request was routed to the service layer.

_Client_ logs generally record user interface-initiated requests and responses. These logs are useful when troubleshooting actions performed in the Publisher console.

Service, repository, and background service logs generally record the underlying processing performed by Publisher. These logs are useful when troubleshooting synchronization, publishing, package processing, catalog activity, licensing, cloud communication, or integration behavior.

## Merging Logs for Troubleshooting

Merging multiple Publisher logs with [CMTrace](https://learn.microsoft.com/en-us/intune/configmgr/core/support/cmtrace) can make troubleshooting easier because related activity may be written across multiple component logs. For example, a single action started in the Publisher console may appear in a client log, a controller log, and one or more service or repository logs.

When reviewing an issue, merge the relevant logs and sort entries by timestamp. This provides a combined timeline of the activity and can help identify where a request started, which component processed it, and where an error occurred.

## Scenario-Based Log Review

When troubleshooting a specific area, review logs that match the related scenario name. For example, when troubleshooting Intune activity, review logs that include `Intune` in the filename.&#x20;

When troubleshooting WSUS activity, review logs that include `Wsus` or `WSUS` in the filename.&#x20;

When troubleshooting ConfigMgr activity, review logs that include `ConfigMgr` in the filename.

### Intune logs

* **PatchMyPC-Intune.log**
* **PatchMyPC-IntuneCacheService.log**
* **PatchMyPC-IntuneClient.log**
* **PatchMyPC-IntuneReportBackgroundService.log**
* **PatchMyPC-IntuneReportRepository.log**
* **PatchMyPC-IntuneRepository.log**

### WSUS logs

* **PatchMyPC-WsusClient.log**
* **PatchMyPC-WsusController.log**
* **PatchMyPC-WsusOptionsViewModel.log**
* **PatchMyPC-SdkWsusRepository\*.log**

### ConfigMgr logs

* **PatchMyPC-ConfigMgrClient.log**
* **PatchMyPC-ConfigMgrController.log**
* **PatchMyPC-ConfigMgrSqlDbRepository.log**
* **PatchMyPC-SmsProviderConfigMgrRepository.log**

### Component Logs

* **PatchMyPC-AppMigrationService\*.log**
* **PatchMyPC-CertificateClient.log**
* **PatchMyPC-CertificateController.log**
* **PatchMyPC-CertificateValidationManager.log**
* **PatchMyPC-CloudConnectionApiClient.log**
* **PatchMyPC-CloudFileUploadBackgroundService.log**
* **PatchMyPC-CloudMigrationSignalRClient.log**
* **PatchMyPC-ConfigMgrClient.log**
* **PatchMyPC-ConfigMgrController.log**
* **PatchMyPC-ConfigMgrSqlDbRepository.log**
* **PatchMyPC-CustomCatalogService.log**
* **PatchMyPC-CustomerPortalApiClient\*.log**
* **PatchMyPC-FeatureManagerClient.log**
* **PatchMyPC-HeartbeatClient.log**
* **PatchMyPC-HeartbeatController.log**
* **PatchMyPC-HeartbeatService.log**
* **PatchMyPC-Intune.log**
* **PatchMyPC-IntuneCacheService.log**
* **PatchMyPC-IntuneClient.log**
* **PatchMyPC-IntuneReportBackgroundService.log**
* **PatchMyPC-IntuneReportRepository.log**
* **PatchMyPC-IntuneRepository.log**
* **PatchMyPC-JobManagerBackgroundService.log**
* **PatchMyPC-JobsClient.log**
* **PatchMyPC-JobsController.log**
* **PatchMyPC-LicenseClient.log**
* **PatchMyPC-LicenseController.log**
* **PatchMyPC-LicenseRepository\*.log**
* **PatchMyPC-PackageClient.log**
* **PatchMyPC-PackageController.log**
* **PatchMyPC-PackageService\*.log**
* **PatchMyPC-PmpcCatalogService.log**
* **PatchMyPC-PmpcPublisherTokenProvider\*.log**
* **PatchMyPC-ProductSelectionsClient.log**
* **PatchMyPC-SdkWsusRepository\*.log**
* **PatchMyPC-ServiceActionClient.log**
* **PatchMyPC-ServiceActionController.log**
* **PatchMyPC-SmsProviderConfigMgrRepository.log**
* **PatchMyPC-TenantMismatchCheckerViewModel.log**
* **PatchMyPC-WsusClient.log**
* **PatchMyPC-WsusController.log**
* **PatchMyPC-WsusOptionsViewModel.log**

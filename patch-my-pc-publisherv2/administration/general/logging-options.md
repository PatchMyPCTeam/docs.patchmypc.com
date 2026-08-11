# Logging Options

_Applies to: Patch My PC Publisher V2.x_

## Overview

Logging options control the level of detail written to Publisher log files and provide tools to assist with troubleshooting and support.

![Logging Options](../../../.gitbook/assets/image-\(3918\).png)

## Logging Level

The logging level determines how much information is written to the log files.

* **Information**\
  This is the default setting and is recommended for normal operation. It records high level operational events and status messages.
* **Debug**\
  This setting records detailed diagnostic information and is intended for troubleshooting. Debug logging can significantly increase log volume and should typically be enabled only when investigating an issue.

When troubleshooting, it is recommended to temporarily enable Debug logging and revert to Information once the issue has been resolved.

## Logs to Retain

Specifies the number of log files to keep before older logs are overwritten.

> \*\*Note\*\*
>
> It is recommended to set \*\*Logs to Retain\*\* to \*\*10\*\*. Publisher log files are relatively small, and retaining additional history is extremely valuable when troubleshooting issues or providing support, as it preserves publishing context that may otherwise be lost.

## Max Size in MB

Specifies the maximum size of each individual log file before a new log is created.

> \*\*Note\*\*
>
> It is recommended to set \*\*Max Size in MB\*\* to \*\*10\*\*. Publisher log files are relatively small, and retaining additional history is extremely valuable when troubleshooting issues or providing support, as it preserves publishing context that may otherwise be lost.

## Open PatchMyPC.log

Opens the primary Publisher log file. This log contains the main operational and publishing activity for the Publisher.

> \*\*Note\*\*
>
> It is recommended to view this log using CMTrace to improve readability and highlight warnings and errors.

## Open wsyncmgr.log

Opens the wsynccmgr.log file. This option is applicable when the Publisher is installed on a ConfigMgr site server and is useful for troubleshooting software update synchronization behavior.

## Collect Logs

Collects relevant Publisher log files and packages them into a compressed archive.

The generated log bundle is intended for troubleshooting and is particularly useful when working with support, as it includes the files needed to diagnose most Publisher related issues.

## Log Reference

The Publisher creates multiple log files to record synchronization, publishing, service, cloud, licensing, certificate, package, catalog, and repository activity.

These logs are used when troubleshooting Publisher behavior or when collecting information for support.

The primary Publisher log is `PatchMyPC.log`. In older installations, this log is located in the root of the Publisher installation directory, `%ProgramFiles%\Patch My PC\Patch My PC Publishing Service`. In new installations, this log is located in the `Logs` subfolder.

### Log Naming Guidance

Publisher component logs are named to help identify the area of the product that generated the log.

`Controller` logs generally record communication between the Publisher user interface and the related background service or component. These logs are useful when an action is started from the Publisher and you need to confirm how that request was passed to the service layer.

`Client` logs generally record user interface initiated requests and responses. These logs are useful when troubleshooting actions performed in the Publisher console.

Service, repository, and background service logs generally record the underlying processing performed by the Publisher. These logs are useful when troubleshooting synchronization, publishing, package processing, catalog activity, licensing, cloud communication, or integration behavior.

### Scenario Based Log Review

When troubleshooting a specific area, review logs that match the related scenario name. For example, when troubleshooting Intune activity, review logs that include `Intune` in the file name. When troubleshooting WSUS activity, review logs that include `Wsus` or `WSUS` in the file name. When troubleshooting ConfigMgr activity, review logs that include `ConfigMgr` in the file name.

#### Intune logs

* `PatchMyPC-Intune.log`
* `PatchMyPC-IntuneCacheService.log`
* `PatchMyPC-IntuneClient.log`
* `PatchMyPC-IntuneReportBackgroundService.log`
* `PatchMyPC-IntuneReportRepository.log`
* `PatchMyPC-IntuneRepository.log`

#### WSUS logs

* `PatchMyPC-WsusClient.log`
* `PatchMyPC-WsusController.log`
* `PatchMyPC-WsusOptionsViewModel.log`
* `PatchMyPC-SdkWsusRepository*.log`

#### ConfigMgr logs

* `PatchMyPC-ConfigMgrClient.log`
* `PatchMyPC-ConfigMgrController.log`
* `PatchMyPC-ConfigMgrSqlDbRepository.log`
* `PatchMyPC-SmsProviderConfigMgrRepository.log`

### Merging Logs for Troubleshooting

Merging multiple Publisher logs with [CMTrace](https://learn.microsoft.com/en-us/intune/configmgr/core/support/cmtrace) can make troubleshooting easier because related activity may be written across more than one component log. For example, a single action started in the Publisher console may appear in a client log, a controller log, and one or more service or repository logs.

When reviewing an issue, merge the relevant logs and sort entries by timestamp. This provides a combined timeline of the activity and can help identify where a request started, which component processed it, and where an error occurred.

### Component Logs

* `PatchMyPC-AppMigrationService*.log`
* `PatchMyPC-CertificateClient.log`
* `PatchMyPC-CertificateController.log`
* `PatchMyPC-CertificateValidationManager.log`
* `PatchMyPC-CloudConnectionApiClient.log`
* `PatchMyPC-CloudFileUploadBackgroundService.log`
* `PatchMyPC-CloudMigrationSignalRClient.log`
* `PatchMyPC-ConfigMgrClient.log`
* `PatchMyPC-ConfigMgrController.log`
* `PatchMyPC-ConfigMgrSqlDbRepository.log`
* `PatchMyPC-CustomCatalogService.log`
* `PatchMyPC-CustomerPortalApiClient*.log`
* `PatchMyPC-FeatureManagerClient.log`
* `PatchMyPC-HeartbeatClient.log`
* `PatchMyPC-HeartbeatController.log`
* `PatchMyPC-HeartbeatService.log`
* `PatchMyPC-Intune.log`
* `PatchMyPC-IntuneCacheService.log`
* `PatchMyPC-IntuneClient.log`
* `PatchMyPC-IntuneReportBackgroundService.log`
* `PatchMyPC-IntuneReportRepository.log`
* `PatchMyPC-IntuneRepository.log`
* `PatchMyPC-JobManagerBackgroundService.log`
* `PatchMyPC-JobsClient.log`
* `PatchMyPC-JobsController.log`
* `PatchMyPC-LicenseClient.log`
* `PatchMyPC-LicenseController.log`
* `PatchMyPC-LicenseRepository*.log`
* `PatchMyPC-PackageClient.log`
* `PatchMyPC-PackageController.log`
* `PatchMyPC-PackageService*.log`
* `PatchMyPC-PmpcCatalogService.log`
* `PatchMyPC-PmpcPublisherTokenProvider*.log`
* `PatchMyPC-ProductSelectionsClient.log`
* `PatchMyPC-SdkWsusRepository*.log`
* `PatchMyPC-ServiceActionClient.log`
* `PatchMyPC-ServiceActionController.log`
* `PatchMyPC-SmsProviderConfigMgrRepository.log`
* `PatchMyPC-TenantMismatchCheckerViewModel.log`
* `PatchMyPC-WsusClient.log`
* `PatchMyPC-WsusController.log`
* `PatchMyPC-WsusOptionsViewModel.log`

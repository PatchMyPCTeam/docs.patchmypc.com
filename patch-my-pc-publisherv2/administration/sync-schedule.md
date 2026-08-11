# Sync Schedule

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Sync Schedule** tab controls when the Publisher runs an automated publishing sync. A sync evaluates third party apps and updates and publishes content based on the configured selections in the product trees, customizations, and global options across the tabs.

![Publisher scheduling options](../../.gitbook/assets/image-\(252\).png)

## How a Publishing Sync Works

A publishing sync represents the evaluation of publishing intent at a specific point in time. During the first sync, the Publisher evaluates all configured selections across the Updates, ConfigMgr Apps, Intune Apps, and Intune Updates tabs, along with any customizations and global options configured throughout the console. These settings define what content the Publisher is expected to publish.

At the start of every publishing sync, the Publisher downloads and processes the latest version of the Patch My PC catalog. Each sync always evaluates the most current catalog data available.

After the catalog is loaded, the Publisher evaluates the selected products across all publishing tabs. For each selected app or update, the Publisher checks whether the version in the catalog has already been published. If the version has not been published, the Publisher publishes the new version using the configured options and customizations.

## Scheduling Options

The Publisher supports multiple scheduling options to control how often the publishing service runs.

* **Daily (Default)**\
  Use this option to run the publishing service once per day. You configure the time using hour and minute selectors and choose AM or PM. The sync will start within plus or minus five minutes of the configured time.
* **Weekly**\
  Use this option to run the publishing service once per week. You select the day of the week and the time. The sync runs on the chosen weekday at the specified time.
* **Monthly by Weekday**\
  Use this option to run the publishing service on a specific weekday pattern. You select the occurrence such as first, second, third, or last, then select the weekday and time. An optional offset in days can be applied to shift the sync earlier or later than the calculated date.
* **Monthly**\
  Use this option to run the publishing service once per month. You specify the day of the month and the time.
* **Hourly**\
  Use this option to run the publishing service at a recurring hourly interval. You specify the number of hours between each sync. The schedule begins as soon as the service starts and continues at the defined interval.
* **Disable Sync Schedule**\
  Use this option to prevent the publishing service from running automatically. When selected, all publishing actions require a manual sync. This is useful for testing or tightly controlled publishing environments.

> \*\*Important\*\*
>
> The Publisher uses a single, global sync schedule that applies across all tabs and products. You cannot configure different sync schedules per platform or product.

## Trigger ConfigMgr SUP Sync after publishing

When enabled, the Publisher triggers a ConfigMgr software update point sync after new third party updates are published. This ensures that newly published updates become available in ConfigMgr as quickly as possible, without waiting for the next scheduled software update point sync.

This option requires a valid SMS Provider connection. The **Configure SMS Provider connection** button is used to define the connection settings. See [Connection and Source Options](configmgr-apps/options/connection-and-source-options.md#configure-sms-provider-connection) for more information on configuring the SMS Provider in the Publisher.

## Run Publishing Service Sync

Clicking **Run Publishing Service Sync** starts an immediate publishing sync. This process performs the same evaluation as a scheduled sync. The Publisher downloads the latest version of the Patch My PC catalog and evaluates all configured product selections, customizations, and global options to determine which apps and updates should be published.

This action is referred to as a **manual sync** and is commonly used for testing, validation, or ad hoc publishing scenarios.

> \*\*Note\*\*
>
> A manual sync is frequently used in conjunction with the \[right-click customization option]\(../customizations-right-click-options/) \[\*\*Publish this product during the next manual sync (selective sync)\*\*]\(../customizations-right-click-options/publish-this-product-during-the-next-manual-sync-selective-sync.md). When this option is selected on one or more products in the product tree across any publishing tab, the next manual sync prompts whether to run a selective sync.
>
> When a selective sync is chosen, the Publisher evaluates and processes only the products that were explicitly selected using that right-click option. This allows administrators to quickly test individual apps or updates, including checking for newly released versions, without processing the entire catalog and all selected products.
>
> Selective sync provides a faster and more targeted publishing workflow compared to a full catalog evaluation.

## Sync Schedule Recommendations

The primary purpose of the sync schedule is to continuously evaluate the latest third party apps and updates as they are released by vendors. Third party vendors do not release updates on a single predictable schedule, and new versions can be released at any time, particularly for products such as browsers and collaboration tools. Because each sync evaluates the latest version available in the catalog, the configured schedule directly determines how quickly newly released content is detected and made available for deployment.

The default configuration is a daily sync, which is suitable for most environments. Running the sync infrequently, such as on a monthly schedule, is generally not recommended unless strict operational processes require that frequency. Infrequent synchronization can result in missed security updates and delayed visibility of newly released third party content. The sync schedule should be configured to run as often as practical based on operational constraints.

## How Deployment Timing Is Controlled

The sync schedule determines when apps and updates are published, not inherently when they are installed on devices. How quickly they are deployed to clients is dictated by the target management platform and the configuration applied either within the Publisher or natively in the platform.

### Intune Apps & Updates

For Intune apps and Intune updates, assignments _can_ be configured directly in the Publisher. These assignments define targeting, availability, deadline and other deployment behaviors, which ultimately control when apps and updates are delivered to devices after they have been published.

### WSUS/ConfigMgr Updates

For updates published in a standalone WSUS environment, deployment timing is controlled through update approvals. Administrators can manually approve updates or use WSUS auto approval rules to manage when updates become available to devices.

For updates synced to ConfigMgr from WSUS after they are published, deployment cadence can be controlled using Automatic Deployment Rules (ADRs). ADRs define availability and deadline behavior and allowing staged or delayed rollouts.

### ConfigMgr Apps

For ConfigMgr apps, the Publisher is responsible only for creating the applications. Deployment targeting and timing are fully controlled by administrators using standard ConfigMgr deployment practices.

> \*\*Note\*\*
>
> If the \[global option to update an application in place]\(configmgr-apps/options/application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default) is enabled, newly published app versions will inherit existing deployments. For required deployments, this inheritance may directly influence how quickly devices receive the updated application.

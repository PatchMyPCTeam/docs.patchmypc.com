# Overview of the Scheduling tab in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Sync Schedule** tab in Patch My PC (PMPC) Publisher controls when Publisher runs an automated _publishing sync_.&#x20;

<figure><img src="../../../.gitbook/assets/image (4860).png" alt="&#x27;Sync Schedule&#x27; tab" width="563"><figcaption></figcaption></figure>

A _publishing sync_ evaluates third party apps and updates, and publishes content based on the configured selections in the Product Trees, customizations, and global options across the tabs.

## How a Publishing Sync Works

A _publishing sync_ represents the evaluation of publishing intent at a specific point in time. During the first sync, Publisher evaluates all configured selections across the **WSUS Updates**, **ConfigMgr Apps**, **Intune Apps**, and **Intune Updates** tabs, along with any customizations and global options configured throughout the console. These settings define what content Publisher is expected to publish.

At the start of every publishing sync, Publisher downloads and processes the latest version of the Patch My PC catalog. Each sync always evaluates the most current catalog data available.

After the catalog is loaded, Publisher evaluates the selected products across all publishing tabs. For each selected app or update, Publisher checks whether the version in the catalog has already been published. If the version has not been published, Publisher publishes the new version using the configured options and customizations.

## Sync Schedule Recommendations

The primary purpose of the Sync Schedule is to continuously evaluate the latest third party apps and updates as they are released by vendors. Third-party vendors do not release updates on a single predictable schedule, and new versions can be released at any time, particularly for products such as browsers and collaboration tools.&#x20;

As each sync evaluates the latest version available in the catalog, the configured schedule directly determines how quickly newly released content is detected and made available for deployment.

The default configuration is a daily sync, which is suitable for most environments. Running the sync infrequently, such as on a monthly schedule, is generally not recommended unless strict operational processes require that frequency.&#x20;

Infrequent synchronization can result in missed security updates and delayed visibility of newly released third party content. The Sync Schedule should be configured to run as often as practical based on operational constraints.

## How Deployment Timing Is Controlled

The Sync Schedule determines when apps and updates are published, not inherently when they are installed on devices. How quickly they are deployed to clients is dictated by the target management platform and the configuration applied either within the Publisher or natively in the platform:

* [Intune Apps & Updates](overview.md#intune-apps-and-updates)
* [WSUS/ConfigMgr Updates](overview.md#wsus-configmgr-updates)
* [ConfigMgr Apps](overview.md#configmgr-apps)

### Intune Apps & Updates

For Intune apps and Intune updates, assignments can be configured directly in Publisher. These assignments define targeting, availability, deadline, and other deployment behaviors, which ultimately control when apps and updates are delivered to devices after they have been published.

### WSUS/ConfigMgr Updates

For updates published in a standalone WSUS environment, deployment timing is controlled through update approvals. Administrators can manually approve updates or use WSUS auto approval rules to manage when updates become available to devices.

For updates synced to ConfigMgr from WSUS after they are published, deployment cadence can be controlled using Automatic Deployment Rules (ADRs). ADRs define availability and deadline behavior and allow staged or delayed rollouts.

### ConfigMgr Apps

For ConfigMgr apps, Publisher is responsible only for creating the applications. Deployment targeting and timing are fully controlled by administrators using standard ConfigMgr deployment practices.

{% hint style="info" %}
**Note**

If the [global option to update an application in place](../configmgr-apps-tab/base-install-options/application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default) is enabled, newly published app versions will inherit existing deployments. For required deployments, this inheritance may directly influence how quickly devices receive the updated application.
{% endhint %}

# Scenario 3: WSUS (Standalone)

_Applies to: Patch My PC Publisher V2.x_

## Overview

Use this scenario when the Publisher is used exclusively to create and manage third party updates in Windows Server Update Services (WSUS). This configuration is for environments that do not publish applications through ConfigMgr and do not integrate with Intune.

After completing the configuration steps in this section, the Publisher will be ready to publish third-party updates to WSUS.

## Checklist

Before configuring the Publisher, ensure the following information is identified and validated:

**General Items**

* [x] You have started a trial and/or have a valid [license key](../../administration/general/license-information.md).
* [x] The Publisher [installation location](../../download-and-install.md#where-should-i-install-the-publisher) has been identified.
* [x] Publisher [core requirements](../../publisher-requirements/core-requirements.md) are met.

**Platform Checklist (WSUS)**

* [x] Publisher [platform requirements](../../publisher-requirements/wsus-requirements/) are met.

## Installation and Configuration Steps

The following steps are suitable for getting the Publisher up and running in most environments and are recommended to be completed before selecting products to enable for publishing and applying product customizations.

1. After the [core](../../publisher-requirements/core-requirements.md) and [WSUS](../../publisher-requirements/wsus-requirements/) platform requirements have been met, and the Publisher installation location is identified, [download and install](../../../installation-guides/configmgr/download-and-run-the-msi.md) the Publisher.
2. Open the Publisher console and go to the [General ](../../administration/general/)tab. Enter your [license key or start a trial](../../administration/general/license-information.md).
3. Click the Validate button to validate the licence.
4. On the General tab still, confirm that a valid [code signing certificate is selected](../../administration/general/certificate-management/) or create/select one.
5. On the General tab still, configure [log retention](../../administration/general/logging-options.md) to keep a minimum of 10 logs and set the maximum log size to 10 megabytes.
6. Go to the [Updates ](../../administration/updates/)tab, right-click the [All Products](../../administration/updates/product-tree.md#all-products-level) node in the [product tree](../../administration/updates/product-tree.md) and enable and configure, the _Manage Installation Logging_ [customization](../../customizations-right-click-options/) option. This ensures detailed installation logs are generated on client devices when third-party applications are installed. This helps with troubleshooting if issues occur during installation.
7. On the Updates tab still, click the [Options](../../administration/updates/options/) button. In the [Standalone WSUS Mode](../../administration/updates/options/standalone-wsus-mode.md) section, enable the **Make updates appear in the WSUS console** setting.&#x20;
8. Go to the [Sync Schedule](../../administration/sync-schedule.md) tab to confirm the schedule aligns with your operational requirements.
9. Go to the [Alerts ](../../administration/alerts/)tab to configure email or webhook notifications if publishing and operational notifications are required.
10. Go to the [Advanced](../../administration/advanced/) tab and review:
    1. Configure [proxy settings](../../administration/advanced/proxy-settings.md) if your environment requires outbound internet access through a proxy.
    2. Configure a [Local Content Repository](../../administration/advanced/local-content-repository.md) path for binary free applications.
11. Go to the [About](../../administration/about.md) tab and review the self-update settings for the Publisher. If your organization has strict change control, disable automatic self updates. In most environments this is not recommended, as new versions include bug fixes and new features.
12. Click **Apply** to save the settings.

After completing these steps, the Publisher is configured and ready to publish third-party updates to WSUS.

The next step is to [Customize and publish applications and updates](../../getting-started.md#customize-and-publish-applications-and-updates).

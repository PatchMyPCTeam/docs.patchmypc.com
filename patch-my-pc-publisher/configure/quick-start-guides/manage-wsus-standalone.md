# Quick Start Guide for Managing WSUS (Standalone) using Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This article has not been updated for Version 3.x. Once it has, this banner will be removed.</p>
</blockquote>

Use this checklist when the Patch My PC (PMPC) Publisher is used exclusively to create and manage third party updates in Microsoft Windows Server Update Services (WSUS).

This configuration is for environments that do not publish applications through ConfigMgr and do not integrate with Intune.

After completing the configuration steps in this section, the Publisher will be ready to publish third-party updates to WSUS.

## Prerequisites

<table><thead><tr><th width="83" valign="top">Item</th><th width="323" valign="top">Task</th><th valign="top">Done?</th></tr></thead><tbody><tr><td valign="top"></td><td valign="top"></td><td valign="top">![](/_images/image-(4460).png)</td></tr><tr><td valign="top"></td><td valign="top"></td><td valign="top"></td></tr><tr><td valign="top"></td><td valign="top"></td><td valign="top"></td></tr></tbody></table>





Before continuing to configure Publisher to manage WSUS (Standalone), ensure you have completed the following checklist:

<table><thead><tr><th width="83" valign="top">Item</th><th width="444" valign="top">Task</th><th width="99" align="center" valign="top">Done?</th></tr></thead><tbody><tr><td valign="top">1.</td><td valign="top">You have started a trial and/or have a valid <a href="../../../patch-my-pc-publisherv2/administration/general/license-information.md">license key</a>.</td><td align="center" valign="top">![](/_images/image-(4460).png)</td></tr><tr><td valign="top">2.</td><td valign="top">You have identified Publisher's <a href="../../../patch-my-pc-publisherv2/download-and-install.md#where-should-i-install-the-publisher">installation location</a>.</td><td align="center" valign="top">![](/_images/image-(4460).png)</td></tr><tr><td valign="top">3.</td><td valign="top">Publisher's <a href="../../../patch-my-pc-publisherv2/publisher-requirements/core-requirements.md">core requirements</a> are met.</td><td align="center" valign="top">![](/_images/image-(4460).png)</td></tr><tr><td valign="top">4.</td><td valign="top">Publisher's <a href="../../../patch-my-pc-publisherv2/publisher-requirements/wsus-requirements/">requirements for WSUS</a> are met.</td><td align="center" valign="top">![](/_images/image-(4460).png)</td></tr></tbody></table>







## Installation and Configuration Steps

The following steps are suitable for getting the Publisher up and running in most environments and are recommended to be completed before selecting products to enable for publishing and applying product customizations.

1. After the [core](../../../patch-my-pc-publisherv2/publisher-requirements/core-requirements.md) and [WSUS](../../../patch-my-pc-publisherv2/publisher-requirements/wsus-requirements/) platform requirements have been met, and the Publisher installation location is identified, [download and install](../../../installation-guides/configmgr/download-and-run-the-msi.md) the Publisher.
2. Open the Publisher console and go to the [General ](../../../patch-my-pc-publisherv2/administration/general/)tab. Enter your [license key or start a trial](../../../patch-my-pc-publisherv2/administration/general/license-information.md).
3. Click the Validate button to validate the licence.
4. On the General tab still, confirm that a valid [code signing certificate is selected](../../../patch-my-pc-publisherv2/administration/general/certificate-management/) or create/select one.
5. On the General tab still, configure [log retention](../../../patch-my-pc-publisherv2/administration/general/logging-options.md) to keep a minimum of 10 logs and set the maximum log size to 10 megabytes.
6. Go to the [Updates ](../../../patch-my-pc-publisherv2/administration/updates/)tab, right-click the [All Products](../../../patch-my-pc-publisherv2/administration/updates/product-tree.md#all-products-level) node in the [product tree](../../../patch-my-pc-publisherv2/administration/updates/product-tree.md) and enable and configure, the _Manage Installation Logging_ [customization](../../../patch-my-pc-publisherv2/customizations-right-click-options/) option. This ensures detailed installation logs are generated on client devices when third-party applications are installed. This helps with troubleshooting if issues occur during installation.
7. On the Updates tab still, click the [Options](../../../patch-my-pc-publisherv2/administration/updates/options/) button. In the [Standalone WSUS Mode](../../../patch-my-pc-publisherv2/administration/updates/options/standalone-wsus-mode.md) section, enable the **Make updates appear in the WSUS console** setting.
8. Go to the [Sync Schedule](../../../patch-my-pc-publisherv2/administration/sync-schedule.md) tab to confirm the schedule aligns with your operational requirements.
9. Go to the [Alerts ](../../../patch-my-pc-publisherv2/administration/alerts/)tab to configure email or webhook notifications if publishing and operational notifications are required.
10. Go to the [Advanced](../../../patch-my-pc-publisherv2/administration/advanced/) tab and review:
    1. Configure [proxy settings](../../../patch-my-pc-publisherv2/administration/advanced/proxy-settings.md) if your environment requires outbound internet access through a proxy.
    2. Configure a [Local Content Repository](../../../patch-my-pc-publisherv2/administration/advanced/local-content-repository.md) path for binary free applications.
11. Go to the [About](../../../patch-my-pc-publisherv2/administration/about.md) tab and review the self-update settings for the Publisher. If your organization has strict change control, disable automatic self updates. In most environments this is not recommended, as new versions include bug fixes and new features.
12. Click **Apply** to save the settings.

After completing these steps, the Publisher is configured and ready to publish third-party updates to WSUS.

The next step is to [Customize and publish applications and updates](../../../patch-my-pc-publisherv2/getting-started.md#customize-and-publish-applications-and-updates).
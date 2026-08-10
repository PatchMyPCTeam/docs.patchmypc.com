# Quick Start Guide for Managing Intune Apps and Updates using Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This article has not been updated for Version 3.x. Once it has, this banner will be removed.</p>
</blockquote>

Use this scenario when the Patch My PC (PMPC) Publisher is used to publish third party applications and updates to Microsoft Intune only. This configuration is intended for cloud managed environments that do not publish third-party applications through ConfigMgr or updates through Windows Server Update Services (WSUS).

In this scenario, the Publisher integrates with Intune, using the Microsoft Graph API, to create and manage third-party applications and assignments.

After completing the configuration steps in this section, the Publisher will be ready to publish third-party applications and updates to Intune.

## Prerequisites

Before continuing to configure Publisher to manage Intune Apps and Updates, ensure you have completed the following checklist:





##

**General Items**

* [x] You have started a trial and/or have a valid [license key](../../../patch-my-pc-publisherv2/administration/general/license-information.md).
* [x] The Publisher [installation location](../../../patch-my-pc-publisherv2/download-and-install.md#where-should-i-install-the-publisher) has been identified.
* [x] Publisher [core requirements](../../../patch-my-pc-publisherv2/publisher-requirements/core-requirements.md) are met.

**Platform Checklist (Intune)**

* [x] Publisher [platform requirements](../../../patch-my-pc-publisherv2/publisher-requirements/intune-requirements/) are met.

## Installation and Configuration Steps

The following steps are suitable for getting the Publisher up and running in most environments and are recommended to be completed before selecting products to enable for publishing and applying product customizations.

1. After the [core ](../../../patch-my-pc-publisherv2/publisher-requirements/core-requirements.md)and [Intune](../../../patch-my-pc-publisherv2/publisher-requirements/intune-requirements/) platform requirements have been met, and the Publisher installation location is identified, [download and install](../../../installation-guides/configmgr/download-and-run-the-msi.md) the Publisher. In the installation wizard, check the box to enable [Intune standalone mode](../../../patch-my-pc-publisherv2/administration/advanced/intune-standalone-options.md).
2. Open the Publisher console and go to the [General ](../../../patch-my-pc-publisherv2/administration/general/)tab. Enter your [license key or start a trial](../../../patch-my-pc-publisherv2/administration/general/license-information.md).
3. Click the Validate button to validate the licence.
4. On the General tab still, configure [log retention](../../../patch-my-pc-publisherv2/administration/general/logging-options.md) to keep a minimum of 10 logs and set the maximum log size to 10 megabytes.
5. If [Intune standalone mode](../../../patch-my-pc-publisherv2/administration/advanced/intune-standalone-options.md) was not enabled in the Publisher installation wizard, go to the [Advanced](../../../patch-my-pc-publisherv2/administration/advanced/) tab. Because this is a Intune only scenario, find the **Intune Standalone Options** settings and hide disable the ConfigMgr Apps and Updates tabs to simplify the console experience.
6. Go to the [Intune Apps tab](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/), check **Enable creation of Win32 applications in Microsoft Intune** and the [Options](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/) form will open.
7. Enter a Tenant Friendly name.
8. From the information gathered when creating the [Entra ID App Registration](../../../patch-my-pc-publisherv2/publisher-requirements/intune-requirements/entra-id-app-registration/), complete the Authority URL, enter the Application (Client) ID and select the credential (Enter an App Secret or select a Client Authentication certificate). For more information, see [Authentication Settings](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/authentication-settings.md).
9. On the same Options page, review the [Application Options](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/application-options.md) section:
   1. Consider enabling the [Update application dependencies...](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/application-options.md#update-application-dependencies-from-previously-created-applications-when-an-updated-application-is) and [Copy the requirements... ](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/application-options.md#copy-the-requirements-from-previously-created-applications-or-updates-when-an-updated-application-is)options
   2. Configure [application retention](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/application-options.md#retention-best-practice) to keep at least 1 previous version to support rollback scenarios using supersedence.
   3. Consider enabling [Allow available uninstall](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/application-options.md#allow-available-uninstall).
10. Click [Test Connection](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/authentication-settings.md#test-connection) to verify the app registration is configured correctly.
11. On the Intune Apps tab still, right-click the [All Products](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md#all-products-level) node in the [product tree](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md) and enable and configure, the _Manage Installation Logging_ [customization](../../../patch-my-pc-publisherv2/customizations-right-click-options/) option. This ensures detailed installation logs are generated on client devices when third-party applications are installed. This helps with troubleshooting if issues occur during installation.
12. Go to the Intune Updates tab and check **Enable creation of Win32 updates in Microsoft Intune**.&#x20;
13. Click OK to close the options form that opens.
14. On the Intune Updates tab still, right-click the [All Products](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md#all-products-level) node in the [product tree](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md) and enable and configure, the Manage Installation Logging [customization](../../../patch-my-pc-publisherv2/customizations-right-click-options/) option. This ensures detailed installation logs are generated on client devices when third-party applications are installed. This helps with troubleshooting if issues occur during installation.
15. Go to the [Sync Schedule](../../../patch-my-pc-publisherv2/administration/sync-schedule.md) tab to confirm the schedule aligns with your operational requirements.
16. Go to the [Alerts ](../../../patch-my-pc-publisherv2/administration/alerts/)tab to configure email or webhook notifications if publishing and operational notifications are required.
17. Go to the [Advanced](../../../patch-my-pc-publisherv2/administration/advanced/) tab and review:
    1. Configure [proxy settings](../../../patch-my-pc-publisherv2/administration/advanced/proxy-settings.md) if your environment requires outbound internet access through a proxy.
    2. Configure a [Local Content Repository](../../../patch-my-pc-publisherv2/administration/advanced/local-content-repository.md) path for binary free applications.
    3. Consider enabling the option to [Store encryption information locally to allow extraction of Win32 .intunewin files](../../../patch-my-pc-publisherv2/administration/advanced/intune-global-options.md#store-encryption-information-locally-to-allow-extraction-of-win32-.intunewin-files) later.
18. Go to the [About](../../../patch-my-pc-publisherv2/administration/about.md) tab and review the self-update settings for the Publisher. If your organization has strict change control, disable automatic self updates. In most environments this is not recommended, as new versions include bug fixes and new features.
19. Click **Apply** to save the settings.

After completing these steps, the Publisher is configured and ready to publish third-party applications and Updates to Intune.

The next step is to [Customize and publish applications and updates](../../../patch-my-pc-publisherv2/getting-started.md#customize-and-publish-applications-and-updates).
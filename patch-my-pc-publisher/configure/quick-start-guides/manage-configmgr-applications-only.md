# Quick Start Guide for Managing ConfigMgr Applications only using Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Use this quick start when you want to create and manage third-party applications in Microsoft Configuration Manager.

{% hint style="info" %}
**Note**

This guide is for environments that do not intend to publish third-party updates through Windows Server Update Services (WSUS) or Intune.
{% endhint %}

After completing the configuration steps in this section, Publisher will be ready to publish third-party applications to ConfigMgr.

## Prerequisites

Before continuing to install and configure Publisher to manage ConfigMgr Applications only, ensure you have completed the following checklist.

<table><thead><tr><th width="55.77777099609375" align="right" valign="top">Item</th><th width="474.4444580078125" valign="top">Task</th><th align="center" valign="top">Done?</th></tr></thead><tbody><tr><td align="right" valign="top">1.</td><td valign="top">You have started a trial and/or have a valid <a href="../../../patch-my-pc-publisherv2/administration/general/license-information.md">license key</a>.</td><td align="center" valign="top"></td></tr><tr><td align="right" valign="top">2.</td><td valign="top">You have decided where to <a href="../../install/where.md">install</a> Publisher.</td><td align="center" valign="top"></td></tr><tr><td align="right" valign="top">3.</td><td valign="top">Publisher's <a href="../../requirements/core-requirements.md">core requirements</a> are met.</td><td align="center" valign="top"></td></tr><tr><td align="right" valign="top">4.</td><td valign="top">Publisher's <a href="../../requirements/configmgr-requirements/">ConfigMgr requirements</a> are met.</td><td align="center" valign="top"></td></tr><tr><td align="right" valign="top">5.</td><td valign="top">You know the <a href="../../manage/configmgr-apps-tab/scan-configmgr/sql-configuration.md#site-database-server">location and name of the ConfigMgr site database</a>.</td><td align="center" valign="top"></td></tr><tr><td align="right" valign="top">6.</td><td valign="top">You know the <a href="../../technical-references/configure-sms-provider.md#connection-settings">SMS Provider's</a> location.</td><td align="center" valign="top"></td></tr></tbody></table>

## Installing Publisher

The following steps are suitable for getting Publisher up and running in most environments and are recommended to be completed before selecting products to enable for publishing and applying product customizations.

<table><thead><tr><th width="55.77777099609375" align="right" valign="top">Item</th><th width="406.6666259765625" valign="top">Task</th><th align="center" valign="top">Done?</th></tr></thead><tbody><tr><td align="right" valign="top">1.</td><td valign="top"></td><td align="center" valign="top"></td></tr><tr><td align="right" valign="top"></td><td valign="top"></td><td align="center" valign="top"></td></tr></tbody></table>



???

<table><thead><tr><th width="55.77777099609375" align="right" valign="top">Item</th><th width="406.6666259765625" valign="top">Task</th><th align="center" valign="top">Done?</th></tr></thead><tbody><tr><td align="right" valign="top">1.</td><td valign="top"></td><td align="center" valign="top"></td></tr><tr><td align="right" valign="top"></td><td valign="top"></td><td align="center" valign="top"></td></tr></tbody></table>

??

## Installation and Configuration Steps

The following steps are suitable for getting the Publisher up and running in most environments and are recommended to be completed before selecting products to enable for publishing and applying product customizations.

1. After the [core ](../../../patch-my-pc-publisherv2/publisher-requirements/core-requirements.md)and [ConfigMgr](../../../installation-guides/configmgr/requirements.md) platform requirements have been met, and the Publisher installation location is identified, [download and install](../../../installation-guides/configmgr/download-and-run-the-msi.md) the Publisher.
2. Open the Publisher console and go to the [General ](../../../patch-my-pc-publisherv2/administration/general/)tab. Enter your [license key or start a trial](../../../patch-my-pc-publisherv2/administration/general/license-information.md).
3. Click the Validate button to validate the licence.
4. On the General tab still, confirm that a valid [code signing certificate is selected](../../../patch-my-pc-publisherv2/administration/general/certificate-management/) or create/select one.
5. On the General tab still, configure [log retention](../../../patch-my-pc-publisherv2/administration/general/logging-options.md) to keep a minimum of 10 logs and set the maximum log size to 10 megabytes.
6. Go to the [Advanced](../../../patch-my-pc-publisherv2/administration/advanced/) tab. Because this is a ConfigMgr applications only scenario and no WSUS or Software Update Point is used, hide the Updates tab to simplify the console experience.
7. Go to the [ConfigMgr Apps](../../../patch-my-pc-publisherv2/administration/configmgr-apps/) tab and configure the [Scan ConfigMgr Database for Supported Products](../../../patch-my-pc-publisherv2/administration/configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md) form control.
8. On the ConfigMgr Apps tab still, right-click the [All Products](../../../patch-my-pc-publisherv2/administration/configmgr-apps/product-tree.md#all-products-level) node in the [product tree](../../../patch-my-pc-publisherv2/administration/configmgr-apps/product-tree.md) and enable and configure, the _Manage Installation Logging_ [customization](../../../patch-my-pc-publisherv2/customizations-right-click-options/) option. This ensures detailed installation logs are generated on client devices when third-party applications are installed. This helps with troubleshooting if issues occur during installation.
9. On the ConfigMgr Apps tab still, click the [Options ](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/)button. Configure the [SMS Provider connection](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/connection-and-source-options.md#configure-sms-provider-connection) by specifying the SMS Provider server and validating connectivity.
10. On the same Options page, configure the [source folder](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/connection-and-source-options.md#source-folder) used for application content. Ensure the folder is accessible to the ConfigMgr site server and distribution points.
11. On the same Options page, review the [Application Creation Options](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/application-creation-options.md) section:
    1. Disable the option to[ allow applications to be installed from the Install Application task sequence action](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/application-creation-options.md#allow-applications-to-be-installed-from-the-install-application-task-sequence-action) unless it is required for your environment.
    2. Configure a [default folder in the Applications node](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/application-creation-options.md#move-applications-to-a-specific-console-folder) so applications published by the Publisher are centralized and easy to manage.
    3. Leave the default options enabled to [update existing application metadata, deployment types, detection methods, and content when new application versions are published](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default).
    4. Configure [application retention](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/application-creation-options.md#retain-up-to-x-previously-created-applications) to keep at least 1 previous version to support rollback scenarios using supersedence.
12. Review [Content Distribution Options](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/content-distribution-options.md) and confirm applications are automatically distributed to the appropriate distribution points if required.
13. Go to the [Sync Schedule](../../../patch-my-pc-publisherv2/administration/sync-schedule.md) tab to confirm the schedule aligns with your operational requirements.
14. Go to the [Alerts ](../../../patch-my-pc-publisherv2/administration/alerts/)tab to configure email or webhook notifications if publishing and operational notifications are required.
15. Go to the [Advanced](../../../patch-my-pc-publisherv2/administration/advanced/) tab and review:
    1. Configure [proxy settings](../../../patch-my-pc-publisherv2/administration/advanced/proxy-settings.md) if your environment requires outbound internet access through a proxy.
    2. Configure a [Local Content Repository](../../../patch-my-pc-publisherv2/administration/advanced/local-content-repository.md) path for binary free applications.
16. Go to the [About](../../../patch-my-pc-publisherv2/administration/about.md) tab and review the self-update settings for the Publisher. If your organization has strict change control, disable automatic self updates. In most environments this is not recommended, as new versions include bug fixes and new features.
17. Click **Apply** to save the settings.

After completing these steps, the Publisher is configured and ready to publish third-party applications to ConfigMgr.

The next step is to [Customize and publish applications and updates](../../../patch-my-pc-publisherv2/getting-started.md#customize-and-publish-applications-and-updates).

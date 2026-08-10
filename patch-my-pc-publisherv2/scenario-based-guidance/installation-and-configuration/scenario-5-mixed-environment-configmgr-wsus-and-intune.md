# Scenario 5: Mixed Environment (ConfigMgr, WSUS and Intune)

_Applies to: Patch My PC Publisher V2.x_

## Overview

Use this scenario when the Publisher is used to publish third party applications and updates in a mixed environment that includes ConfigMgr, Windows Server Update Services (WSUS), and Intune. This configuration is typically intended for organizations transitioning between management platforms or managing multiple platforms simultaneously.

In this scenario, a Software Update Point (SUP) site system role that leverages WSUS is used as the update publishing endpoint for the Publisher. The Publisher publishes third-party update metadata and binaries directly to the WSUS instance associated with the top-level SUP in the ConfigMgr environment.

ConfigMgr uses the SUP to synchronize third-party update metadata from WSUS. After synchronization, ConfigMgr orchestrates update approval, deployment and reporting.

The same Publisher instance can also be used to publish third-party applications and updates to Intune.

After completing the configuration steps in this section, the Publisher will be ready to publish third-party applications to both ConfigMgr and Intune and third-party updates to both WSUS and Intune.

## Checklist

Before configuring the Publisher, ensure the following information is identified and validated:

**General Items**

* [x] You have started a trial and/or have a valid [license key](../../administration/general/license-information.md).
* [x] The Publisher [installation location](../../download-and-install.md#where-should-i-install-the-publisher) has been identified.
* [x] Publisher [core requirements](../../publisher-requirements/core-requirements.md) are met.

**Platform Checklist (WSUS)**

* [x] Publisher [platform requirements](../../publisher-requirements/wsus-requirements/) are met.

**Platform Checklist (ConfigMgr)**

* [x] Publisher [platform requirements](../../../installation-guides/configmgr/requirements.md) are met.
* [x] The [SUP site system role](../../publisher-requirements/configmgr-requirements/site-system-role/) has been considered and is configured.
* [x] The [location and the name of the ConfigMgr site database](../../administration/configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md#site-database-server) has been identified.
* [x] The [SMS Provider location](../../publisher-reference/configure-the-sms-provider-connection.md#connection-settings) has been identified.

**Platform Checklist (Intune)**

* [x] Publisher [platform requirements](../../publisher-requirements/intune-requirements/) are met.

## Installation and Configuration Steps

The following steps are suitable for getting the Publisher up and running in most environments and are recommended to be completed before selecting products to enable for publishing and applying product customizations.

1. After the [core](../../publisher-requirements/core-requirements.md), [WSUS](../../publisher-requirements/wsus-requirements/), [ConfigMgr](../../../installation-guides/configmgr/requirements.md) and [Intune](../../publisher-requirements/intune-requirements/) platform requirements have been met, and the Publisher installation location is identified, [download and install](../../../installation-guides/configmgr/download-and-run-the-msi.md) the Publisher.
2. Open the Publisher console and go to the [General ](../../administration/general/)tab. Enter your [license key or start a trial](../../administration/general/license-information.md).
3. Click the Validate button to validate the licence.
4. On the General tab still, confirm that a valid [code signing certificate is selected](../../administration/general/certificate-management/) or create/select one.
5. On the General tab still, configure [log retention](../../administration/general/logging-options.md) to keep a minimum of 10 logs and set the maximum log size to 10 megabytes.
6. Go to the [Updates ](../../administration/updates/)tab, right-click the [All Products](../../administration/updates/product-tree.md#all-products-level) node in the [product tree](../../administration/updates/product-tree.md) and enable and configure, the _Manage Installation Logging_ [customization](../../customizations-right-click-options/) option. This ensures detailed installation logs are generated on client devices when third-party applications are installed. This helps with troubleshooting if issues occur during installation.
7. Go to the [ConfigMgr Apps](../../administration/configmgr-apps/) tab and configure the [Scan ConfigMgr Database for Supported Products](../../administration/configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md) form control.
8. On the ConfigMgr Apps tab still, right-click the [All Products](../../administration/configmgr-apps/product-tree.md#all-products-level) node in the [product tree](../../administration/configmgr-apps/product-tree.md) and enable and configure, the _Manage Installation Logging_ [customization](../../customizations-right-click-options/) option.
9. On the ConfigMgr Apps tab still, click the [Options ](../../administration/configmgr-apps/options/)button. Configure the [SMS Provider connection](../../administration/configmgr-apps/options/connection-and-source-options.md#configure-sms-provider-connection) by specifying the SMS Provider server and validating connectivity.
10. On the same Options page, configure the [source folder](../../administration/configmgr-apps/options/connection-and-source-options.md#source-folder) used for application content. Ensure the folder is accessible to the ConfigMgr site server and distribution points.
11. On the same Options page, review the [Application Creation Options](../../administration/configmgr-apps/options/application-creation-options.md) section:
    1. Disable the option to[ allow applications to be installed from the Install Application task sequence action](../../administration/configmgr-apps/options/application-creation-options.md#allow-applications-to-be-installed-from-the-install-application-task-sequence-action) unless it is required for your environment.
    2. Configure a [default folder in the Applications node](../../administration/configmgr-apps/options/application-creation-options.md#move-applications-to-a-specific-console-folder) so applications published by the Publisher are centralized and easy to manage.
    3. Leave the default options enabled to [update existing application metadata, deployment types, detection methods, and content when new application versions are published](../../administration/configmgr-apps/options/application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default).
    4. Configure [application retention](../../administration/configmgr-apps/options/application-creation-options.md#retain-up-to-x-previously-created-applications) to keep at least 1 previous version to support rollback scenarios using supersedence.
12. Review [Content Distribution Options](../../administration/configmgr-apps/options/content-distribution-options.md) and confirm applications are automatically distributed to the appropriate distribution points if required.
13. Go to the [Intune Apps tab](../../administration/intune-apps-updates/), check **Enable creation of Win32 applications in Microsoft Intune** and the [Options](../../administration/intune-apps-updates/options/) form will open.
14. Enter a Tenant Friendly name.
15. From the information gathered when creating the [Entra ID App Registration](../../publisher-requirements/intune-requirements/entra-id-app-registration/), complete the Authority URL, enter the Application (Client) ID and select the credential (Enter an App Secret or select a Client Authentication certificate). For more information, see [Authentication Settings](../../administration/intune-apps-updates/options/authentication-settings.md).
16. On the same Options page, review the [Application Options](../../administration/intune-apps-updates/options/application-options.md) section:
    1. Consider enabling the [Update application dependencies...](../../administration/intune-apps-updates/options/application-options.md#update-application-dependencies-from-previously-created-applications-when-an-updated-application-is) and [Copy the requirements... ](../../administration/intune-apps-updates/options/application-options.md#copy-the-requirements-from-previously-created-applications-or-updates-when-an-updated-application-is)options
    2. Configure [application retention](../../administration/intune-apps-updates/options/application-options.md#retention-best-practice) to keep at least 1 previous version to support rollback scenarios using supersedence.
    3. Consider enabling [Allow available uninstall](../../administration/intune-apps-updates/options/application-options.md#allow-available-uninstall).
17. Click [Test Connection](../../administration/intune-apps-updates/options/authentication-settings.md#test-connection) to verify the app registration is configured correctly.
18. On the Intune Apps tab still, right-click the [All Products](../../administration/intune-apps-updates/product-tree.md#all-products-level) node in the [product tree](../../administration/intune-apps-updates/product-tree.md) and enable and configure, the _Manage Installation Logging_ [customization](../../customizations-right-click-options/) option. This ensures detailed installation logs are generated on client devices when third-party applications are installed. This helps with troubleshooting if issues occur during installation.
19. Go to the Intune Updates tab and check **Enable creation of Win32 updates in Microsoft Intune**.&#x20;
20. Click OK to close the options form that opens.
21. On the Intune Updates tab still, right-click the [All Products](../../administration/intune-apps-updates/product-tree.md#all-products-level) node in the [product tree](../../administration/intune-apps-updates/product-tree.md) and enable and configure, the Manage Installation Logging [customization](../../customizations-right-click-options/) option. This ensures detailed installation logs are generated on client devices when third-party applications are installed. This helps with troubleshooting if issues occur during installation.
22. Go to the [Sync Schedule](../../administration/sync-schedule.md) tab to confirm the schedule aligns with your operational requirements.
23. Go to the [Alerts ](../../administration/alerts/)tab to configure email or webhook notifications if publishing and operational notifications are required.
24. Go to the [Advanced](../../administration/advanced/) tab and review:
    1. Configure [proxy settings](../../administration/advanced/proxy-settings.md) if your environment requires outbound internet access through a proxy.
    2. Configure a [Local Content Repository](../../administration/advanced/local-content-repository.md) path for binary free applications.
    3. Consider enabling the option to [Store encryption information locally to allow extraction of Win32 .intunewin files](../../administration/advanced/intune-global-options.md#store-encryption-information-locally-to-allow-extraction-of-win32-.intunewin-files) later.
25. Go to the [About](../../administration/about.md) tab and review the self-update settings for the Publisher. If your organization has strict change control, disable automatic self updates. In most environments this is not recommended, as new versions include bug fixes and new features.
26. Click **Apply** to save the settings.

After completing these steps, the Publisher is configured and ready to publish third-party applications to both ConfigMgr and Intune and third-party updates to both WSUS and Intune.

The next step is to [Customize and publish applications and updates](../../getting-started.md#customize-and-publish-applications-and-updates).
---
hidden: true
---

# Integrations and Platform category of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Integrations and Platform** category on the **Advanced** tab of Patch My PC (PMPC) Publisher allows you to configure:

* [ScriptRunner Customization](integrations-platform.md#scriptrunner-customization)
* [Intune Global Options](integrations-platform.md#intune-global-options)
* [Timestamp Options](integrations-platform.md#timestamp-options)

<figure><img src="../../../.gitbook/assets/image (1397).png" alt="&#x27;Integrations and Platform&#x27; category" width="563"><figcaption></figcaption></figure>



## ScriptRunner Customization

The **SCRIPTRUNNER CUSTOMIZATIONS** section allows you to configure settings for ScriptRunner that influence how it handles long-running installer executions during client-side installation, as well as how client-side installation logs are cleaned up.

<figure><img src="../../../.gitbook/assets/image (1411).png" alt="&#x27;SCRIPTRUNNER CUSTOMIZATIONS&#x27; section" width="502"><figcaption></figcaption></figure>



## Intune Global Options

The **ADVANCED REPORTING AND ANALYTICS** section allows you to configure Advanced Insights.

## Timestamp Options

The **ADVANCED REPORTING AND ANALYTICS** section allows you to configure Advanced Insights.



\*\*\*\*

* [Advanced Reporting and Analytics](integrations-platform.md#advanced-reporting-and-analytics)
* [Backup and Restore Settings](integrations-platform.md#backup-and-restore-settings)
* [Product Export](integrations-platform.md#product-export)

<figure><img src="../../../.gitbook/assets/image (1381).png" alt="&#x27;Reporting &#x26; Backup&#x27; category" width="563"><figcaption></figcaption></figure>

## Advanced Reporting and Analytics

The **ADVANCED REPORTING AND ANALYTICS** section allows you to configure Advanced Insights.

### **Advanced Insights**

The **Advanced Insights** section allows you to download PMPC Advanced Insights, which extends Microsoft Configuration Manager (ConfigMgr) reporting with enhanced analytics, visualizations, and compliance insights.

<figure><img src="../../../.gitbook/assets/image (1383).png" alt="&#x27;ADVANCED REPORTING AND ANALYTICS&#x27; section" width="496"><figcaption></figcaption></figure>

Click **Download Advanced Insights** to access the latest version at:

[https://patchmypc.com/advanced-insights-download](https://patchmypc.com/advanced-insights-download)

{% hint style="info" %}
**Note**

The Advanced Reporting and Analytics option provides access to Patch My PC Advanced Insights, with available functionality determined by your subscription level.

* **Enterprise Plus customers**\
  Installing Advanced Insights enables Patch Insights functionality, providing visibility and reporting for Software Updates within ConfigMgr.
* **Enterprise Premium customers**\
  Enterprise Premium includes the full Advanced Insights analytics experience, unlocking advanced dashboards, expanded reporting, and deeper compliance and operational analytics.

Feature availability is controlled by your Patch My PC subscription (SKU), and functionality is automatically enabled based on your licensed tier. For more information, see [https://patchmypc.com/product/advanced-insights/](https://patchmypc.com/product/advanced-insights/)
{% endhint %}

## Backup and Restore Settings

The **BACKUP AND RESTORE SETTINGS** section allows you to export, import, and automatically back up Publisher configuration settings. This is useful for disaster recovery, migrating Publisher to a new server, or maintaining historical configuration snapshots.

This section allows you to configure the following settings:

* [Import/export settings](integrations-platform.md#import-export-settings)
* [Automatic backup](integrations-platform.md#product-export)

<figure><img src="../../../.gitbook/assets/image (1385).png" alt="&#x27;BACKUP AND RESTORE SETTINGS&#x27; section" width="494"><figcaption></figcaption></figure>

### Import/export settings

This section allows you to save Publisher's current configuration to a file or restore the configuration from a previous version.&#x20;

#### Import Settings button

Clicking **Import Settings** allows you to restore Publisher settings from a previously exported backup file. When you click **Import Settings**, a confirmation dialog appears asking you to confirm you wish to proceed.

<figure><img src="../../../.gitbook/assets/image (1386).png" alt="&#x27;Import Settings&#x27; confirmation dialog" width="310"><figcaption></figcaption></figure>

If you proceed, the current Publisher configuration will be replaced with the settings contained in the selected backup file. After importing settings, it is recommended to review critical configuration areas such as credentials, paths, and authentication settings before running a publishing sync.

Common use cases include:

* Restoring settings after server recovery
* Migrating the Publisher to a new system
* Reverting to a known-good configuration

#### Export Settings button

Clicking **Export Settings** allows you to create a manual backup of the current Publisher configuration.

When you click **Export Settings**, you will be asked to provide a location and filename for the export.

The exported file contains Publisher configuration data such as enabled products, publishing options, schedules, alerts, and **Advanced** tab settings. This file can be stored securely and later imported if needed.

This option is commonly used before:

* Making significant configuration changes.
* Upgrading or reinstalling Publisher.
* Moving Publisher to a new server.

### Automatic backup

The **Automatic backup** option lets you specify a location for Publisher to use to automatically write an updated backup file to whenever settings are saved.

<figure><img src="../../../.gitbook/assets/image (1387).png" alt="&#x27;Automatic backup&#x27; option" width="248"><figcaption></figcaption></figure>

Only a single backup file exists in this location, and it is overwritten each time a configuration change is made, ensuring the folder always contains the most recent configuration.

This design makes the custom backup path especially useful for disaster recovery scenarios, such as rebuilding a Publisher server or restoring settings quickly after an unexpected failure, without needing to manually export configuration files.

{% hint style="danger" %}
**Important**

Even when a custom automatic backup location is configured, Publisher continues to maintain backups in its default internal backup location. This internal location retains multiple historical backup versions and supports rollback and recovery scenarios, while the custom location stores only the most recent backup file for quick access.
{% endhint %}

#### Backup Pruning and Retention

Publisher automatically manages the retention of configuration backups using a built-in pruning process. This behavior is not configurable and is designed to balance historical recovery options with controlled disk usage.

The following retention rules are applied automatically:

* For the current day, Publisher retains up to 50 backups. These capture frequent configuration changes made throughout the day and allow quick rollback to recent states.
* For the previous 31 days, Publisher retains up to 10 backups per day. This provides daily historical coverage while limiting the total number of stored files.
* For backups older than 31 days, Publisher retains one backup per week for up to one year. This enables long-term recovery while minimizing storage growth.

Publisher automatically removes older backups outside of these thresholds. No manual cleanup or configuration is required. This retention model ensures recent changes are well protected while still maintaining a useful historical record for recovery, auditing, or troubleshooting scenarios.

#### Settings and Files Not Included in Backups

Some Publisher settings are protected using encryption that is unique to the device where Publisher is installed. When settings are restored on a different machine, these values may appear to be restored in the UI, and the fields may still be populated with masked values such as **\*\*\*\*\*\*\***. However, the underlying values are not valid on the new device and cannot be reused.

In addition, certificates and file-based dependencies are not included in backups. Because of this, after restoring settings on a different server or device, you must manually re-enter the protected values, re-import or reconfigure required certificates, and ensure any referenced files and folders are present and accessible, even if the UI appears populated.

#### Settings That Must Be Reconfigured

The following settings must be manually reconfigured after restoring settings on a new server:

* Microsoft Entra ID app registration client secret.
* Proxy password.
* SMS Provider connection account credentials.
* SMTP email password.
* SQL connection account credentials.
* Webhook URLs configured for alerts.

#### Certificates Not Restored

Certificates are not included in backups and must be manually re-imported or reconfigured after a restore. This includes certificates used for:

* Code signing.
* Authentication to Cloud services.
* Intune publishing.
* OAuth-based email authentication.

#### Files and Paths Not Included in Backups

The following items are also not included in backups and will not be restored:

* Staged Content Repository files.
* Additional Content Repository files.
* Manage Conflicting Processes custom banner images.
* MST transform files.
* Custom pre-install and post-install scripts and associated files.

If you need these files, ensure they are either accessible from the new server using the same paths, or manually copied to the new server and placed in the original configured locations.

## Product Export

The **PRODUCT EXPORT** section lets you export a list of enabled products and their configuration from Publisher to a CSV file. The export includes product-level settings and right-click options, which makes it useful for documentation, audits, change reviews, and comparing configurations.

<figure><img src="../../../.gitbook/assets/image (1388).png" alt="&#x27;PRODUCT EXPORT&#x27; section" width="496"><figcaption></figcaption></figure>

Some exported properties may appear populated even if they are not actively in use. This occurs when a property has a default value defined by Publisher. For example, Intune apps and Intune updates may show a maximum run time value that is only applicable when the same product is published to ConfigMgr.

### To export a list of products

1. Load Publisher.
2. Navigate to **Advanced | Reporting & Backup**.
3. Scroll down to the **PRODUCT EXPORT** section.
4. Select the checkboxes for each product type you want to export, then click **Export**.

<figure><img src="../../../.gitbook/assets/image (1389).png" alt="Selecting products to export and clicking &#x27;Export&#x27;" width="498"><figcaption></figcaption></figure>

5. Choose a location to save the CSV file.

The available export options align with the main product categories in Publisher. These include **WSUS updates**, **ConfigMgr Apps**, **Intune Apps**, and **Intune Updates**. Only product types that are currently available and enabled in Publisher can be selected.

Below is an example of an exported CSV.

<figure><img src="../../../.gitbook/assets/image (3951).png" alt="Exported product CSV example" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

A product type checkbox is only selectable when two conditions are met. The product type must be enabled using the main checkbox at the top of its corresponding tab, and at least one product of that type must exist. If either condition is not met, the checkbox for that product will be disabled.
{% endhint %}

{% hint style="danger" %}
**Important**

The Product export CSV is intended for reference and reporting purposes. It is not designed to be imported back into Publisher.
{% endhint %}

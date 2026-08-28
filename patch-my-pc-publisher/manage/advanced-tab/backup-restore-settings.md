# Backup and Restore Settings section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Backup and Restore Settings** section on the **Advanced** tab of Patch My PC (PMPC) Publisher allows you to export, import, and automatically back up the Publisher configuration settings. This is useful for disaster recovery, migrating the Publisher to a new server, or maintaining historical configuration snapshots.

<figure><img src="../../../.gitbook/assets/image (3).png" alt="&#x27;Backup and Restore Settings&#x27; section" width="563"><figcaption></figcaption></figure>

## Import Settings from a File

Use **Import settings from a file** to restore Publisher settings from a previously exported backup file.

This action replaces the current Publisher configuration with the settings contained in the selected backup file. After importing settings, it is recommended to review critical configuration areas such as credentials, paths, and authentication settings before running a publishing sync.

Common use cases include:

* Restoring settings after server recovery
* Migrating the Publisher to a new system
* Reverting to a known-good configuration

## Export Settings to a File

Use **Export settings to a file** to create a manual backup of the current Publisher configuration.

The exported file contains Publisher configuration data such as enabled products, publishing options, schedules, alerts, and Advanced tab settings. This file can be stored securely and later imported if needed.

* This option is commonly used before:
* Making significant configuration changes
* Upgrading or reinstalling the Publisher
* Moving the Publisher to a new server

## Automatically backup the latest settings to

This option enables automatic backups of the Publisher configuration.

When configured, the Publisher automatically writes an updated backup file to the specified folder whenever settings are saved. Only a single backup file exists in this location and it is overwritten each time a configuration change is made, ensuring the folder always contains the most recent configuration.

This design makes the custom backup path especially useful for **disaster recovery scenarios**, such as rebuilding a Publisher server or restoring settings quickly after an unexpected failure, without needing to manually export configuration files.

{% hint style="danger" %}
**Important**

Even when a custom automatic backup location is configured, the Publisher continues to maintain backups in its default internal backup location. This internal location retains multiple historical backup versions and supports rollback and recovery scenarios, while the custom location stores only the most recent backup file for quick access.
{% endhint %}

## Backup Pruning and Retention

The Publisher automatically manages the retention of configuration backups using a built-in pruning process. This behavior is not configurable and is designed to balance historical recovery options with controlled disk usage.

The following retention rules are applied automatically:

* For the current day, the Publisher retains up to 50 backups. These capture frequent configuration changes made throughout the day and allow quick rollback to recent states.
* For the previous 31 days, the Publisher retains up to 10 backups per day. This provides daily historical coverage while limiting the total number of stored files.
* For backups older than 31 days, the Publisher retains one backup per week for up to one year. This enables long-term recovery while minimizing storage growth.

Older backups outside of these thresholds are automatically removed by the Publisher. No manual cleanup or configuration is required. This retention model ensures recent changes are well protected while still maintaining a useful historical record for recovery, auditing, or troubleshooting scenarios.

## Settings and Files Not Included in Backups

Some settings in the Publisher are protected using encryption that is unique to the device where the Publisher is installed. When settings are restored on a different machine, these values may appear to be restored in the UI and the fields may still be populated with masked values such as \*\*\*\*\*\*\*. However, the underlying values are not valid on the new device and cannot be reused.

In addition, certificates and file based dependencies are not included in backups. Because of this, after restoring settings on a different server or device, you must manually re enter the protected values, re import or re configure required certificates, and ensure any referenced files and folders are present and accessible, even if the UI appears populated.

### Settings That Must Be Reconfigured

The following settings must be manually reconfigured after restoring settings on a new server:

* Microsoft Entra ID app registration client secret
* Proxy password
* SMS Provider connection account credentials
* SMTP email password
* SQL connection account credentials
* Webhook URLs configured for alerts

### Certificates Not Restored

Certificates are not included in backups and must be manually re-imported or reconfigured after a restore. This includes certificates used for:

* Code signing
* Authentication to Cloud services
* Intune publishing
* OAuth based email authentication

### Files and Paths Not Included in Backups

The following items are also not included in backups and will not be restored:

* Local Content Repository files
* Manage Conflicting Processes custom banner image
* MST transform files
* Custom pre-install and post-install scripts and associated files

If these files are required, ensure they are either accessible from the new server using the same paths, or manually copied to the new server and placed in the original configured locations.

# Application Migration section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Application Migration** section on the **Cloud** tab of Patch My PC (PMPC) Publisher helps you migrate applications from Microsoft Configuration Manager to Intune using the _Migration_ feature of PMPC Cloud.

<figure><img src="../../../.gitbook/assets/image (4858).png" alt="&#x27;Application Migration&#x27; section" width="563"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

You will be unable to enable the **Application Migration** feature until you have connected Publisher to your PMPC Cloud company as detailed in [Connect Publisher to Patch My PC Cloud](connect-publisher-cloud.md)
{% endhint %}

When **Application Migration** is enabled, Publisher inventories ConfigMgr applications and makes them available for migration to Intune through PMPC Cloud.

Discovery runs automatically every 60 minutes. Migration status and the number of discovered applications are shown for visibility and validation.

{% hint style="info" %}
**Note**

See [Setting Up ConfigMgr to Intune App Migration](../../../patch-my-pc-cloud/migration/setting-migration.md) for more details on setting up the Application Migration feature
{% endhint %}

## App Migration Database

When an app migration inventory runs, Publisher saves the inventoried ConfigMgr results in the Publishing Service's installation folder under the **Database** subfolder.

<figure><img src="../../../.gitbook/assets/image (168).png" alt="Migration Database" width="563"><figcaption></figcaption></figure>

This folder contains two files:

* **AppMigration.db** stores the app migration inventory data and processing state.
* **existingApps.json** contains a JSON copy of the discovery data.

{% hint style="danger" %}
**Important**

For reliability, consider excluding the **AppMigration.db** file from antivirus or endpoint protection scanning. This prevents the **AppMigration.db** file from being locked during scheduled scans, which can cause inventory or migration operations to fail.
{% endhint %}

# Application Migration section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Application Migration** section of the Patch My PC (PMPC) Publisher **Cloud** tab is used to help you migrate applications from Microsoft Configuration Manager to Intune using the _Migration_ feature of PMPC Cloud.

!['Application Migration' section](/_images/image-(4858).png "&#x27;Application Migration&#x27; section")

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>You will be unable to enable the **Application Migration** feature until you have connected Publisher to your PMPC Cloud company as detailed in [Connect Publisher to Patch My PC Cloud](connect-publisher-cloud.md)</p>
</blockquote>

When **Application Migration** is enabled, Publisher inventories ConfigMgr applications and makes them available for migration to Intune through PMPC Cloud.

Discovery runs automatically every 60 minutes. Migration status and the number of discovered applications are shown for visibility and validation.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Setting Up ConfigMgr to Intune App Migration](../../../patch-my-pc-cloud/migration/setting-migration.md) for more details on setting up the Application Migration feature</p>
</blockquote>

## App Migration Database

When an app migration inventory runs, Publisher saves the inventoried ConfigMgr results in the Publishing Service's installation folder under the **Database** subfolder.

![Migration Database](/_images/image-(168).png "Migration Database")

This folder contains two files:

* **AppMigration.db** stores the app migration inventory data and processing state.
* **existingApps.json** contains a JSON copy of the discovery data.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>For reliability, consider excluding the **AppMigration.db** file from antivirus or endpoint protection scanning. This prevents the **AppMigration.db** file from being locked during scheduled scans, which can cause inventory or migration operations to fail.</p>
</blockquote>
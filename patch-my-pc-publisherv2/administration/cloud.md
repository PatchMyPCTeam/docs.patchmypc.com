# Cloud

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Cloud** tab connects the Publisher to Patch My PC Cloud. This connection enables Cloud based features such as Custom Apps and application migration from Configuration Manager to Intune.

![Cloud Settings](/_images/image-(174).png "Cloud Settings")

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>An account on <a href="https://portal.patchmypc.com/">https://portal.patchmypc.com</a> is required to use Cloud features.</p>
</blockquote>

## Cloud Connection

The Cloud connection links the on premises Publisher to Patch My PC Cloud. Once connected, the Publisher is registered in Patch My PC Cloud under **Settings > Connections** with the connection type shown as Publisher.

### Connection Name

The Connection Name configured in the Publisher is displayed in Patch My PC Cloud and is used to identify the associated Publisher instance. Using a descriptive name is recommended.

![Connection Name](/_images/image-(169).png "Connection Name")

### Connect

The **Connect** button establishes a link between the Publisher and a Patch My PC Cloud Company. When selected, you are prompted to authenticate and approve the connection.

After a successful connection, the status changes to Connected and the Publisher appears in Patch My PC Cloud under Settings > Connections with the type shown as Publisher.

See [**Add a Connection**](../../patch-my-pc-cloud/manage/settings/connections/add-connection.md) for detailed steps on connecting the Publisher to Patch My PC Cloud.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>When selecting **Connect**, sign in using the same account that was used to create the Patch My PC Cloud company, or an account that has **Full Admin** privileges in Patch My PC Cloud. See [User Roles](../../patch-my-pc-cloud/manage/settings/users/user-roles-reference.md) for more information.</p>
</blockquote>

#### Multiple Cloud Companies

If the account used to sign in is associated with multiple Patch My PC Cloud companies, a selection window will appear.

![Select a Cloud Company](/_images/image-(4140).png "Select a Cloud Company")

Select the appropriate company from the list and click OK to complete the connection process.

### Disconnect

Disconnect removes the active connection between the Publisher and Patch My PC Cloud.\
After disconnecting, Cloud based features such as Custom Apps and application migration are no longer available until the Publisher is connected again.&#x20;

### Test Connection

Test Connection verifies connectivity and authentication between the Publisher and Patch My PC Cloud without changing the current connection state.

## Application Migration

When **Application Migration** is enabled, the Publisher inventories ConfigMgr applications and makes them available for migration to Intune through Patch My PC Cloud.

Discovery runs automatically every 60 minutes. Migration status and the number of discovered applications are shown for visibility and validation.

See [Setting up Migration](../../patch-my-pc-cloud/migration/setting-migration.md) for more information.

#### App Migration Database

When an app migration inventory runs, the Publisher saves the inventoried ConfigMgr results in the Publishing Service installation folder under the **Database** subfolder.

![Migration Database](/_images/image-(168).png "Migration Database")

This folder contains two files. **AppMigration.db** stores the app migration inventory data and processing state. **existingApps.json** contains a JSON copy of the discovery data.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>For reliability, consider exclude the **AppMigration.db** file from antivirus or endpoint protection scanning. This prevents the AppMigration.db file from being locked during scheduled scans, which can cause inventory or migration operations to fail.</p>
</blockquote>
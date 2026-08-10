# Setting Up ConfigMgr to Intune App Migration for Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Before you can perform a migration using the Patch My PC (PMPC) Cloud _Migration_ feature, you need to ensure that Publisher is connected to the same PMPC Cloud Company that you plan to migrate the objects to.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Add a Connection](../manage/settings/connections/add-connection.md) for further details.</p>
</blockquote>

You also need to ensure that the **Enable application migration** checkbox on the **Cloud** tab is checked.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you do not see the **Enable Application Migration** checkbox on the **Cloud** tab, ensure you are running the required version of Publisher as detailed in [Migration Requirements](requirements.md).</p>
<p>Also, if the <a href="https://docs.patchmypc.com/patch-my-pc-publisher/administration/cloud">Publisher was connected to the Cloud</a> more than 90 days ago, you may be prompted to sign in again using an account that has access to the Cloud Portal.</p>
<p>This is expected behavior as we do not control the authentication token, and once it expires, it must be renewed by re-authenticating.</p>
</blockquote>

!['Enable Application Migration' checkbox is checked on the 'Cloud' tab](/_images/image-(4859).png "&#x27;Enable Application Migration&#x27; checkbox is checked on the &#x27;Cloud&#x27; tab")

By default, Publisher polls the ConfigMgr Site Database every 60 minutes for application changes.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If you click **Disconnect** on the Publisher's **Cloud** tab, all of the Migration features data will be deleted from your PMPC Cloud company. You should therefore avoid doing this until you have completed the migration of all required items from ConfigMgr to PMPC Cloud.</p>
</blockquote>

Next, sign in to your PMPC Cloud company and verify that the **Migration** node is visible in the Cloud Portal.

!['Migration' node](/_images/image-(131).png "&#x27;Migration&#x27; node")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>The following log files can be used for more information and for troubleshooting the migration feature:</p>
<p>`"%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-AppMigrationService.log”`&#x20;</p>
<p>`"%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-CloudFileUploadBackgroundService.log”`</p>
<p>`"%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\PatchMyPC.log”`</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note:**</p>
<p>For new installations of Patch My PC Publisher, the **PatchMyPC.log** file will exist in the following folder:</p>
<p>`"%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs"`</p>
</blockquote>
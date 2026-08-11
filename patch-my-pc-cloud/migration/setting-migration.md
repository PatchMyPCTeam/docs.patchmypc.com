# Setting Up ConfigMgr to Intune App Migration for Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Before you can perform a migration using the Patch My PC (PMPC) Cloud _Migration_ feature, you need to ensure that Publisher is connected to the same PMPC Cloud Company that you plan to migrate the objects to.

{% hint style="info" %}
**Note**

See [Add a Connection](../manage/settings/connections/add-connection.md) for further details.
{% endhint %}

You also need to ensure that the **Enable application migration** checkbox on the **Cloud** tab is checked.

{% hint style="info" %}
**Note**

If you do not see the **Enable Application Migration** checkbox on the **Cloud** tab, ensure you are running the required version of Publisher as detailed in [Migration Requirements](requirements.md).

Also, if the [Publisher was connected to the Cloud](https://docs.patchmypc.com/patch-my-pc-publisher/administration/cloud) more than 90 days ago, you may be prompted to sign in again using an account that has access to the Cloud Portal.

This is expected behavior as we do not control the authentication token, and once it expires, it must be renewed by re-authenticating.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (4859).png" alt="&#x27;Enable Application Migration&#x27; checkbox is checked on the &#x27;Cloud&#x27; tab" width="563"><figcaption></figcaption></figure>

By default, Publisher polls the ConfigMgr Site Database every 60 minutes for application changes.

{% hint style="danger" %}
**Important**

If you click **Disconnect** on the Publisher's **Cloud** tab, all of the Migration features data will be deleted from your PMPC Cloud company. You should therefore avoid doing this until you have completed the migration of all required items from ConfigMgr to PMPC Cloud.
{% endhint %}

Next, sign in to your PMPC Cloud company and verify that the **Migration** node is visible in the Cloud Portal.

<figure><img src="../../.gitbook/assets/image (131).png" alt="&#x27;Migration&#x27; node" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

The following log files can be used for more information and for troubleshooting the migration feature:

`"%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-AppMigrationService.log”`&#x20;

`"%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-CloudFileUploadBackgroundService.log”`

`"%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\PatchMyPC.log”`
{% endhint %}

{% hint style="info" %}
**Note:**

For new installations of Patch My PC Publisher, the **PatchMyPC.log** file will exist in the following folder:

`"%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs"`
{% endhint %}

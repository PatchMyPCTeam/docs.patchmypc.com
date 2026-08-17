# Manage the Sync Schedule in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

By default, every day our sync job runs at 2 AM Coordinated Universal Time (UTC) to check if your deployments within Patch My PC (PMPC) Cloud are up-to-date.

The _Sync Schedule_ allows you to set a different time and frequency for the sync job to run.

To set a different time or frequency for the sync job:

1.  Navigate to **Settings | Sync Schedule**.<br>

    <figure><img src="../../../.gitbook/assets/image (2419).png" alt="Navigating to “Settings | Sync Schedule”"><figcaption></figcaption></figure>
2.  On the **Sync Schedule** page, make the required changes, then click **Save**.<br>

    <figure><img src="../../../.gitbook/assets/image-(464).png" alt="Clicking “Save” to save your changes"><figcaption></figcaption></figure>

    \
    The **Success – Sync Scheduler updated** notification is displayed.<br>

    <figure><img src="../../../.gitbook/assets/image-(465).png" alt="“Success – Sync Scheduler saved” notification"><figcaption></figcaption></figure>

## Other Frequencies

You can also choose to run the Sync Schedule on a Weekly or Monthly basis.

{% hint style="warning" %}
**Important**

If you are using [Update Rings](../../deployments/update-rings/), we recommend running the Sync Schedule daily to avoid potential issues with the timing of updates and the overall performance of this feature.

This is why the warning message about this is displayed whenever you select either the **Weekly** or **Monthly** options.
{% endhint %}

If you choose the **Weekly** option, as well as the time the sync runs, you can also choose which days it runs on.

<figure><img src="../../../.gitbook/assets/image (2818).png" alt="Choosing the “Weekly” option"><figcaption></figcaption></figure>

If you choose the **Monthly** option, as well as the time the sync runs, you can also choose to run it on a specific day of the month or a recurring pattern.

<figure><img src="../../../.gitbook/assets/image (2819).png" alt="Choosing the “Monthly” option"><figcaption></figcaption></figure>

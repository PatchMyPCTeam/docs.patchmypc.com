# Resume Updates to a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

If the _Pause Updates_ feature of Patch My PC (PMPC) Cloud has been configured for an app that has since been updated, and you want to bring the app up-to-date to the latest version, you need to disable pause updates.

{% hint style="info" %}
**Note**

If an app has more than one version of an update available, resuming updates will ensure it is updated to the latest version.

Also, if you paused a deployment with [Update Rings](../../update-rings/) enabled, when you resume updates for that deployment, the Update Rings are re-enabled and function normally.
{% endhint %}

To resume updates for an app:

1. Click on the relevant deployment that has been paused.

{% hint style="success" %}
**Tip**

Click the filter button (![](<../../../../.gitbook/assets/image (3215).png>)) and select the **Enabled** option under the **Updates** section, followed by **Apply Filters** to see just those deployments that have updates paused.&#x20;
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (2702).png" alt="Clicking on the relevant successful deployment which has been paused for updates"><figcaption></figcaption></figure>

2.  Click the **Pause Updates** slider to disable it.<br>

    <figure><img src="../../../../.gitbook/assets/image (2703).png" alt="Clicking the “Pause Updates” slider "><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Notice on the above screenshot that the **Sync Now** button is available, meaning one or more updates are available for this app.
{% endhint %}

3.  Click the **X** to close the deployment properties page.<br>

    <figure><img src="../../../../.gitbook/assets/image (2704).png" alt="Clicking “X” to close the deployment properties page"><figcaption></figcaption></figure>

    \
    The list of deployments is displayed without **UPDATES PAUSED** under the deployment you just unpaused.<br>

    <figure><img src="../../../../.gitbook/assets/image (2705).png" alt="&#x22;UPDATES PAUSED&#x22; no longer under the deployment name."><figcaption></figcaption></figure>

Updates for this app are now resumed.

You now need to decide how you want to install any updates for this app:

* **Install the updates now –** If you want to install the updates as soon as possible, follow the [Sync Now](sync-now.md) process.
* **Wait for the nightly sync to run –** If you are happy to wait for the updates to be installed the next time the daily sync runs (at 2 am by default), you do not need to do anything.

{% hint style="info" %}
**Note**

You can change the Sync Schedule to a different time, as detailed in the [Managing the Sync Schedule](../../../manage/settings/sync-schedule.md) process.
{% endhint %}

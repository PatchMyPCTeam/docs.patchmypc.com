# "Sync Now" Cloud feature

_Applies to: Patch My PC Cloud_

{% hint style="info" %}
**Note**

If an app has more than one version of an update available, using **Sync Now** ensures it is updated to the latest version as soon as possible, which could impact your users. So, think carefully before using this.
{% endhint %}

If you have [resumed updates](resume-cloud-updates.md) for an app in Patch My PC (PMPC) Cloud and want to update it as soon as possible rather than waiting for the nightly sync job to run:

1.  Click on the relevant deployment which has been resumed.\


    <figure><img src="/_images/gitbook/image%20%282004%29.png" alt="Clicking on the relevant successful deployment for which updates have been resumed"><figcaption></figcaption></figure>
2.  Click **Sync Now** to install any updates for the app immediately.\
    \


    <figure><img src="/_images/gitbook/image%20%282005%29.png" alt="Clicking “Sync Now”"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If the **Sync Now** button is greyed out, no updates are available for this app.
{% endhint %}

3.  On the **Are you sure you want to update <**_**app\_name**_**> to the latest version** popup, click **OK**.\


    <figure><img src="/_images/gitbook/image%20%281828%29.png" alt="&#x22;Are you sure you want to update <app_name> to the latest version&#x22; popup"><figcaption></figcaption></figure>

    \
    The **Deployment <**_**app\_name**_**> updated** notification is displayed and the deployment **Status** changes to **In Progress**.\


    <figure><img src="/_images/gitbook/image%20%281829%29.png" alt="“Deployment <app_name> updated” notification is displayed and the deployment “Status” changes to “In Progress”."><figcaption></figcaption></figure>

    \
    Once the deployment has been completed successfully, the **Status** changes to **Success**.\


    <figure><img src="/_images/gitbook/image%20%281830%29.png" alt="“Status” changing to Success."><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

If you look in the **Events node**, you will see the following event:

**Deployment <**_**app\_name**_**> Updated.**
{% endhint %}

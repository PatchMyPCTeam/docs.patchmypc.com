# About the "Summary" tab of a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

{% hint style="info" %}
**Note**

Reviewing the **Summary** tab is optional, but recommended.
{% endhint %}

The **Summary** tab of the Patch My PC (PMPC) Cloud deployment wizard provides a summary of the deployment so you can confirm that it is configured correctly before you create it.

<figure><img src="../../../.gitbook/assets/image (3093).png" alt="&#x22;Summary&#x22; tab"><figcaption></figcaption></figure>

Review the summary of the deployment shown on the **Summary** page.\
\
If you are happy click **Deploy**.\
\
If you need to change something, click **< Prev** to backtrack through the Deployment Wizard to the relevant setting. Make the change, then step back through the wizard to this page. If everything is now correct, click **Deploy**.

<figure><img src="../../../.gitbook/assets/image (3094).png" alt="Clicking &#x22;Deploy&#x22;"><figcaption></figcaption></figure>

{% hint style="info" %}
Note

If you have configured this deployment to use [Update Rings](../update-rings/), you will see the **Deployment Summary** screen, containing details on how you have configured the rings.

!["Deployment Summary" shown if this deloyment is using Update Rings](<../../../.gitbook/assets/image (2993).png>)

See [Update Rings](../update-rings/) for more information.
{% endhint %}

The App Catalog is redisplayed along with the **Success - Created&#x20;**_**\<deployment\_name>**_ notification.

<figure><img src="../../../.gitbook/assets/image (3095).png" alt="App Catalog is redisplayed along with the &#x22;Success - Created <deployment_name>&#x22; notification"><figcaption></figcaption></figure>

{% hint style="warning" %}
**Important**

When a new version of software is released, it is automatically deployed using the settings of the existing deployment. The old version will be removed from the target user/device and replaced with the newer version.
{% endhint %}

{% hint style="info" %}
**Note**

By default, the installation logs for an app will be created in the following folder regardless of the installer file type:

`%ProgramData%\PatchMyPCInstallLogs`

The only exception is for EXE files, where the specified value for the **loggingSwitch** variable will be used if it is not null or empty.
{% endhint %}

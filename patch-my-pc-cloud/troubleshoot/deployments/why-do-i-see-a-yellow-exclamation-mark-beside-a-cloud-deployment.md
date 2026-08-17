# Why do I see a yellow exclamation mark ("!") beside a Cloud deployment?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I’ve successfully deployed an app using Patch My PC (PMPC) Cloud, but when I look at the deployment, I see a yellow exclamation mark ("**!**") beside it in the **Status** column.

<figure><img src="../../../.gitbook/assets/image (3048).png" alt="Yellow exclamation mark beside a deployment"><figcaption></figcaption></figure>

### CAUSE

You need to hover over the exclamation mark ("**!**") as the message displayed will tell you what is causing the problem.

### RESOLUTION

Follow the relevant section for the error message you are seeing.

#### Failed to add application with version ‘_\<version\_number>_’ to app limit reached’ ESP Profile.

<figure><img src="../../../.gitbook/assets/image (3049).png" alt="“Failed to add application with version ‘<version_number>’ to app limit reached’ ESP Profile” error"><figcaption></figcaption></figure>

This message is telling you that when the Sync Schedule ran, a new version of an app was detected, which we successfully deployed.

However, we could not add this new version to the Enrollment Status Page (ESP) Profile to which this app is deployed, as the profile has reached the limit of 100 apps.

{% hint style="info" %}
**Note**

See [ESP Profiles](../../deployments/deploy-app/configurations-tab/additional-tools/esp-profiles.md) for more information.
{% endhint %}

To resolve this issue, you need to use the Intune admin center and from the ESP Profile remove either:

* An app that no longer needs to be a member
* The oldest version of the app.

#### Failed to apply new parent dependency for the child app '<_app\_name_>' '<_app\_version_>'

<figure><img src="../../../.gitbook/assets/image (3051).png" alt="“Failed to apply new parent dependency for the child app &#x27;<app_name>&#x27; &#x27;<app_version>&#x27;” error"><figcaption></figcaption></figure>

This message is telling you that the deployment of a dependency for this app has failed.

To resolve this issue, hover over the exclamation mark, which will tell you the name of the failed deployment.

Follow the [Recreate a Deployment](https://docs.patchmypc.com/installation-guides/patch-my-pc-cloud/deployments/manage-deployments/recreate-a-deployment) process to recreate this deployment, including all app dependencies.

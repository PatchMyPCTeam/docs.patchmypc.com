# "These settings are locked after deployment to prevent installation issues" message in Cloud

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to edit a Patch My PC (PMPC) Cloud deployment, but when I view its properties, options such as **Language** are greyed out and I see the message:

**These settings are locked after deployment to prevent installation issues. Create a new deployment to apply different settings**

<figure><img src="../../../.gitbook/assets/image (3214).png" alt="&#x22;These settings are locked after deployment to prevent installation issues. Create a new deployment to apply different settings&#x22;"><figcaption></figcaption></figure>

### CAUSE

As detailed in [Edit a Deployment](../../deployments/manage-deployments/edit.md), if when you edit an existing deployment several variants of the app are available, we prevent you from changing any settings that could lead to issues such as different installer variants of the same app being installed on devices with the currently deployed one already installed.

### RESOLUTION

If you need to change the settings for an existing deployment, you can:

* [Create a new deployment](../../deployments/deploy-app/) with the required settings if you want to keep the existing deployment.
* [Delete the existing deployment](../../deployments/manage-deployments/delete.md) and [create a new one](../../deployments/deploy-app/) with the required settings if you don't want to keep the existing deployment/modify it.

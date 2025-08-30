# "Error - Editing is not allowed until all rings are created after the configured delay" Cloud error

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to edit a Patch My PC (PMPC) Cloud deployment, but when I click on the ellipsis beside the deployment and choose **Edit**, I get the following error:

**Error - Editing is not allowed until all rings are created after the configured delay.**

![“Error - Editing is not allowed until all rings are created after the configured delay.” when trying to edit a deployment](/_images/image-%28458%29.png-"\"Error-Editing-is-not-allowed-until-all-rings-are-created-after-the-configured-delay.\"-when-trying-to-edit-a-deployment" "“Error - Editing is not allowed until all rings are created after the configured delay.” when trying to edit a deployment")

### CAUSE

This is because when the Update Rings were created for this deployment, the **Delayed** option was selected.

### RESOLUTION

As the **Delayed** option was selected for the Update Rings when this deployment was created, you cannot edit it until all of the configured Update Rings have finished being created.

{% hint style="info" %}
**Note**

Use the [Check if an Update Ring has been created](../../cloud-deployments/cloud-update-rings/check-if-an-update-ring-has-been-created-in-cloud.md) process to check if one or more Update Rings have yet to be created. If a ring shows as **Scheduled**, then you know this deployment was created with the **Delayed** option for the Update Rings.
{% endhint %}

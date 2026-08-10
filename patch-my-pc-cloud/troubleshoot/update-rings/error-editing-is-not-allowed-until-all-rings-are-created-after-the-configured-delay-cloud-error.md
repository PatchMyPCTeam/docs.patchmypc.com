# "Error - Editing is not allowed until all rings are created after the configured delay" Cloud error

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to edit a Patch My PC (PMPC) Cloud deployment, but when I click on the ellipsis beside the deployment and choose **Edit**, I get the following error:

**Error - Editing is not allowed until all rings are created after the configured delay.**

!["Error - Editing is not allowed until all rings are created after the configured delay." when trying to edit a deployment](/_images/image-(1160).png "“Error - Editing is not allowed until all rings are created after the configured delay.” when trying to edit a deployment")

### CAUSE

This is because when the Update Rings were created for this deployment, the **Delayed** option was selected.

### RESOLUTION

As the **Delayed** option was selected for the Update Rings when this deployment was created, you cannot edit it until all of the configured Update Rings have finished being created.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Use the [Check if an Update Ring has been created](../../deployments/update-rings/check.md) process to check if one or more Update Rings have yet to be created. If a ring shows as **Scheduled**, then you know this deployment was created with the **Delayed** option for the Update Rings.</p>
</blockquote>
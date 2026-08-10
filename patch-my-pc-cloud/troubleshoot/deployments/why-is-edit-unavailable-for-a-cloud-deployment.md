# Why is “Edit” Unavailable for a Cloud Deployment?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to edit a Patch My PC (PMPC) Cloud deployment, but when I view its properties, the **Edit** button is unavailable.

<figure><img src="../../../.gitbook/assets/image (2749).png" alt="“Edit” button unavailable on the properties of a deployment"><figcaption></figcaption></figure>

### CAUSE

This is because Update Rings have been configured for this deployment, and when it was created, the [Delayed](../../deployments/update-rings/update-ring-types.md#delayed-update-rings) option was selected.

### RESOLUTION

As the [Delayed](../../deployments/update-rings/update-ring-types.md#delayed-update-rings) option was selected for Update Rings when this deployment was created, you cannot edit it until all of the configured Update Rings have finished being created.

{% hint style="info" %}
**Note**

See [Check if an Update Ring has been created](../../deployments/update-rings/check.md) for more details.
{% endhint %}

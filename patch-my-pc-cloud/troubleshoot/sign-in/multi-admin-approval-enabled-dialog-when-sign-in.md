# Why do I see a “Multi Admin Approval Enabled” dialog when I sign in to Patch My PC Cloud?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

When I sign in to my Patch My PC (PMPC) Cloud company, why do I see a **Multi Admin Approval Enabled** dialog?

<figure><img src="../../../.gitbook/assets/image (1510).png" alt="‘Multi Admin Approval Enabled’ dialog" width="455"><figcaption></figcaption></figure>

### CAUSE

This is because your Microsoft Intune tenant has been configured to use one or more Multi Admin Approval access policies.

If you click **Close**, the Cloud Portal loads, but you will see the same message as a banner at the top.

<figure><img src="../../../.gitbook/assets/image (1511).png" alt="‘Multi Admin Approval Enabled’ banner" width="563"><figcaption></figcaption></figure>

Until you add the Patch My PC Cloud Enterprise Application as an exclusion to your MAA policy, PMPC Cloud functionality will be limited as detailed in [How Microsoft Intune Multi-Admin Approval affects Patch My PC products](../../../patch-my-pc-product-reference/how-intune-maa-affects-patch-my-pc-products.md).

### RESOLUTION

To resolve this issue, you need to add the Patch My PC Cloud Enterprise Application as an exclusion, as detailed in the [To add an exclusion](../../../patch-my-pc-product-reference/how-intune-maa-affects-patch-my-pc-products.md#to-add-an-exclusion) section of [How Microsoft Intune Multi-Admin Approval affects Patch My PC products](../../../patch-my-pc-product-reference/how-intune-maa-affects-patch-my-pc-products.md).&#x20;

Until you do this, PMPC Cloud functionality will be limited as detailed in [How Microsoft Intune Multi-Admin Approval affects Patch My PC products](../../../patch-my-pc-product-reference/how-intune-maa-affects-patch-my-pc-products.md).

{% hint style="info" %}
**Note**

See [Use access policies to require multi admin approval](https://learn.microsoft.com/en-us/intune/fundamentals/role-based-access-control/multi-admin-approval) for more details on Microsoft Intune Multi admin approval access policies.
{% endhint %}

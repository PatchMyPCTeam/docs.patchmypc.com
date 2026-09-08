# Manage Role Scope Tags option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: Intune Apps, Intune Updates_

The **Manage Role Scope Tags** right-click option in Patch My PC (PMPC) Publisher allows you to control which Intune role scope tags are applied to Win32 applications created by Publisher.

Role scope tags are part of Intune RBAC and limit which administrators can view or manage specific resources. By assigning scope tags, you ensure that only admins with matching role assignments and scope permissions can see or modify the applications created by the Publisher.

## To configure role scope tags:

1. Right-click the relevant item and select **Manage Role Scope Tags**. The list of available role scope tags is retrieved directly from your Intune tenant.
2. On the **Select scope tags** screen, check the relevant checkboxes for the scope tags you want to configure and click **OK**.

<figure><img src="../../../.gitbook/assets/image (925).png" alt="Selecting the relevant Scope Tags" width="375"><figcaption></figcaption></figure>

When Publisher creates a Win32 app, it automatically applies the selected role scope tags during publishing.

During each synchronization, Publisher evaluates existing Win32 apps that it previously created and compares the scope tags configured in Publisher with those assigned in Intune.&#x20;

Any scope tags selected in Publisher but missing on the Intune app are added.

{% hint style="info" %}
**Note**

Scope tags that already exist on the Intune app but are not defined in Publisher are not removed.

This behavior ensures the Publisher-configured tags are always present while allowing additional tags to be managed directly in Intune if required.
{% endhint %}

{% hint style="danger" %}
**Important**

Role scope tags affect administrator visibility and management only. They do not control application installation, availability, or assignment behavior.
{% endhint %}

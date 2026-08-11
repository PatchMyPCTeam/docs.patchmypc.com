# Manage Role Scope Tags option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: Intune Apps, Intune Updates_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Manage role scope tags** right-click option in Patch My PC (PMPC) Publisher allows you to control which Intune role scope tags are applied to Win32 applications created by the Publisher.

Role scope tags are part of Intune RBAC and are used to limit which administrators can view or manage specific resources. By assigning scope tags, you ensure that only admins with matching role assignments and scope permissions can see or modify the applications created by the Publisher.

## Select a Role Scope Tag

The list of available role scope tags is retrieved directly from your Intune tenant. You can select one or more tags to associate with an application.

![Select Scope Tags](../../../.gitbook/assets/image-\(113\).png)

When a Win32 application is created by the Publisher, the selected role scope tags are applied automatically during publishing.

During each synchronization, the Publisher evaluates existing Win32 applications that it previously created and compares the scope tags configured in the Publisher with the tags assigned in Intune. Any scope tags selected in the Publisher but missing on the Intune app are added.

> \*\*Note\*\*
>
> Scope tags that already exist on the Intune app but are not defined in the Publisher are not removed.
>
> This behavior ensures the Publisher configured tags are always present while allowing additional tags to be managed directly in Intune if required.

> \*\*Important\*\*
>
> Role scope tags only affect administrator visibility and management. They do not control application installation, availability, or assignment behavior.

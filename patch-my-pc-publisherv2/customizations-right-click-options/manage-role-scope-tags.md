# Manage Role Scope Tags

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_
\
_Available on tab: Intune Apps, Intune Updates_

## Overview

Manage Role Scope Tags allows you to control which Intune role scope tags are applied to Win32 applications created by the Publisher.

![Manage Role Scope Tags](/_images/image-(112).png "Manage Role Scope Tags")

Role scope tags are part of Intune RBAC and are used to limit which administrators can view or manage specific resources. By assigning scope tags, you ensure that only admins with matching role assignments and scope permissions can see or modify the applications created by the Publisher.

## Select a Role Scope Tag

The list of available role scope tags is retrieved directly from your Intune tenant. You can select one or more tags to associate with an application.

![Select Scope Tags](/_images/image-(113).png "Select Scope Tags")

When a Win32 application is created by the Publisher, the selected role scope tags are applied automatically during publishing.

During each synchronization, the Publisher evaluates existing Win32 applications that it previously created and compares the scope tags configured in the Publisher with the tags assigned in Intune. Any scope tags selected in the Publisher but missing on the Intune app are added.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Scope tags that already exist on the Intune app but are not defined in the Publisher are not removed.</p>
<p>This behavior ensures the Publisher configured tags are always present while allowing additional tags to be managed directly in Intune if required.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Role scope tags only affect administrator visibility and management. They do not control application installation, availability, or assignment behavior.</p>
</blockquote>
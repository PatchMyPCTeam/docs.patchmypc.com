# Delete Desktop Shortcut(s)

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Products, Vendor, Product_
\
_Available on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Delete desktop shortcut(s)** option automatically removes public desktop shortcuts created by an application installer. This applies only to shortcuts that are defined in the Patch My PC catalog for the product.

![Delete Desktop Shortcuts(s)](/_images/image-(4005).png "Delete Desktop Shortcuts(s)")

When enabled, Patch My PC ScriptRunner checks the public desktop location on the client device and deletes any shortcuts created by the installer that match the Patch My PC catalog definition.&#x20;

When enabled at the **Product** level, the setting applies only to that specific application. No confirmation dialog is displayed.

When enabled at the **Vendor** level, such as Oracle, the setting applies to all supported products for that vendor.

![Delete Desktop Shortcut(s) set at the Vendor level](/_images/image-(4007).png "Delete Desktop Shortcut(s) set at the Vendor level")

When enabled at the **All Products** level, the setting applies to all products that support desktop shortcut deletion.

![Delete Desktop Shortcut(s) set at the All Products level](/_images/image-(4006).png "Delete Desktop Shortcut(s) set at the All Products level")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Some applications create a desktop shortcut for the user the next time they sign in after an application or update is installed. In these cases, Patch My PC ScriptRunner, which managed the installation, cannot remove the shortcut retrospectively, as it is created outside of the installation process.</p>
<p>If required, these shortcuts must be removed using a separate automation or cleanup mechanism.</p>
</blockquote>
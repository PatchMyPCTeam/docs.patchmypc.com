# Delete Desktop Shortcut(s)

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: All Products, Vendor, Product_\
_&#x41;vailable on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Delete desktop shortcut(s)** option automatically removes public desktop shortcuts created by an application installer. This applies only to shortcuts that are defined in the Patch My PC catalog for the product.

![Delete Desktop Shortcuts(s)](../../.gitbook/assets/image-\(4005\).png)

When enabled, Patch My PC ScriptRunner checks the public desktop location on the client device and deletes any shortcuts created by the installer that match the Patch My PC catalog definition.

When enabled at the **Product** level, the setting applies only to that specific application. No confirmation dialog is displayed.

When enabled at the **Vendor** level, such as Oracle, the setting applies to all supported products for that vendor.

![Delete Desktop Shortcut(s) set at the Vendor level](../../.gitbook/assets/image-\(4007\).png)

When enabled at the **All Products** level, the setting applies to all products that support desktop shortcut deletion.

![Delete Desktop Shortcut(s) set at the All Products level](../../.gitbook/assets/image-\(4006\).png)

> \*\*Note\*\*
>
> Some applications create a desktop shortcut for the user the next time they sign in after an application or update is installed. In these cases, Patch My PC ScriptRunner, which managed the installation, cannot remove the shortcut retrospectively, as it is created outside of the installation process.
>
> If required, these shortcuts must be removed using a separate automation or cleanup mechanism.

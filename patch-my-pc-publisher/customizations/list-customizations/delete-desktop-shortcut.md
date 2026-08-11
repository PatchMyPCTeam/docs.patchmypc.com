# Delete Desktop Shortcut option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Products, Vendor, Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Delete Desktop Shortcut** right-click option in Patch My PC (PMPC) Publisher automatically removes public desktop shortcuts created by an application installer. This applies only to shortcuts that are defined in the Patch My PC catalog for the product.

When enabled, Patch My PC ScriptRunner checks the public desktop location on the client device and deletes any shortcuts created by the installer that match the Patch My PC catalog definition.

When enabled at the **Product** level, the setting applies only to that specific application. No confirmation dialog is displayed.

When enabled at the **Vendor** level, such as Oracle, the setting applies to all supported products for that vendor.

!['Delete Desktop Shortcut' set at the Vendor level](/_images/image-(4420).png)

When enabled at the **All Vendors** level, the setting applies to all products that support deleting desktop shortcuts.

!['Delete Desktop Shortcut' set at the 'All Vendors' level](/_images/image-(4421).png)

> \*\*Note\*\*
>
> Some applications create a desktop shortcut for the user the next time they sign in after an application or update is installed.
>
> In these cases, Patch My PC ScriptRunner, which managed the installation, cannot remove the shortcut retroactively, as it was created outside the installation process.
>
> If required, these shortcuts must be removed using a separate automation or cleanup mechanism.
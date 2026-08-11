# Exclude from Auto-Publishing Rules

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: Vendor, Product_\
_&#x41;vailable on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Exclude from Auto-Publishing Rules** option allows you to prevent specific vendors or products from being automatically enabled for publishing by the Publishers auto-publishing logic.

![Exclude from Auto-Publishing Rules](/_images/image-(4066).png)

This is useful when you want to maintain full manual control over which applications or updates are enabled, even when inventory-based auto-publishing rules are in use.

The Publisher includes an inventory-based auto-publishing feature that can automatically enable applications or updates when they are detected on a defined number of devices. This uses platform inventory data to determine how widely a product is installed before enabling it for publishing.

Auto-publishing can be configured independently on each supported tab using the Scan for Supported Products form control. Each link below opens that configuration for the corresponding area:

* [Updates](../administration/updates/form-controls/scan-configmgr-database-for-supported-products.md)
* [ConfigMgr Apps](../administration/configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md)
* [Intune Apps](../administration/intune-apps-updates/form-controls/scan-intune-for-supported-products.md)
* [Intune Updates](../administration/intune-apps-updates/form-controls/scan-intune-for-supported-products.md)

The **Exclude from Auto-Publishing Rules** right-click option acts as an explicit override. When applied, the selected vendor or product will never be automatically enabled, even if auto-publishing is configured and the device threshold is met.

> \*\*Important\*\*
>
> Vendor level exclusion applies only to products that exist at the time the exclusion is configured. Any new products added to the Patch My PC catalog for that vendor in the future are not excluded automatically and must be reviewed and excluded manually if needed.
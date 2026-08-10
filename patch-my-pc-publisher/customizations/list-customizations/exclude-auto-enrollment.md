# Exclude From Auto-Enrollment option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: Vendor, Product_
\
_Available on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Exclude From Auto-Enrollment** right-click option in Patch My PC (PMPC) Publisher allows you to prevent specific vendors or products from being automatically enabled for publishing by Publisher's auto-publishing logic.

This is useful when you want to maintain full manual control over which applications or updates are enabled, even when inventory-based auto-publishing rules are in use.

Publisher includes an inventory-based auto-publishing feature that can automatically enable applications or updates when they are detected on a defined number of devices. This uses platform inventory data to determine how widely a product is installed before enabling its publication.

Auto-publishing can be configured independently on each supported tab using the **Scan** tab for each product:

* [WSUS Updates](../../manage/wsus-updates-tab/scan-configmgr.md)
* [ConfigMgr Apps](../../manage/wsus-updates-tab/scan-configmgr.md)
* [Intune Apps/ Updates](../../manage/intune-tabs/scan-intune.md)

The **Exclude From Auto-Enrollment** right-click option acts as an explicit override. When applied, the selected vendor or product will never be automatically enabled, even if auto-publishing is configured and the device threshold is met.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Vendor-level exclusion applies only to products that exist when the exclusion is configured. Any new products added to the Patch My PC catalog for that vendor in the future are not automatically excluded and must be reviewed and manually excluded if needed.</p>
</blockquote>
# Sync Schedule support for Multi-tenants in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

In a multi-tenant configuration, there is _no_ independent sync schedule per tenant.

The **Sync Schedule** tab in Patch My PC (PMPC) Publisher defines a single global schedule for the entire Publisher instance. When the configured sync time occurs, the Publisher evaluates all enabled product selections across all configured tenants and processes publishing accordingly.

![Sync Schedule Options](../../../.gitbook/assets/image-\(4121\).png)

## Selective Sync for MSP Scenarios

Although the scheduled sync is global, MSP customers can still perform targeted publishing using the [Selective Sync right-click option](../../../patch-my-pc-publisherv2/customizations-right-click-options/publish-this-product-during-the-next-manual-sync-selective-sync.md). This allows you to manually synchronize specific applications or updates without waiting for the next scheduled sync.

Selective Sync processes only the selected applications or updates for the currently selected tenant. This provides flexibility for MSPs who need to publish changes for a single customer without triggering a full global sync across all tenants.

To synchronize all selected products for a **single** MSP customer, first select the tenant from the tenant drop down list. Then right click the **All Products** node and choose [Publish this Product During the Next Manual Sync (Selective Sync)](../../../patch-my-pc-publisherv2/customizations-right-click-options/publish-this-product-during-the-next-manual-sync-selective-sync.md).

![Sync a single tenant](../../../.gitbook/assets/image-\(4124\).png)

This will process all enabled applications and updates for that selected tenant only.

![Sync a single tenant confirmation](../../../.gitbook/assets/image-\(4123\).png)

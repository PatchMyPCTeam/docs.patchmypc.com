# Publish this Product During the Next Manual Sync (Selective Sync)

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

The **Publish This Product During the Next Manual Sync** option allows you to selectively publish one or more specific products during the next manual publishing service sync.

![Selective Sync](../../.gitbook/assets/image-\(4071\).png)

When this option is used, only the selected products are evaluated and processed during the next manual publishing service sync.

Selective Sync is designed to reduce processing time and scope when a full evaluation of all products is unnecessary.

## How Selective Sync Works

By default, running a [manual publishing service sync](../administration/sync-schedule.md#run-publishing-service-sync) causes the Publisher to evaluate every enabled product across all platform tabs. In environments with a large number of products, this can take a significant amount of time.

When Selective Sync is enabled for a product, the Publisher flags that product to be included in the next manual sync. During that sync, only products marked for Selective Sync are processed.

> \*\*Note\*\*
>
> Selective Sync applies only to manual syncs initiated from the Sync Schedule tab. It does not apply to scheduled syncs.

## When to Use Selective Sync

Selective Sync is useful in scenarios where you want to limit processing to a small set of products.

Common use cases include testing a new configuration, validating a recent change, troubleshooting a publishing issue, or quickly republishing or updating a single application without running a full sync cycle.

### Selective Sync Behavior

When you use the right-click option to select a product or products for selective sync, you are prompted to confirm that decision.

![Selective Sync confirmation](../../.gitbook/assets/image-\(4073\).png)

When you select Run Publishing Service Sync from the Sync Schedule tab, the Publisher displays a list of all products currently marked for Selective Sync.

![Run a manual Publishing Service Sync](../../.gitbook/assets/image-\(4072\).png)

![Confirm Product(s) for Selective Sync](../../.gitbook/assets/image-\(4074\).png)

Clicking **OK** starts a manual sync that processes only those selected products.

If you click **Cancel** instead, you are prompted to choose how to proceed.

![Cancelled Selective Sync](../../.gitbook/assets/image-\(4075\).png)

Clicking **Yes** clears all Selective Sync flags and immediately runs a normal full publishing service sync. All enabled products across all platforms will be evaluated and processed.

Clicking **No** keeps the existing Selective Sync flags in place and returns you to the console without running a sync. This allows you to modify the current Selective Sync selections or run the manual sync at a later time using the same selected products.

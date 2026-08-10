# Publish this Product During the Next Manual Sync (Selective Sync)

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_\
_Available on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

The **Publish This Product During the Next Manual Sync** option allows you to selectively publish one or more specific products during the next manual publishing service sync.

<figure><img src="../../.gitbook/assets/image (4071).png" alt="Selective Sync" width="556"><figcaption></figcaption></figure>

When this option is used, only the selected products are evaluated and processed during the next manual publishing service sync.

Selective Sync is designed to reduce processing time and scope when a full evaluation of all products is unnecessary.

## How Selective Sync Works

By default, running a [manual publishing service sync](../administration/sync-schedule.md#run-publishing-service-sync) causes the Publisher to evaluate every enabled product across all platform tabs. In environments with a large number of products, this can take a significant amount of time.

When Selective Sync is enabled for a product, the Publisher flags that product to be included in the next manual sync. During that sync, only products marked for Selective Sync are processed.

{% hint style="info" %}
**Note**

Selective Sync applies only to manual syncs initiated from the Sync Schedule tab. It does not apply to scheduled syncs.
{% endhint %}

## When to Use Selective Sync

Selective Sync is useful in scenarios where you want to limit processing to a small set of products.

Common use cases include testing a new configuration, validating a recent change, troubleshooting a publishing issue, or quickly republishing or updating a single application without running a full sync cycle.

### Selective Sync Behavior

When you use the right-click option to select a product or products for selective sync, you are prompted to confirm that decision.

<figure><img src="../../.gitbook/assets/image (4073).png" alt="Selective Sync confirmation" width="430"><figcaption></figcaption></figure>

When you select Run Publishing Service Sync from the Sync Schedule tab, the Publisher displays a list of all products currently marked for Selective Sync.

<figure><img src="../../.gitbook/assets/image (4072).png" alt="Run a manual Publishing Service Sync" width="545"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4074).png" alt="Confirm Product(s) for Selective Sync" width="525"><figcaption></figcaption></figure>

Clicking **OK** starts a manual sync that processes only those selected products.

If you click **Cancel** instead, you are prompted to choose how to proceed.

<figure><img src="../../.gitbook/assets/image (4075).png" alt="Cancelled Selective Sync" width="383"><figcaption></figcaption></figure>

Clicking **Yes** clears all Selective Sync flags and immediately runs a normal full publishing service sync. All enabled products across all platforms will be evaluated and processed.

Clicking **No** keeps the existing Selective Sync flags in place and returns you to the console without running a sync. This allows you to modify the current Selective Sync selections or run the manual sync at a later time using the same selected products.

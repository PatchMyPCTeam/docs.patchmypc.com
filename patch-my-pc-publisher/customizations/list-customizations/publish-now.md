# Publish Now option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Publish Now** right-click option in Patch My PC (PMPC) Publisher allows you to selectively publish one or more specific products during the next manual publishing service sync.

When used, only the selected products are evaluated and processed during the next manual publishing service sync.

Selective Sync is designed to reduce processing time and scope when a full evaluation of all products is unnecessary.

## How Selective Sync Works

By default, running a [manual publishing service sync](../../manage/sync-schedule-tab/sync-status.md#run-publishing-service-sync) causes Publisher to evaluate every enabled product across all platform tabs. In environments with a large number of products, this can take a significant amount of time.

When Selective Sync is enabled for a product, Publisher flags it for inclusion in the next manual sync. During that sync, only products marked for Selective Sync are processed.

{% hint style="info" %}
**Note**

Selective Sync applies only to manual syncs initiated from the **Sync Schedule** tab. It does not apply to scheduled syncs.
{% endhint %}

## When to Use Selective Sync

Selective Sync is useful when you want to limit processing to a small set of products.

For example:

* Testing a new configuration
* Validating a recent change
* Troubleshooting a publishing issue
* Quickly republishing or updating a single application without running a full sync cycle.

### Enabling Selective Sync Behavior

When you right-click at a supported level in the Product Tree and select **Publish Now**, the **Selective Sync** dialog appears.

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1).png" alt="&#x27;Selective Sync&#x27; dialog box" width="461"><figcaption></figcaption></figure>

If you click **Yes**, the selected items are added to the queue for the next Selective Sync, which can be triggered by [Running a Selective Sync](../../manage/sync-schedule-tab/sync-status.md#running-a-selective-sync).

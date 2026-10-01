# Auto-Publishing Rules section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **AUTO-PUBLISHING RULES** section on the **Scan ConfigMgr** tab of Patch My PC (PMPC) Publisher defines how Publisher connects to Microsoft Configuration Manager (ConfigMgr) and where it stores application source content.

<figure><img src="/broken/files/kDYOhUFKAhNgrRgROs2f" alt="&#x27;AUTO-PUBLISHING RULES&#x27; section" width="563"><figcaption></figcaption></figure>

_Auto-publishing rules_ allow Publisher to automatically enable products for publishing based on what is detected in your ConfigMgr environment, removing the need to manually review scan results and enabling a more hands-off approach to keeping third-party updates current.

When these rules are enabled, Publisher evaluates application inventory data collected by ConfigMgr, compares detected applications against the PMPC catalog, and automatically enables supported products that meet the configured device threshold.

{% hint style="danger" %}
**Important**

These rules rely on the same ConfigMgr database access and SQL permissions described in the [Connect to ConfigMgr SQL Database As](sql-configuration.md#connect-to-configmgr-sql-database-as) section.
{% endhint %}

Auto-publishing rules are evaluated during scheduled [synchronizations](../../sync-schedule-tab/). Each time a sync runs, Publisher scans application inventory data from ConfigMgr and automatically enables any newly detected products that meet the configured thresholds.

This automation can be extremely powerful, but it’s important to configure it thoughtfully.

## Auto-enable products to be published as an update

When the **Auto-enable products to be published as an update** option is enabled, products detected in ConfigMgr inventory are automatically enabled on the **WSUS Updates** tab once they are found on at least the specified number of devices.

* The device count acts as a threshold to prevent enabling products seen only on a small number of devices.
* Once enabled, updates for the product are published according to your existing sync and deployment processes.

This option is commonly used to keep patching coverage up to date as new applications appear in the environment.

### Also publish as **Metadata Only when** found but the threshold is not met

The **Also publish as Metadata Only when found but the threshold is not met** option works with [Auto-enable products to be published as an update.](auto-publishing-rules.md#auto-enable-products-to-be-published-as-an-update)

When enabled:

* Products detected below the configured device threshold are enabled as Metadata Only.
* No update content is downloaded or stored in WSUS.
* WSUS can still evaluate applicability and compliance for those products.

This is particularly useful for **early visibility** of newly discovered or low-prevalence applications without immediately introducing update content into the environment.

## Auto-enable products to be published as an application

Enabling the **Auto-enable products to be published as an application** option automatically enables products detected in ConfigMgr inventory on the [ConfigMgr Apps](../) tab once they are found on at least the specified number of devices.

When checked:

* Publisher can automatically manage application creation for newly detected software.
* The same device threshold concept applies to avoid enabling applications prematurely.

This option is typically used in environments that want application lifecycle management to be driven directly from inventory data.

## Device Threshold Best Practice

Patch My PC releases several hundred new applications per month, so it’s entirely possible for a scheduled scan to detect multiple new products. When low device thresholds are used, auto-publishing can enable these products very quickly, ensuring new additions don’t go unnoticed.&#x20;

However, this speed should be balanced with operational readiness, as downstream processes such as Automatic Deployment Rules (ADRs), testing, and change control may not be prepared for a sudden influx of updates, particularly when ADRs are broadly scoped and evaluate new content with little or no delay.

{% hint style="danger" %}
**Important**

Whilst it may be tempting to set the device threshold to a very low number (even **1**), this is generally not recommended for most environments. This would be especially impactful for new customers who have not yet reviewed and enabled products in the Product Tree, as a very low threshold can cause newly discovered applications to be enabled simultaneously, potentially resulting in a large number of updates being synchronized at once.
{% endhint %}

A common and effective approach is:

1. Use **Scan ConfigMgr** to identify products currently installed in your environment.
2. Enable these products from the [scan wizard query window](auto-publishing-rules.md#query-button) or [Product Tree](../../../fundamentals/product-tree/working.md), and [customize](../../../customizations/) those products from the Product Tree (conflicting processes, content options, etc.).
3. Enable auto-publishing rules to catch newly introduced applications over time.

This lets you stay in control initially while still benefiting from automation going forward.

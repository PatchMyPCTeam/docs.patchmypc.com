# Discover ConfigMgr/WSUS Updates using Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This page provides guidance on how to discover third-party applications in your environment or manually select products for publishing using Patch My PC (PMPC) Publisher.

Updates are always published to Microsoft WSUS. When integrated with Microsoft Configuration Manager (ConfigMgr), those updates are synchronized from WSUS to ConfigMgr during a Software Update Point synchronization.

In ConfigMgr environments, you can scan the ConfigMgr database to discover supported third party products based on existing inventory.

In standalone WSUS environments, you cannot scan the ConfigMgr database. In this scenario, products must be manually selected from the Publisher catalog.

After completing the steps in this section, Publisher will be configured to identify and enable supported third party updates for publishing to WSUS.

## Discovering and Selecting Updates

Your approach differs slightly depending on whether WSUS is [integrated with ConfigMgr](discover-configmgr-wsus-updates.md#configmgr-integrated-with-wsus) or running as a [standalone WSUS server](discover-configmgr-wsus-updates.md#standalone-wsus).

### ConfigMgr Integrated with WSUS

You can enable updates for publishing in one of two ways:

* [Automatically discover installed products by querying the ConfigMgr database](discover-configmgr-wsus-updates.md#automatically-discover-installed-products-by-querying-the-configmgr-database)
* [Manually browse and select products directly from the Product Tree on the WSUS Updates tab](discover-configmgr-wsus-updates.md#manually-browse-and-select-products-directly-from-the-product-tree-on-the-wsus-updates-tab)

#### Automatically discover installed products by querying the ConfigMgr database

Running a [query](../../manage/intune-tabs/scan-intune/filters-discovered-products.md#query-button) on the  [Scan ConfigMgr](../../manage/configmgr-apps-tab/scan-configmgr/) tab is the recommended starting point, as the scan leverages ConfigMgr hardware inventory data to identify supported third-party products currently present in your environment and compares those results against the Patch My PC catalog. This allows you to review what is installed _today_ before enabling publishing.

After running a [query](../../manage/intune-tabs/scan-intune/filters-discovered-products.md#query-button), review the results carefully. The device [count](../../manage/intune-tabs/scan-intune/filters-discovered-products.md#count-column) and version information help validate inventory accuracy and determine publishing priority. [Exporting the results to CSV](../../manage/intune-tabs/scan-intune/filters-discovered-products.md#to-export-the-results-to-a-csv) can support internal review, change-control discussions, or phased rollout planning.

A common and effective approach is to begin conservatively. Enable a small number of familiar, low-impact updates to understand how ConfigMgr applications are created by Publisher. Many customers start with widely used utilities such as 7-Zip or Notepad++ to gain confidence in the workflow.

Once you are comfortable with how updates are created and maintained, you can expand your product selection or consider enabling [auto-publishing rules](../../manage/intune-tabs/scan-intune/auto-publishing-rules.md) to automate application lifecycle management over time to publish updates for different products based on discovery thresholds.

### Manually browse and select products directly from the Product Tree on the WSUS Updates tab

Updates can also be enabled manually by selecting products directly from the [Product Tree](../../fundamentals/product-tree/working.md) on the [WSUS Updates](../../manage/wsus-updates-tab/) tab.

You can expand vendors to browse available products or use the [Filter](../../fundamentals/product-tree/working.md#filter-field) field to quickly locate a specific update by name.

Unlike the advice for [ConfigMgr application selection](discover-configmgr-applications.md#manually-browse-and-select-products-directly-from-the-product-tree-on-the-configmgr-apps-tab), it is often appropriate to enable multiple update variants if they exist in your estate. For example, if both x86 and x64 variants are detected, publishing updates for both ensures all devices remain compliant while you work toward long-term standardization.

As a best practice, begin by enabling a small number of familiar, low-impact updates to understand how ConfigMgr updates are created by the Publisher. Many customers start with widely used utilities such as 7-Zip or Notepad++ to gain confidence in the workflow.

### Standalone WSUS

In standalone WSUS environments, you cannot run a [query](../../manage/intune-tabs/scan-intune/filters-discovered-products.md#query-button) on the  [Scan ConfigMgr](../../manage/configmgr-apps-tab/scan-configmgr/) tab as there is no ConfigMgr Site Database to query.

In this scenario, you must manually enable products from the [Product Tree](../../fundamentals/product-tree/working.md) on the [WSUS Updates](../../manage/wsus-updates-tab/) tab.

You can expand vendors to browse available products or use the [Filter](../../fundamentals/product-tree/working.md#filter-field) field to quickly locate a specific update by name.

{% hint style="info" %}
**Note**

See [Manually browse and select products directly from the Product Tree on the WSUS Updates tab](discover-configmgr-wsus-updates.md#manually-browse-and-select-products-directly-from-the-product-tree-on-the-wsus-updates-tab) for advice on using the Product Tree to select updates manually for publishing.
{% endhint %}

## Inventory Variants and Update Selection

Scan results obtained by Publisher from ConfigMgr hardware inventory may not always accurately reflect the exact installer variant deployed on a device. This is due to differences in how vendors name products in Add/Remove Programs and how that data is surfaced through ConfigMgr inventory views.

For example, inventory data may indicate that 7-Zip (x64) is installed, but it may not clearly distinguish whether the MSI or EXE variant was originally used. As a result, multiple update variants may appear as potential matches in the scan results.

To account for this ambiguity, consider one of the following approaches:

* **Enable all variants as Metadata Only First**\
  Enabling [Switch to Metadata Only](../../customizations/list-customizations/switch-full-content-metadata-only.md#switch-to-metadata-only) allows the Windows Update Agent on the device to evaluate applicability and report compliance back to ConfigMgr without downloading full update content. After reviewing compliance results, you can determine which specific variant(s) should be enabled with full content.
* **Enable all update variants as Full Content**\
  In environments where multiple variants may exist and immediate patch coverage is the priority, enabling [Switch to Full Content](../../customizations/list-customizations/switch-full-content-metadata-only.md#switch-to-full-content) for all update variants ensures that no installed instance remains unpatched when deployments are targeted.

Using [Switch to Metadata Only](../../customizations/list-customizations/switch-full-content-metadata-only.md#switch-to-metadata-only) as an initial step is often the most controlled approach, particularly in WSUS standalone environments. It provides visibility into what is truly installed before introducing update binaries into WSUS.

{% hint style="info" %}
**Note**

See [Switch to Full Content/Metadata Only option](../../customizations/list-customizations/switch-full-content-metadata-only.md) for more information about the metadata options when publishing updates.
{% endhint %}

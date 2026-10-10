# Discover ConfigMgr Applications using Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This page provides guidance on how to discover applications in your environment or manually select products for publishing as Microsoft ConfigMgr applications using the Patch My PC (PMPC) Publisher.

You can scan the ConfigMgr database to automatically discover supported products installed in your environment, or manually browse and select products directly from the Publisher catalog.

After completing the steps in this section, you will be able to enable and publish third party applications that align with your environment’s needs.

You can enable applications for publishing in one of two ways:

* [Automatically discover installed products by querying the ConfigMgr database](discover-configmgr-applications.md#automatically-discover-installed-products-by-querying-the-configmgr-database)
* [Manually browse and select products directly from the product tree on the ConfigMgr Apps tab](discover-configmgr-applications.md#manually-browse-and-select-products-directly-from-the-product-tree-on-the-configmgr-apps-tab)

## Automatically discover installed products by querying the ConfigMgr database

Running a [query](../../manage/intune-tabs/scan-intune/filters-discovered-products.md#query-button) on the  [Scan ConfigMgr](../../manage/configmgr-apps-tab/scan-configmgr/) tab is the recommended starting point, as the scan leverages ConfigMgr hardware inventory data to identify supported third-party products currently present in your environment and compares those results against the Patch My PC catalog. This allows you to review what is installed _today_ before enabling publishing.

After running a [query](../../manage/intune-tabs/scan-intune/filters-discovered-products.md#query-button), review the results carefully. The device [count](../../manage/intune-tabs/scan-intune/filters-discovered-products.md#count-column) and version information help validate inventory accuracy and determine publishing priority. [Exporting the results to CSV](../../manage/intune-tabs/scan-intune/filters-discovered-products.md#to-export-the-results-to-a-csv) can support internal review, change-control discussions, or phased rollout planning.

A common and effective approach is to begin conservatively. Enable a small number of familiar, low-impact applications to understand how ConfigMgr applications are created by Publisher. Many customers start with widely used utilities such as 7-Zip or Notepad++ to gain confidence in the workflow.

Once you are comfortable with how applications are created and maintained, you can expand your product selection or consider enabling [auto-publishing rules](../../manage/configmgr-apps-tab/scan-configmgr/auto-publishing-rules.md) to automate application lifecycle management over time to create new applications based on discovery thresholds.

## Manually browse and select products directly from the product tree on the ConfigMgr Apps tab

Applications can also be enabled manually by selecting products directly from the [Product Tree](../../fundamentals/product-tree/working.md) on the [ConfigMgr Apps](../../manage/configmgr-apps-tab/) tab.

Manual selection remains a valid and flexible option, especially when you want to proactively publish applications that may not yet appear in the inventory returned by the scan results.

You can expand vendors to browse available products or use the [Filter](../../fundamentals/product-tree/working.md#filter-field) field to quickly locate a specific application by name.

When selecting products, we recommend standardizing on a single installer variant whenever multiple options are available. For example, some products may provide:

* MSI and EXE variants
* x86 and x64 architectures
* ARM64 variants.

In most environments, it is recommended to standardize on a single architecture and installer type, such as **MSI (x64)**, unless there is a specific requirement for an alternative variant.

{% hint style="info" %}
**Note**

This guidance applies to specifically to applications. For updates, it is common to publish multiple variants if they currently exist in your environment, particularly while working toward a longer-term standardization strategy.
{% endhint %}

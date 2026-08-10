# Discover ConfigMgr Applications using Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

This page provides guidance on how to discover applications in your environment or manually select products for publishing as ConfigMgr applications using the Patch My PC (PMPC) Publisher.

You can scan the ConfigMgr database to automatically discover supported products installed in your environment, or manually browse and select products directly from the Publisher catalog.

After completing the steps in this section, you will be able to enable and publish third party applications that align with your environment’s needs.

## Discovering and Selecting Applications

You can enable applications for publishing in one of two ways:

* [Automatically discover installed products by scanning the ConfigMgr database using the Scan Wizard](discover-configmgr-applications.md#automatically-discover-installed-products-by-scanning-the-configmgr-database-using-the-scan-wizard).
* [Manually browse and select products directly from the product tree on the ConfigMgr Apps tab](discover-configmgr-applications.md#manually-browse-and-select-products-directly-from-the-product-tree-on-the-configmgr-apps-tab).

### Automatically discover installed products by scanning the ConfigMgr database using the Scan Wizard

The [Scan Wizard](../../../patch-my-pc-publisherv2/administration/configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md) is generally a recommended starting point. It leverages ConfigMgr hardware inventory data to identify supported third-party products currently present in your environment and compares those results against the Patch My PC catalog. This allows you to review what is installed _today_ before enabling publishing.

![ConfigMgr Apps Scan Wizard](/_images/image-(4156).png)

After running a scan, review the results carefully. The device count and version information help validate inventory accuracy and determine publishing priority. Exporting the results to CSV can assist with internal review, change control discussions, or phased rollout planning.

A common and effective approach is to begin conservatively. Enable a small number of familiar, low-impact applications to understand how ConfigMgr applications are created by the Publisher. Many customers start with widely used utilities such as 7-Zip or Notepad++ to gain confidence in the workflow.

Once you are comfortable with how applications are created and maintained, you can expand product selections or consider enabling [auto-publishing rules](../../../patch-my-pc-publisherv2/administration/configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md#auto-enable-products-to-be-published-as-an-application) to automate application lifecycle management over time to create new applications based on discovery thresholds.

### Manually browse and select products directly from the product tree on the ConfigMgr Apps tab

Applications can also be enabled manually by selecting products directly from the [product tree](../../../patch-my-pc-publisherv2/administration/configmgr-apps/product-tree.md) on the [ConfigMgr Apps](../../../patch-my-pc-publisherv2/administration/configmgr-apps/) tab.

Manual selection remains a valid and flexible option, especially when you want to proactively publish applications that may not yet appear in the inventory returned by the scan results.

![Manual Product Selection](/_images/image-(4157).png)

You can expand vendors to browse available products or use the [Search](../../../patch-my-pc-publisherv2/administration/configmgr-apps/form-controls/search-products.md) form control to quickly locate a specific application by name.

When selecting products, we recommend to standardize on a single installer variant whenever multiple options are available. For example, some products may provide:

* MSI and EXE variants
* x86 and x64 architectures
* ARM64 variants

In most environments, it is recommended to standardize on a single architecture and installer type, such as **MSI (x64)**, unless there is a specific requirement for an alternative variant.

> \*\*Note\*\*
>
> This guidance applies to specifically to applications. For updates, it is common to publish multiple variants if they currently exist in your environment, particularly while working toward a longer term standardization strategy.

As a best practice, begin by enabling a small number of familiar, low-impact applications to understand how ConfigMgr applications are created by the Publisher. Many customers start with widely used utilities such as 7-Zip or Notepad++ to gain confidence in the workflow.
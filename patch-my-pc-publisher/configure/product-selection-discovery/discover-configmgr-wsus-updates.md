# Discover ConfigMgr/WSUS Updates using Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

This page provides guidance on how to discover third-party applications in your environment or manually select products for publishing using the Patch My PC (PMPC) Publisher.

Updates are always published to WSUS. When integrated with ConfigMgr, those updates are synchronized from WSUS to ConfigMgr during a Software Update Point synchronization.

In ConfigMgr environments, you can scan the ConfigMgr database to discover supported third party products based on existing inventory.

In standalone WSUS environments, scanning the ConfigMgr database is not available. In this scenario, products must be manually selected from the Publisher catalog.

After completing the steps in this section, the Publisher will be configured to identify and enable supported third party updates for publishing to WSUS.

## Discovering and Selecting Updates

The approach differs slightly depending on whether WSUS is integrated with ConfigMgr or running as a standalone WSUS server.

### ConfigMgr Integrated with WSUS

You can enable applications for publishing in one of two ways:

* [Automatically discover installed products by scanning the ConfigMgr database using the Scan Wizard](discover-configmgr-wsus-updates.md#automatically-discover-installed-products-by-scanning-the-configmgr-database-using-the-scan-wizard).
* [Manually browse and select products directly from the product tree on the Updates Apps tab](discover-configmgr-wsus-updates.md#manually-browse-and-select-products-directly-from-the-product-tree-on-the-updates-apps-tab).

#### Automatically discover installed products by scanning the ConfigMgr database using the Scan Wizard

The [Scan Wizard](../../../patch-my-pc-publisherv2/administration/updates/form-controls/scan-configmgr-database-for-supported-products.md) is generally a recommended starting point. It leverages ConfigMgr hardware inventory data to identify supported third-party products currently present in your environment and compares those results against the Patch My PC catalog. This allows you to review what is installed _today_ before enabling publishing.

![ConfigMgr Apps Scan Wizard](/_images/image-(4158).png)

After running a scan, review the results carefully. The device count and version information help validate inventory accuracy and determine publishing priority. Exporting the results to CSV can assist with internal review, change control discussions, or phased rollout planning.

A common and effective approach is to begin conservatively. Enable a small number of familiar, low-impact updates to understand how updates are created by the Publisher. Many customers start with widely used utilities such as 7-Zip or Notepad++ to gain confidence in the workflow.

Once you are comfortable with how updates are created and maintained, you can expand product selections or consider enabling [auto-publishing rules](../../../patch-my-pc-publisherv2/administration/configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md#auto-enable-products-to-be-published-as-an-application) to automate update lifecycle management over time to publish updates for different products based on discovery thresholds.

#### Manually browse and select products directly from the product tree on the Updates Apps tab

Updates can also be enabled manually by selecting products directly from the [product tree](../../../patch-my-pc-publisherv2/administration/updates/product-tree.md) on the [Updates](../../../patch-my-pc-publisherv2/administration/updates/) tab.

![Manual Product Selection](/_images/image-(4160).png)

You can expand vendors to browse available products or use the [Search](../../../patch-my-pc-publisherv2/administration/updates/form-controls/search-products.md) form control to quickly locate a specific update by name.

Unlike the advice for [ConfigMgr application selection](../../../patch-my-pc-publisherv2/scenario-based-guidance/product-selection-and-discovery/scenario-1-configmgr-applications.md#manually-browse-and-select-products-directly-from-the-product-tree-on-the-configmgr-apps-tab), it is often appropriate to enable multiple update variants if they exist in your estate. For example, if both x86 and x64 variants are detected, publishing updates for both ensures all devices remain compliant while you work toward long term standardization.

As a best practice, begin by enabling a small number of familiar, low-impact applications to understand how ConfigMgr applications are created by the Publisher. Many customers start with widely used utilities such as 7-Zip or Notepad++ to gain confidence in the workflow.

### Standalone WSUS

In standalone WSUS environments, the Scan Wizard cannot be used because there is no ConfigMgr site database to query.

In this scenario, products must be enabled manually from the [product tree](../../../patch-my-pc-publisherv2/administration/updates/product-tree.md) on the [Updates tab](../../../patch-my-pc-publisherv2/administration/updates/).

You can expand vendors to browse available products or use the [Search](../../../patch-my-pc-publisherv2/administration/updates/form-controls/search-products.md) form control to quickly locate a specific update.

See [Manually browse and select products directly from the product tree on the Updates Apps tab](discover-configmgr-wsus-updates.md#manually-browse-and-select-products-directly-from-the-product-tree-on-the-updates-apps-tab) for advice on how to use the product tree to select updates manually for publishing.

## Inventory Variants and Update Selection

Scan results obtained by the Publisher from ConfigMgr hardware inventory may not always accurately reflect the exact installer variant deployed on a device. This is due to differences in how vendors name products in Add/Remove Programs and how that data is surfaced through ConfigMgr inventory views.

For example, inventory data may indicate that 7-Zip (x64) is installed, but it may not clearly distinguish whether the MSI or EXE variant was originally used. As a result, multiple update variants may appear as potential matches in the scan results.

To account for this ambiguity, consider one of the following approaches:

* **Enable all variants as Metadata Only first.**\
  This allows the Windows Update Agent on the device to evaluate applicability and report compliance back to ConfigMgr without downloading full update content. After reviewing compliance results, you can determine which specific variant(s) should be enabled with full content.
* **Enable all update variants as Full Content.**\
  In environments where multiple variants may exist and immediate patch coverage is the priority, enabling all update variants ensures that no installed instance remains unpatched when deployments are targeted.

![Enable multiple variants as full content or metadata only](/_images/image-(4159).png)

Using Metadata Only as an initial step is often the most controlled approach, particularly in WSUS standalone environments. It provides visibility into what is truly installed before introducing update binaries into WSUS.

For more information about about the metadata options when publishing updates, see [Publish with Full-content or Metadata Only](../../../patch-my-pc-publisherv2/customizations-right-click-options/publish-with-full-content-or-metadata-only.md).
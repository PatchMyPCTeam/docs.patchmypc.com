# Scan Intune in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Scan Intune for Supported Products** form control in Patch My PC (PMPC) Publisher requires access to your Intune tenant through Microsoft Graph. It inventories installed applications to determine which third-party products are present in your environment.

The scan results are compared against the Publisher catalog to identify supported products. This information helps you decide which products to enable on the Intune Apps or Intune Updates tab for deploying newer versions of applications and updates through Intune as Win32 apps.

![Scan Intune for Supported Products](../../../.gitbook/assets/image-\(4103\).png)

> \*\*Note\*\*
>
> The \*\*Scan Intune for Supported Products\*\* form control is shared between the Intune Apps and the Intune Updates tab and behaves identically in both locations. As a result, the form control on the Intune Apps tab can be used to configure and control auto-publishing behavior on the Intune Updates tab, and vice versa.
>
> While the form control itself is shared, manually selecting products in the query results only enables them on the tab from which the form was launched. For example, launching the scan wizard from the Intune Apps tab enables products for applications, whereas launching it from the Intune Updates tab enables products as updates.

> \*\*Tip\*\*
>
> This form control will use the Entra ID App Registration, configured from the \[Options]\(../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/) button, to connect to Microsoft Graph to retrieve data from the Intune Reporting Endpoint. For more details about the required API permissions and authentication options, see \[Entra ID App Registration]\(../../../patch-my-pc-publisherv2/publisher-requirements/intune-requirements/entra-id-app-registration/).

## Auto-Publishing Rules

Auto-publishing rules allow the Publisher to automatically enable products for publishing based on what is detected in your Intune environment, removing the need to manually review scan results and enabling a more hands-off approach to keeping third-party applications and updates current.

When these rules are enabled, the Publisher evaluates discovered application inventory data collected by the Intune Management Extension on managed devices, compares detected applications against the Patch My PC catalog, and automatically enables supported products that meet the configured device threshold.

![Auto-Publishing Rules](../../../.gitbook/assets/image-\(4084\).png)

Auto-publishing rules are evaluated during scheduled [**synchronizations**](../../../patch-my-pc-publisherv2/administration/sync-schedule.md). Each time a sync runs, the Publisher scans application inventory data from the AppInvRawData report, obtained from the Intune Reporting Endpoint, through the Microsoft Graph, and automatically enables any newly detected products that meet the configured thresholds.

This automation can be extremely powerful, but it’s important to configure it thoughtfully.

> \*\*Note\*\*
>
> Automatic enablement of products is based solely on configured device thresholds. Filters in this form only control what is displayed in the query results and do not influence which applications or updates are automatically enabled.

### Auto-enable products to be published as an update

When enabled, products detected in the inventory report obtained through Microsoft Graph are automatically enabled on the Intune Updates tab once they are found on at least the specified number of devices.

* The device count acts as a threshold to prevent enabling products seen only on a small number of machines
* Once enabled, updates for the product are published according to your existing sync and deployment processes

This option is commonly used to keep patching coverage up to date as new applications appear in the environment.

### Auto-enable products to be published as an application

When enabled, products detected in the inventory report obtained through Microsoft Graph are automatically enabled on the Intune Apps tab once they are found on at least the specified number of devices.

* This allows Patch My PC to automatically manage application creation for newly detected software
* The same device threshold concept applies to avoid enabling applications prematurely

This option is typically used in environments that want **application lifecycle management** to be driven directly from inventory data.

### Auto-enabled Products and Assignment Inheritance

When products are automatically enabled by auto-publishing rules based on the configured device threshold, any Intune assignments configured at the [All Products Level](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md#all-products-level) or [Vendor Level](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md#vendor-level) in the [product tree ](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md)are not inherited by newly enabled products. Newly detected products are enabled for publishing only and do not automatically receive existing assignment configurations.

Customers should review the publishing reports after each synchronization to identify products that were automatically enabled. After reviewing the report, configure the desired assignments directly on those products in the Publisher.

Alternatively, customers can use the [Manage Dynamic Assignments](../../../patch-my-pc-publisherv2/customizations-right-click-options/manage-dynamic-assignments.md) right-click customization option to automatically apply assignments to autopublished Intune updates. For more information, see [Auto-Enabled Products and Dynamic Assignments](scan-intune.md#auto-enabled-products-and-dynamic-assignments).

> \*\*Important\*\*
>
> Reapplying assignments at a higher level in the product tree to force inheritance on products enabled through auto-publishing rules is supported but should be used with caution. Reapplying assignments at the product or vendor level overwrites any assignments already configured on child products. This action can unintentionally replace specific assignment configurations that were intentionally set on individual products.

### Auto-Enabled Products and Dynamic Assignments

Customers can use the [Manage Dynamic Assignments](../../../patch-my-pc-publisherv2/customizations-right-click-options/manage-dynamic-assignments.md) right-click customization option, at the All Products level, for **Intune Updates** to automatically apply assignments to auto published updates. This provides a way to automate assignment behavior for newly enabled products.

Dynamic Assignments are evaluated only for products that are currently enabled in the Publisher product tree on the **Intune Updates** tab and only for the current version of a product at the time it is published. When Dynamic Assignments are used together with auto publishing rules, there is a timing consideration. During the first synchronization, auto publishing rules enable the product and publish the update. Because the product was not enabled at the start of the synchronization, Dynamic Assignment evaluation does not occur at that time.

A second synchronization is required for Dynamic Assignments to evaluate the newly enabled product and determine whether the update meets the configured criteria for assignment. This behavior is expected and should be considered when designing automation workflows that combine auto publishing rules with Dynamic Assignments.

> \*\*Note\*\*
>
> Assignments added using the Manage Dynamic Assignments feature do not persist indefinitely in the Publisher configuration. Dynamic Assignments are evaluated during each synchronization and applied only to updates that meet the configured criteria at that time.

## Device Threshold Best Practice

Patch My PC releases approximately 100 new applications per month, so it’s entirely possible for a scheduled scan to detect multiple new products. When low device thresholds are used, auto-publishing can enable these products very quickly, ensuring new additions don’t go unnoticed. However, this speed should be balanced with operational readiness, as downstream processes such as phased deployments and change control may not be prepared for a sudden influx of new applications and updates, particularly when assignments are broadly scoped.

> \*\*Important\*\*
>
> While it may be tempting to set the device threshold to a very low number, even 1, this is generally not recommended for most environments. This would be especially impactful for new customers who have not yet reviewed and enabled products in the product tree, as a very low threshold can cause newly discovered applications to be enabled simultaneously, potentially resulting in a large number of updates being synchronized at once.

A common and effective approach is:

1. Use the Scan Wizard to identify products currently installed in your environment
2. Enable the products from the scan wizard [query ](scan-intune.md#query)window or [product tree](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md) and [customize](../../../patch-my-pc-publisherv2/customizations-right-click-options/) those products from the product tree (conflicting processes, content options, etc.)
3. Enable auto-publishing rules to catch newly introduced applications over time

This allows you to remain in control initially, while still benefiting from automation going forward.

## Filters

The filters section lets you narrow the scan results shown in the list below, making it easier to review and manage products that may be later auto-enabled for publishing as updates.

* **Product**\
  Filter results by product name to focus on specific applications.
* **Vendor**\
  Filter results by software vendor.
* **Count**\
  Filter products based on how many devices they are detected on. This is useful when reviewing products that meet (or fall below) your auto-publishing device threshold.
* **Include / Exclude already enabled products**\
  Control whether products that are already enabled in the product tree are shown in the results. Excluding already enabled products helps you focus on newly discovered applications.

These filters do not affect detection or auto-publishing behavior directly, they only control what is displayed, helping you validate and review scan results before taking action.

![Available Filters](../../../.gitbook/assets/image-\(4085\).png)

## Query

The query button performs an interactive scan using the current configuration defined in the form and any filters that have been applied.

When clicked, the Publisher queries the obtained Intune report and displays the results in the list below. The products shown reflect:

* What applications detected in the Intune report matches products in the Patch My PC catalog.
* The device count for each product

> \*\*Note\*\*
>
> The device count value shown for each product matched is clickable. Selecting it displays a detailed view of the devices and application versions where the product was detected, allowing you to validate inventory results before enabling or publishing the product.

The Query button does not enable or publish products by itself, it simply retrieves and displays the results based on the current settings, allowing you to review and validate findings before taking further action.

![Query Results](../../../.gitbook/assets/image-\(4086\).png)

Selecting products from this list is equivalent to manually selecting the same products in the [product tree](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md) either on the Intune Apps tab or Intune Updates tab. When you check a product here, it enables that product for publishing in the same way as selecting it directly in the product tree.

> \*\*Important\*\*
>
> Because there is no universal standard for how vendors name applications, inventory results cannot always distinguish between multiple variants of the same product. For example, if 7-Zip (x64) is detected in the Intune report, Publisher cannot reliably determine whether the MSI or EXE installer was originally used, so both variants may be shown as matches. This ensures coverage while acknowledging the limitations of vendor-provided inventory data.

### Count

The Count value shown for each matched product is clickable. Selecting the count opens a detailed view that lists the devices where the product was detected, along with the reported application version on each device.

![Clicking device count value](../../../.gitbook/assets/image-\(4151\).png)

This detailed view allows you to review inventory results and verify product presence and version distribution before enabling or publishing the product.

Clicking Export CSV will generated CSV file includes the following columns:

* **Device Name**\
  The name of the device where the product was detected.
* **Product Name**\
  The application name as reported in inventory.
* **Product Version**\
  The version of the application detected on the device.

## Export to CSV

The **Export to CSV** form control is used to export the results displayed in the query window to a comma separated values file for offline review or reporting.

![Export to CSV](../../../.gitbook/assets/image-\(4152\).png)

This control is disabled when no query results are present in the window. After a query is selected and results are displayed, the control becomes available.

To export the results to a CSV:

1. Run a query so that results are displayed in the window and click **Export to CSV**.
2. When prompted, choose **Yes** to export only products that match the current filter or choose **No** to export the full unfiltered results.

![Filter Export Option](../../../.gitbook/assets/image-\(4153\).png)

3. Select the save location, enter a file name if required.

![Choose a save location](../../../.gitbook/assets/image-\(4154\).png)

4. Click **Save** to complete the export.

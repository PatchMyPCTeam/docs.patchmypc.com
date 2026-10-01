# Filters and Discovered Products sections of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **FILTERS** and **DISCOVERED APPS** sections on the **Scan ConfigMgr** tab of Patch My PC (PMPC) Publisher defines how Publisher connects to Microsoft Configuration Manager (ConfigMgr) and where it stores application source content.

## Filters

The _Filters_ section lets you narrow the scan results shown in the list below, making it easier to review and manage products that may be later auto-enabled for publishing as updates.

<figure><img src="../../../../.gitbook/assets/image (1115).png" alt="Filters" width="563"><figcaption></figcaption></figure>

The available filters are:

* **Product-** Filter results by product name to focus on specific applications.
* **Vendor -** Filter results by software vendor.
* **Count -** Filter products based on how many devices they are detected on. This is useful when reviewing products that meet (or fall below) your auto-publishing device threshold.
* **Include/Exclude already enabled products -** Controls whether products already enabled in the Product Tree are shown in the results. Excluding already enabled products helps you focus on newly discovered applications.
* **Languages -** Filters results by the application's language.

{% hint style="info" %}
**Note**

These filters do not affect detection or auto-publishing behavior directly; they only control what is displayed, helping you validate and review scan results before taking action.
{% endhint %}

## Query button

The _Query_ button performs an interactive scan using the current configuration defined in the form, including SQL connection settings, collection scoping, and any filters that have been applied.

<figure><img src="../../../../.gitbook/assets/image (1122).png" alt="&#x27;Query&#x27; button" width="563"><figcaption></figcaption></figure>

When you click the **Query** button, Publisher queries the ConfigMgr site database and displays the results in the list below. The products shown reflect:

* What applications detected in the ConfigMgr HINV match products in the Patch My PC catalog.
* The device count for each product.

<figure><img src="../../../../.gitbook/assets/image (1127).png" alt="Query results" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The **Query** button does not enable or publish products by itself; it simply retrieves and displays the results based on the current settings, allowing you to review and validate findings before taking further action.
{% endhint %}

Checking the checkbox beside products in this list to select them is equivalent to manually selecting the same products in the [Product Tree](../../../fundamentals/product-tree/working.md) on the **ConfigMgr Apps** tab. Selecting a product here enables it for publishing in the same way as selecting it directly in the Product Tree.

{% hint style="danger" %}
**Important**

As there is no universal standard for how vendors name applications, inventory results cannot always distinguish between multiple variants of the same product. For example, if 7-Zip (x64) is detected in the ConfigMgr HINV, Publisher cannot reliably determine whether the MSI or EXE installer was originally used, so both variants may be shown as matches. This ensures coverage while acknowledging the limitations of vendor-provided inventory data.
{% endhint %}

### Count column

Clicking the **Count** value beside a product opens the **Devices with Application** window, which shows a detailed view that lists the devices where the product was detected, along with the reported application version on each device.

<figure><img src="../../../../.gitbook/assets/image (1128).png" alt="&#x27;Devices with Application&#x27; window" width="450"><figcaption></figcaption></figure>

This detailed view allows you to review inventory results and verify product presence and version distribution before enabling or publishing the product.

Clicking **Export CSV** on the **Devices with Application** window generates a CSV file that includes the following columns:

* **Device Name -** The name of the device where the product was detected.
* **Product Name -** The application name as reported in inventory.
* **Product Version -** The version of the application detected on the device.
* **Discovery Source -** The ConfigMgr inventory view used to detect the application. For example, `v_GS_ADD_REMOVE_PROGRAMS_64`.

## Export to CSV button&#x20;

Clicking the **Export to CSV** button allows you to export the results from the **Scan ConfigMgr** window to a CSV file.

<figure><img src="../../../../.gitbook/assets/image (1129).png" alt="&#x27;Export to CSV&#x27; button" width="563"><figcaption></figcaption></figure>

### To export the results to a CSV

1. Load Publisher.
2. Navigate to the **ConfigMgr Apps | Scan ConfigMgr** tab.
3. Run a [query](filters-discovered-products.md#query-button) so that results are displayed in the window.
4. Click **Export to CSV...**
5. On the **Export** dialog, click the relevant option for the products you want to export.

<figure><img src="../../../../.gitbook/assets/image (1130).png" alt="&#x27;Export&#x27; dialog" width="306"><figcaption></figcaption></figure>

6. Browse to the relevant location where you want to save the export file, change the filename if required, then click **Save**.

<figure><img src="../../../../.gitbook/assets/image (4134).png" alt="Select the save location" width="563"><figcaption></figcaption></figure>

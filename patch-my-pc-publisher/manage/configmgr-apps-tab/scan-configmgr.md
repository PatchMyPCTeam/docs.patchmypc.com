# Scan ConfigMgr in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Scan ConfigMgr** tab of Patch My PC (PMPC) Publisher requires access to your ConfigMgr site database to inventory installed applications via a Hardware Inventory Collection (HINV) to determine which third-party products are present in your environment.

The scan results are then compared against the PMPC catalog to identify matches, helping you make informed decisions about which products to enable on the **ConfigMgr Apps** tab for deploying newer versions of those applications through Software Center, task sequences, or manual deployments.

{% hint style="info" %}
**Note**

The **Scan ConfigMgr** tab is shared with the tab of the same name under the **WSUS Updates** tab and behaves identically in both locations. As a result, you can use the **Scan ConfigMgr** tab under the **ConfigMgr Apps** tab to configure and control auto-publishing behavior on the **WSUS Updates** tab, and vice versa.

Although the tab is shared, manually selecting products in the [query](scan-configmgr.md#query-button) results enables them only on the tab from which **Scan ConfigMgr** was launched. For example, launching the scan wizard from the **WSUS Updates** tab enables products for updates, whereas launching it from the **ConfigMgr Apps** tab enables products as applications.
{% endhint %}

## SQL Configuration

### Site Database Server

To configure the scan, Publisher needs the site database server name and database name used by ConfigMgr. You can find this information in the ConfigMgr console by navigating to:

**Monitoring | System Status | Site Status**

<figure><img src="../../../.gitbook/assets/image (1096).png" alt="Monitoring | System Status | Site Status" width="563"><figcaption></figcaption></figure>

Select the **Site database server** site system role. The details shown here provide the correct values to enter into Publisher.

<figure><img src="../../../.gitbook/assets/image (1100).png" alt="Site Database Server" width="563"><figcaption></figcaption></figure>

By default, no **Limiting Collection** is specified. When you leave this field empty, the scan for supported products runs against **All Systems**.

Optionally, you can limit the scan scope by selecting a specific device collection using the browse button.

{% hint style="info" %}
**Note**

When you select a device collection, only the hardware inventory (HINV) data for devices in that collection is evaluated. This can significantly reduce scan time in large environments or when you want to validate a specific subset of devices rather than scanning the entire estate.
{% endhint %}

### Connect to ConfigMgr SQL Database As

The **Scan ConfigMgr** tab runs direct SQL queries against your ConfigMgr site database to inventory installed software. This scan _does not_ use the SMS Provider, so the account performing the scan must have the appropriate SQL permissions on the ConfigMgr database.

<figure><img src="../../../.gitbook/assets/image (1099).png" alt="Connect to ConfigMgr SQL Database As" width="563"><figcaption></figcaption></figure>

Publisher supports multiple ways to authenticate to SQL, allowing flexibility depending on where Publisher is installed and which account has the required permissions.

### **As Windows service account**

The **As Windows service account** option (the default) uses the account under which the Publisher service is running. By default, the Publisher service runs as SYSTEM. This option is recommended:

* When Publisher is installed on the site server.
* Windows authentication is used.
* No credentials need to be entered.

{% hint style="info" %}
**Note**

When Publisher is installed on the ConfigMgr site server, the **SYSTEM** account typically already has the required read permissions on the ConfigMgr database views. In most environments, you don't need additional SQL configuration.
{% endhint %}

### **With these credentials using SQL authentication**

The **With these credentials using SQL authentication** option allows you to specify a SQL login and password. This option is recommended:

* You use SQL authentication instead of Windows authentication.
* If you want to use a SQL login (which needs read access to the required ConfigMgr database views).

This option is less common and generally not recommended unless Windows authentication cannot be used.

### **Run interactive scan as logged in user**

When the **Run interactive scan as logged in user** checkbox is checked, the scan runs using the currently logged-in user’s Windows credentials instead of Publisher's service account. This option is recommended:

* For troubleshooting permission issues
* Can be helpful when testing access before granting permissions to the service account

This option requires the logged-in user to have the necessary SQL SELECT permissions on the required ConfigMgr views.

{% hint style="danger" %}
**Important**

This option does not change how scheduled scans run; it only applies to the interactive scan being executed.
{% endhint %}

{% hint style="info" %}
**Note**

See [Microsoft SQL Permission Requirements](../../requirements/configmgr-requirements/permissions.md#microsoft-sql-permission-requirements) for more information.
{% endhint %}

## Auto-Publishing Rules

_Auto-publishing rules_ allow Publisher to automatically enable products for publishing based on what is detected in your ConfigMgr environment, removing the need to manually review scan results and enabling a more hands-off approach to keeping third-party updates current.

<figure><img src="../../../.gitbook/assets/image (1113).png" alt="Auto-Publishing Rules" width="563"><figcaption></figcaption></figure>

When these rules are enabled, Publisher evaluates application inventory data collected by ConfigMgr, compares detected applications against the PMPC catalog, and automatically enables supported products that meet the configured device threshold.

{% hint style="danger" %}
**Important**

These rules rely on the same ConfigMgr database access and SQL permissions described earlier in this document under [Database Authentication](scan-configmgr.md#database-authentication).
{% endhint %}

Auto-publishing rules are evaluated during scheduled [synchronizations](../sync-schedule-tab/). Each time a sync runs, Publisher scans application inventory data from ConfigMgr and automatically enables any newly detected products that meet the configured thresholds.

This automation can be extremely powerful, but it’s important to configure it thoughtfully.

### Auto-enable products to be published as an update if installed on at least _x_ devices

When the **Auto-enable products to be published as an update if installed on at least&#x20;**_**x**_**&#x20;devices** checkbox is checked, products detected in ConfigMgr inventory are automatically enabled on the **WSUS Updates** tab once they are found on at least the specified number of devices.

* The device count acts as a threshold to prevent enabling products seen only on a small number of devices.
* Once enabled, updates for the product are published according to your existing sync and deployment processes.

This option is commonly used to keep patching coverage up to date as new applications appear in the environment.

#### Auto-enable products as "**Metadata Only"** if found, but threshold is not met

Checking the **Auto-enable products as "Metadata Only" if found, but threshold is not met** checkbox works with [Auto-enable products to be published as an update](scan-configmgr.md#auto-enable-products-to-be-published-as-an-update).

When checked:

* Products detected below the configured device threshold are enabled as Metadata Only.
* No update content is downloaded or stored in WSUS.
* WSUS can still evaluate applicability and compliance for those products.

This is particularly useful for **early visibility** of newly discovered or low-prevalence applications without immediately introducing update content into the environment.

### Auto-enable products to be published as an application if installed on at least _x_ devices

Checking the **Auto-enable products to be published as an application if installed on at least&#x20;**_**x**_**&#x20;devices** checkbox automatically enables products detected in ConfigMgr inventory on the [ConfigMgr Apps](./) tab once they are found on at least the specified number of devices.

When checked:

* Publisher can automatically manage application creation for newly detected software.
* The same device threshold concept applies to avoid enabling applications prematurely.

This option is typically used in environments that want application lifecycle management to be driven directly from inventory data.

### Device Threshold Best Practice

Patch My PC releases about 100 new applications per month, so it’s entirely possible for a scheduled scan to detect multiple new products. When low device thresholds are used, auto-publishing can enable these products very quickly, ensuring new additions don’t go unnoticed. However, this speed should be balanced with operational readiness, as downstream processes such as Automatic Deployment Rules (ADRs), testing, and change control may not be prepared for a sudden influx of updates, particularly when ADRs are broadly scoped and evaluate new content with little or no delay.

{% hint style="danger" %}
**Important**

Whilst it may be tempting to set the device threshold to a very low number (even **1**), this is generally not recommended for most environments. This would be especially impactful for new customers who have not yet reviewed and enabled products in the Product Tree, as a very low threshold can cause newly discovered applications to be enabled simultaneously, potentially resulting in a large number of updates being synchronized at once.
{% endhint %}

A common and effective approach is:

1. Use **Scan ConfigMgr** to identify products currently installed in your environment.
2. Enable these products from the [scan wizard query window](scan-configmgr.md#query) or [Product Tree](../../fundamentals/product-tree/working.md), and [customize](../../customizations/) those products from the Product Tree (conflicting processes, content options, etc.).
3. Enable auto-publishing rules to catch newly introduced applications over time

This lets you stay in control initially while still benefiting from automation going forward.

## Filters

The filters section lets you narrow the scan results shown in the list below, making it easier to review and manage products that may be later auto-enabled for publishing as updates.

<figure><img src="../../../.gitbook/assets/image (1115).png" alt="Filters" width="563"><figcaption></figcaption></figure>

The available filters are:

* **Product-** Filter results by product name to focus on specific applications.
* **Vendor -** Filter results by software vendor.
* **Count -** Filter products based on how many devices they are detected on. This is useful when reviewing products that meet (or fall below) your auto-publishing device threshold.
* **Include / Exclude already enabled products -** Controls whether products already enabled in the Product Tree are shown in the results. Excluding already enabled products helps you focus on newly discovered applications.
* **Languages -** Filters results by the application's language.

{% hint style="info" %}
**Note**

These filters do not affect detection or auto-publishing behavior directly; they only control what is displayed, helping you validate and review scan results before taking action.
{% endhint %}

## Query button

The **Query** button performs an interactive scan using the current configuration defined in the form, including SQL connection settings, collection scoping, and any filters that have been applied.

<figure><img src="../../../.gitbook/assets/image (1122).png" alt="&#x27;Query&#x27; button" width="563"><figcaption></figcaption></figure>

When you click the **Query** button, Publisher queries the ConfigMgr site database and displays the results in the list below. The products shown reflect:

* What applications detected in the ConfigMgr HINV match products in the Patch My PC catalog.
* The device count for each product.

<figure><img src="../../../.gitbook/assets/image (1127).png" alt="Query results" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The **Query** button does not enable or publish products by itself; it simply retrieves and displays the results based on the current settings, allowing you to review and validate findings before taking further action.
{% endhint %}

Checking the checkbox beside products in this list to select them is equivalent to manually selecting the same products in the [Product Tree](../../fundamentals/product-tree/working.md) on the **ConfigMgr Apps** tab. Selecting a product here enables it for publishing in the same way as selecting it directly in the Product Tree.

{% hint style="danger" %}
**Important**

As there is no universal standard for how vendors name applications, inventory results cannot always distinguish between multiple variants of the same product. For example, if 7-Zip (x64) is detected in the ConfigMgr HINV, Publisher cannot reliably determine whether the MSI or EXE installer was originally used, so both variants may be shown as matches. This ensures coverage while acknowledging the limitations of vendor-provided inventory data.
{% endhint %}

### Count column

Clicking the **Count** value beside a product opens the **Devices with Application** window, which shows a detailed view that lists the devices where the product was detected, along with the reported application version on each device.

<figure><img src="../../../.gitbook/assets/image (1128).png" alt="&#x27;Devices with Application&#x27; window" width="450"><figcaption></figcaption></figure>

This detailed view allows you to review inventory results and verify product presence and version distribution before enabling or publishing the product.

Clicking **Export CSV** on the **Devices with Application** window generates a CSV file that includes the following columns:

* **Device Name -** The name of the device where the product was detected.
* **Product Name -** The application name as reported in inventory.
* **Product Version -** The version of the application detected on the device.
* **Discovery Source -** The ConfigMgr inventory view used to detect the application. For example, `v_GS_ADD_REMOVE_PROGRAMS_64`.

## Export to CSV button&#x20;

Clicking the **Export to CSV** button allows you to export the results from the **Scan ConfigMgr** window to a CSV file.

<figure><img src="../../../.gitbook/assets/image (1129).png" alt="&#x27;Export to CSV&#x27; button" width="563"><figcaption></figcaption></figure>

### To export the results to a CSV

1. Load Publisher.
2. Navigate to the **ConfigMgr Apps | Scan ConfigMgr** tab.
3. Run a [query](scan-configmgr.md#query) so that results are displayed in the window.
4. Click **Export to CSV...**
5. On the **Export** dialog, click the relevant option for the products you want to export.

<figure><img src="../../../.gitbook/assets/image (1130).png" alt="&#x27;Export&#x27; dialog" width="306"><figcaption></figcaption></figure>

6. Browse to the relevant location where you want to save the export file, and if required, change the filename,then click **Save**.

<figure><img src="../../../.gitbook/assets/image (4134).png" alt="Select the save location" width="563"><figcaption></figcaption></figure>

# Scan ConfigMgr Database for Supported Products

_Applies to: Patch My PC Publisher V2.x_

## ![](/_images/image-(449).png>) Overview

The **Scan ConfigMgr Database for Supported Products** form control requires access to your ConfigMgr site database to inventory installed applications, via a Hardware Inventory Collection (HINV) and determine which third-party products are present in your environment. The scan results are then compared against the Patch My PC catalog to identify matches, helping you make informed decisions about which products to enable on the **ConfigMgr Apps** tab for deploying newer versions of those applications through Software Center, task sequences, or manual deployments.

![Scan ConfigMgr Database for Supported Products](/_images/image-(4095).png "Scan ConfigMgr Database for Supported Products")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The **Scan ConfigMgr Database for Supported Products** form control is shared with the same form control available on the Updates tab and behaves identically in both locations. As a result, the form control on the ConfigMgr Apps tab can be used to configure and control auto-publishing behavior on the ConfigMgr Apps tab, and vice versa.</p>
<p>While the form control itself is shared, manually selecting products in the [query](scan-configmgr-database-for-supported-products.md#query) results only enables them on the tab from which the form was launched. For example, launching the scan wizard from the Updates tab enables products for updates, whereas launching it from the ConfigMgr Apps tab enables products as applications.</p>
</blockquote>

## SQL Configuration

### Site Database Server

To configure the scan, the Publisher needs the site database server name and database name used by ConfigMgr. You can find this information in the ConfigMgr console by navigating to:

Administration > Monitoring > System Status > Site Status

![](/_images/image-(451).png)

Select the Site Database Server site system role. The details shown here provide the correct values to enter into Publisher.

![SQL Configuration](/_images/image-(4098).png "SQL Configuration")

By default, no device collection is specified. When this field is left empty, the scan for supported products runs against **All Systems**.

Optionally, you can limit the scan scope by selecting a specific **device collection** using the browse button.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>When a device collection is selected, only the **hardware inventory (HINV)** data for devices within that collection is evaluated. This can significantly reduce scan time in large environments or when you want to validate a specific subset of devices rather than scanning the entire estate.</p>
</blockquote>

### Database Authentication

The **Scan ConfigMgr Database for Supported Products** form control runs direct SQL queries against your ConfigMgr site database to inventory installed software. This scan _does not_ use the SMS Provider, so the account performing the scan must have the appropriate SQL permissions on the ConfigMgr database.

![SQL Database Authentication](/_images/image-(4099).png "SQL Database Authentication")

The Publisher supports multiple ways to authenticate to SQL, allowing flexibility depending on where Publisher is installed and which account has the required permissions.

### Connect to ConfigMgr SQL Database As

#### **As Windows service account (Default)**

This option uses the account under which the Publisher service is running. By default, the Publisher service runs as SYSTEM.

* Recommended when the Publisher is installed on the site server.
* Uses Windows authentication.
* No credentials need to be entered.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>When the Publisher is installed on the ConfigMgr site server, the **SYSTEM** account typically already has the required read permissions on the ConfigMgr database views. In most environments, no additional SQL configuration is required.</p>
</blockquote>

#### **With these credentials using SQL authentication**

This option allows you to specify a **SQL login and password**.

* Uses SQL authentication instead of Windows authentication.
* Requires a SQL login with read access to the required ConfigMgr database views.
* Less common and generally not recommended unless Windows authentication cannot be used.

#### **Run interactive scan as logged in user**

When enabled, the scan runs using the currently logged-in user’s Windows credentials instead of the Publisher service account.

* Useful for troubleshooting permission issues
* Helpful when testing access before granting permissions to the service account
* Requires the logged-in user to have the necessary SQL SELECT permissions on the required ConfigMgr views.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This option does not change how scheduled scans run, it only applies to the interactive scan being executed.</p>
</blockquote>

### SQL Permissions Required

When the Publisher is installed on the ConfigMgr site server, the Publisher service runs as SYSTEM and the site server’s computer account typically already has the required read permissions on the ConfigMgr site database. In this configuration, no additional SQL permissions are usually required.

If Publisher is installed on a different server, or if you choose to run the scan using a specific SQL or user account, the account used for the scan must be granted read access to the ConfigMgr database views used for application inventory.

To successfully scan the site database, the account needs **SELECT** permissions on the following SQL views in your ConfigMgr database:

* `v_Add_Remove_Programs`
* `v_GS_ADD_REMOVE_PROGRAMS`
* `v_GS_ADD_REMOVE_PROGRAMS_64`
* `v_GS_INSTALLED_SOFTWARE`

To drill into an application count and view the devices on which the selected application is installed, grant **Select** permission on:

* `v_R_System`

If collection filtering is used, also grant **Select** permission on:

* `v_FullCollectionMembership`
* `v_Collection`

These views contain the hardware inventory and collection membership data that the Publisher uses to determine which software is installed on which devices.

### Manually Add SQL Permissions

To grant access, add the computer account (for example, DOMAIN\PUBLISHER01$) or the user/SQL account as a login in SQL Server, map it to the ConfigMgr site database, and grant SELECT permissions on the required inventory and collection views. This ensures the Publisher can successfully query installed application data during the scan.

If the required SQL permissions are not already in place, one option is to provide the following SQL query to your SQL administrator to run against the ConfigMgr site database.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Before running this script, update the **database name** specified in the `USE` statement and replace the account value assigned to the `@UserName` variable with the appropriate computer or user account for your environment.</p>
</blockquote>

```sql
-- Replace CM_LA2 with the database name for your Configuration Manager environment
USE CM_LA2
GO

-- Replace CONTOSO\ServerName$ with the appropriate value for your environment
DECLARE @UserName nvarchar(128) = 'CONTOSO\ServerName$'
DECLARE @QuotedUserToGrant nvarchar(128) = QUOTENAME(@UserName)

IF NOT EXISTS(SELECT principal_id FROM sys.server_principals WHERE name = @UserName) BEGIN
 DECLARE @LoginSQL as varchar(500)
 SET @LoginSQL = 'CREATE LOGIN '+ @QuotedUserToGrant + ' FROM WINDOWS'
 EXEC (@LoginSQL)
END

IF NOT EXISTS(SELECT principal_id FROM sys.database_principals WHERE name = @UserName) BEGIN
 DECLARE @UserSQL as varchar(500)
 SET @UserSQL = 'CREATE USER ' + @QuotedUserToGrant + ' FOR LOGIN ' + @QuotedUserToGrant
 EXEC (@UserSQL)
END

DECLARE @PermissionsSQL as varchar(500)
SET @PermissionsSQL = 'GRANT SELECT ON dbo.v_Add_Remove_Programs TO ' + @QuotedUserToGrant +
'GRANT SELECT ON dbo.v_GS_ADD_REMOVE_PROGRAMS TO ' + @QuotedUserToGrant +
'GRANT SELECT ON dbo.v_GS_ADD_REMOVE_PROGRAMS_64 TO ' + @QuotedUserToGrant +
'GRANT SELECT ON dbo.v_GS_INSTALLED_SOFTWARE TO ' + @QuotedUserToGrant +
'GRANT SELECT ON dbo.v_R_System TO ' + @QuotedUserToGrant +
'GRANT SELECT ON dbo.v_FullCollectionMembership TO ' + @QuotedUserToGrant +
'GRANT SELECT ON dbo.v_Collection TO ' + @QuotedUserToGrant
EXEC (@PermissionsSQL)
```

Alternatively, you can manually assign the required permissions using SQL Server Management Studio:

1. Launch SQL Server Management Studio.
2. Connect to the SQL Server hosting the ConfigMgr site database.
3. Authenticate using an account with permissions to manage logins and database security.

![Authenticate and Connect to via SSMS](/_images/image-(454).png "Authenticate and Connect to via SSMS")

4. In **Object Explorer**, expand **Security > Logins**.
5. Check whether the login already exists:
   * **Windows computer account:** `DOMAIN\PUBLISHER01$`
   * **Windows user account:** `DOMAIN\UserName`
   * **SQL login:** (as provided by your DBA)
6. If the login already exists, reuse it and continue to step 9.
7. If the login does **not** exist:
   * Right-click **Logins** and select **New Login…**
   * For Windows accounts, click **Search…** and select the account
   * For SQL logins, choose **SQL Server authentication** and enter the credentials
8. Click **OK** to create the login.
9. Right-click the newly created (or existing) login and select **Properties**.
10. Select **User Mapping**.
11. Check whether the login is already mapped to your ConfigMgr site database (for example, `CM_LA2`).
12. If the database is **already selected**, continue to step 16.
13. If it is **not selected**, check the box next to the site database to create the mapping.
14. In the **database role membership** section, leave all roles **unchecked** (no database roles are required).
15. Click **OK** to save the changes.

![User Mapping](/_images/image-(455).png "User Mapping")

16. Expand **Databases > CM\_\<SiteCode> > Views**
17. For each required view:
    * Right-click the view
    * Select **Properties**
    * Go to **Permissions**
    * Add the login if not already listed
    * Grant **SELECT** permission
      * **Required views:**
        * `v_Add_Remove_Programs`
        * `v_GS_ADD_REMOVE_PROGRAMS`
        * `v_GS_ADD_REMOVE_PROGRAMS_64`
        * `v_GS_INSTALLED_SOFTWARE`
      * **Additional views (only if limiting scans to a collection):**
        * `v_FullCollectionMembership`
        * `v_Collection`
18. Click **OK** to save permissions.

The example below shows how SELECT permission is granted on the v\_Add\_Remove\_Programs view using SQL Server Management Studio.

In this case, the account LAB2\Administrator has been added to the view’s Permissions page. With the account selected, the SELECT permission is explicitly granted, allowing the Publisher to read data from this view during the scan.

![SQL Select Permission](/_images/image-(456).png "SQL Select Permission")

## Auto-Publishing Rules

Auto-publishing rules allow the Publisher to automatically enable products for publishing based on what is detected in your ConfigMgr environment, removing the need to manually review scan results and enabling a more hands-off approach to keeping third-party updates current. When these rules are enabled, the Publisher evaluates application inventory data collected by ConfigMgr, compares detected applications against the Patch My PC catalog, and automatically enables supported products that meet the configured device threshold.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>These rules rely on the same ConfigMgr database access and SQL permissions described earlier in this document under [Database Authentication](scan-configmgr-database-for-supported-products.md#database-authentication).</p>
</blockquote>

![Auto-Publishing Rules](/_images/image-(4100).png "Auto-Publishing Rules")

Auto-publishing rules are evaluated during scheduled [**synchronizations**](../../sync-schedule.md). Each time a sync runs, the Publisher scans application inventory data from ConfigMgr and automatically enables any newly detected products that meet the configured thresholds.

This automation can be extremely powerful, but it’s important to configure it thoughtfully.

### Auto-enable products to be published as an update

When enabled, products detected in ConfigMgr inventory are automatically enabled on the Updates tab once they are found on at least the specified number of devices.

* The device count acts as a threshold to prevent enabling products seen only on a small number of machines
* Once enabled, updates for the product are published according to your existing sync and deployment processes

This option is commonly used to keep patching coverage up to date as new applications appear in the environment.

### Auto-enable products as **Metadata Only** if found, but threshold is not met

This option works in conjunction with [Auto-enable products to be published as an update](scan-configmgr-database-for-supported-products.md#auto-enable-products-to-be-published-as-an-update).

When enabled:

* Products detected below the configured device threshold are enabled as Metadata Only
* No update content is downloaded or stored in WSUS
* WSUS can still evaluate applicability and compliance for those products

This is particularly useful for **early visibility** of newly discovered or low-prevalence applications without immediately introducing update content into the environment.

### Auto-enable products to be published as an application

When enabled, products detected in ConfigMgr inventory are automatically enabled on the [ConfigMgr Apps](../) tab once they are found on at least the specified number of devices.

* This allows Patch My PC to automatically manage application creation for newly detected software
* The same device threshold concept applies to avoid enabling applications prematurely

This option is typically used in environments that want **application lifecycle management** to be driven directly from inventory data.

### Device Threshold Best Practice

Patch My PC releases approximately 100 new applications per month, so it’s entirely possible for a scheduled scan to detect multiple new products. When low device thresholds are used, auto-publishing can enable these products very quickly, ensuring new additions don’t go unnoticed. However, this speed should be balanced with operational readiness, as downstream processes such as Automatic Deployment Rules (ADRs), testing, and change control may not be prepared for a sudden influx of updates, particularly when ADRs are broadly scoped and evaluate new content with little or no delay.

<blockquote class="wp-block-quote">
<p>**Caution**</p>
<p>While it may be tempting to set the device threshold to a very low number, even 1, this is generally not recommended for most environments. This would be especially impactful for new customers who have not yet reviewed and enabled products in the product tree, as a very low threshold can cause newly discovered applications to be enabled simultaneously, potentially resulting in a large number of updates being synchronized at once.</p>
</blockquote>

A common and effective approach is:

1. Use the Scan Wizard to identify products currently installed in your environment
2. Enable thes producs from the [scan wizard query window](scan-configmgr-database-for-supported-products.md#query) or [product tree](../product-tree.md) and [customize](../../../customizations-right-click-options/) those products from the product tree (conflicting processes, content options, etc.)
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

![Available Filters](/_images/image-(4101).png "Available Filters")

## Query

The query button performs an interactive scan using the current configuration defined in the form, including SQL connection settings, collection scoping and any filters that have been applied.

When clicked, the Publisher queries the ConfigMgr site database and displays the results in the list below. The products shown reflect:

* What applications detected in the ConfigMgr HINV matches products in the Patch My PC catalog.
* The device count for each product

The Query button does not enable or publish products by itself, it simply retrieves and displays the results based on the current settings, allowing you to review and validate findings before taking further action.

![Query Results](/_images/image-(4102).png "Query Results")

Selecting products from this list is equivalent to manually selecting the same products in the [product tree](../product-tree.md) on the [ConfigMgr Apps](../) tab. When you check a product here, it enables that product for publishing in the same way as selecting it directly in the product tree.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Because there is no universal standard for how vendors name applications, inventory results cannot always distinguish between multiple variants of the same product. For example, if 7-Zip (x64) is detected in the ConfigMgr HINV, Publisher cannot reliably determine whether the MSI or EXE installer was originally used, so both variants may be shown as matches. This ensures coverage while acknowledging the limitations of vendor-provided inventory data.</p>
</blockquote>

### Count

The **Count** value shown for each matched product is clickable. Selecting the count opens a detailed view that lists the devices where the product was detected, along with the reported application version on each device.

![Clicking device count value](/_images/image-(4135).png "Clicking device count value")

This detailed view allows you to review inventory results and verify product presence and version distribution before enabling or publishing the product.&#x20;

Clicking **Export CSV** will generated CSV file includes the following columns:

* **Device Name**\
  The name of the device where the product was detected.
* **Product Name**\
  The application name as reported in inventory.
* **Product Version**\
  The version of the application detected on the device.
* **Discovery Source**\
  The ConfigMgr inventory view used to detect the application. For example, `v_GS_ADD_REMOVE_PROGRAMS_64`.

## Export CSV

The **Export to CSV** button allows you to export the results from the Scan ConfigMgr Database for Supported Products window to a CSV file.

![Export CSV](/_images/image-(4132).png "Export CSV")

To export the results to a CSV:

1. Run a [query](scan-configmgr-database-for-supported-products.md#query) so that results are displayed in the window and click Export to CSV.
2. When prompted, click **Yes** to export only products that match the current filter or click **No** to export the full unfiltered results.

![Apply filter to expoerted data prompt](/_images/image-(4133).png "Apply filter to expoerted data prompt")

3. Select the save location and enter a different file name if required,&#x20;

![Select the save location](/_images/image-(4134).png "Select the save location")

3. Save to complete the export.
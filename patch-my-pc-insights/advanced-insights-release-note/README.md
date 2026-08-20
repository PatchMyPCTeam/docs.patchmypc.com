# Release notes for Patch My PC Advanced Insights

_Applies to: Patch My PC Advanced Insights_

Details the production release history for Patch My PC's Advanced Insights, the most recent release being shown first.

### 2.6.5 - 2026-07-27

**New Features:**

* Replaced 22H2 with 25H2 in all Windows 11 readiness tables as 22H2 is now out of support. Reordered to show latest windows build first for the dropdown version selector.
* Added "Progress Description" and "Secure Version Number" to Secureboot tables

**Bug Fixes:**

* Entra setting saving fixed and added warning message about not saving any info unless all three settings are provided.
* Fixed decimal overflow for large download sizes for Downloaded content

**Misc:**

* Logs are now formatted in CMTrace format
* Updated .net runtime to 8.0.29

### 2.6.4 - 2026-07-09

**Bug Fixes:**

* Fixed regression in RBAC handling for users with no RBAC roles set.

### 2.6.3 - 2026-07-08

**New Features:**

* Add debug export for simpler log collector output

**Bugs Fixes:**

* Fix Current Branch version dashstat not working with latest version
* Fix Incorrect dashboard guide link from Printers Dashboard
* Fix dashstat items not storing saved title in custom dashboards
* Fix cancellation tokens not cancelling SQL Queries
* Fix issue where export data on some tables caused duplicate downloads

**Misc Changes:**

* Updated .net version to 8.0.28
* New log collector queries to return tempdb setup & query execution statistics

### 2.6.2 - 2026-06-10

**New Features:**

* Documentation links have been added to the config section of each warranty provider.

**Bug Fixes:**

* Updating configmanager inventory classes via Advanced Insights now correctly adds the PMPC\_Printers class.
* Data collections counts for the PMPC\_Printers class now show accurate counts instead of showing that no data has been collected.

### 2.6.1 - 2026-06-08

**New Features:**

* Add new Printers Dashboard under Hardware Node
  * Shows Installed local and network printers
  * Adds new tab to device modal which shows connected printers
* Add MSI Health to Software > Client Inventory Dashboard
  * Shows installed applications with missing MSI source path
* Add PrimaryDevices to Users table showing number of assigned devices

**Misc Changes:**

* Updated .net version to 8.0.27

### 2.5.6 - 2026-05-05

**New Features:**

* Secure Boot Dashboard Updates - Firmware Dashboard item showing models requiring firmware updates and more drill through data for enhanced data visibility.
  * N.B. This dashboard requires v 2.2.0 of the Inventory Extensions which was released 23rd March. You may need to click to update the inventory schema or import the latest MOF file via the settings - Inventory Extensions tab.

**Fixes**

* Fix issue with Settings > Validate license applying the license but not saving it to settings database
* Fixed Update Notification not showing minor version

**Misc Changes**

* Updated Branding

### 2.5.5 - 2026-04-08

**New Features:**

* Add Secure Boot Dashboard
  * N.B. This dashboard requires v 2.2.0 of the Inventory Extensions which was released 23rd March. You may need to click to update the inventory schema or import the latest MOF file via the settings - Inventory Extensions tab.

**Fixes**

* Fix Audit Log permission required issue caused by udpate notification
* Fix bug where Dashstat clickthrough isn't honouring filter set on load
* Fix bug where disabled actions in device modal dont appear disabled in dark mode
* Fix Windows version donut showing incorrect values

**Misc Changes**

* Update .net runtime to 8.0.25
* Update Task sequence charts to exclude disabled Task Sequences
* Added more logging around permissions logic to help troubleshooting

### 2.5.4 - 2026-01-26

**Fixes**

* Fixed Microsoft Windows Support Status in OS dashboard
* Fixed User Management Setting "New registered users are active by default." not being adhered to when disabled and a new Active Directory user is registered.
* Fixed browser extensions table not loading when date format uses DD.MM.YYYY

**Misc Changes**

* Updated dotnet runtime to 8.0.23

### 2.5.3 - 2025-12-04

**Fixes**

* Task Sequence Fixes
  * Custom Dashboards with Task Sequence items: Changing collection filter sets all tables to same data
  * When changing any filter the dates in the barchart go back 1 day for certain timezones
* SSD Wear progress bar incorrect colour
* Storage table empty on device modal due to newer instances of SCCM changing where the data is stored
* Nav Items Permission Issue for some users
* Fixed a bug where RBAC was not enforced for customers who specify a custom active directory domain.
* Custom Connection String fixes
* Global Search not working
* Non English Windows OS Contributing to Unknown segment in Windows Donut

### 2.5.2 - 2025-10-22

{% hint style="info" %}
This release can be updated automatically via the updater. For more details, [click here](../upgrading-insights/insights-updater.md)
{% endhint %}

**New Features**

* Revised BitLocker status on device modal to show Cipher Strength
* Show Model property on device properties portlet

**Misc Changes**

* Updated to dotnet runtime 8.0.21

**Fixes**

* Fixed Microsoft 365 Apps Support Status donut showing no data when data is available.
* Bug fix for missing table data in Microsoft Updates dashstat clickthrough table
* Fix divide by Zero error on Package modal for deployments
* Fix for Packages dashboard Size Column Sorting
* Win11 LTSC fixes
* Fixed multiple clickthrough modals from not loading

### 2.5.1 - 2025-09-02

**Features / Misc**

* In App Update Notifications and Enhanced Update Experience - Advanced Insights will now show all admin users a notification when a new update is available. The next time you log onto the server hosting Advanced Insights, you will be presented with an update prompt, which will then kick off the update process if you accept to continue. Details for this feature are [shown here](../upgrading-insights/insights-updater.md).
* Patch My PC Activity Dashboard - new dashboard to show Patch My PC patching activity. This new dashboard is available in Advanced Insights and Patch Insights. Description of the dashboard is [available here](../dashboard-guides/advanced-insights-patch-my-pc-activity-dashboard.md). NB The Activity Dashboard requires the latest version of the [Advanced Insights Inventory Extensions](../advanced-insights-inventory-extensions/) to be deployed to your clients. You may also need to grant access to this dashboard via the User or Role permissions using an admin account.
* Packages Dashboard - shows details of your legacy Packages environment. Track packages which are not distributed, have local source paths configured and are updating on a schedule. Click through for detailed package metadata. You may need to grant access to this dashboard via the User or Role permissions using an admin account.
* Boundary Groups Dashboard - view SCCM boundary groups, members and identify overlaps. This data is also shown on the device view on the general page. You may need to grant access to this dashboard via the User or Role permissions using an admin account.
* Implement Cancellation tokens wherever applicable
* Extend audit logs to include impersonated user
* Ability to set full custom SQL Connection String
* Update RestSharp NuGet packages
* Nutanix AHV devices now detected as Virtual Machines

**Fixes:**

* Custom Dashboard OS Deployment Items description errors.
* Table column Greater than filter bug on int values.
* Donut Refresh Resets Collection filter set on load.
* CVE Modal now displays correct number of devices affected
* On first login after install password reset doesn't redirect and shows error on 2nd click.
* Welcome screen always shows on login for some users even though details are entered
* Fix for Installer Modify Password reset for brand new installs.

### 2.4.9 - 2025-06-10

**Fixes:**

* Fixed an RBAC config which may have resulted in RBAC rules not being applied.
* Fixed Users and User Groups dashboard tables not showing any data
* Fixed Storage wear % colours on the device modal hardware tab.

### 2.4.8 - 2025-06-03

{% hint style="warning" %}
This release was re-uploaded on 2025-06-05.
{% endhint %}

**Features / Misc**

* Update logic in Installer when selecting self-signed cert during upgrade
* Add OS Support Status for Windows Business SKU
* Remove unsupported password reset and email activation from login pages
* Disable table click event on long press of left mouse button, helps when highlighting text in tables for copy/paste
* Add more logging to Client Actions, logging what devices were sent in the request
* Update Task Performance Item to allow filter by task sequences in Custom Dashboard
* .NET update to 8.0.16

**Fixes:**

* Fixed Installer Password reset by ensuring references to EditionId field are removed.
* Fixed intermittent issue where Dashboard item filters sometimes get swapped around on load
* Fixed an issue where editing a Custom Dashboard failed because a user that the dashboard was shared with no longer existed.
* Fixed table sorting on Hardware > Storage > Size, DiskSize and FreeSpace Columns
* Fixed Entra fields not being shown in Settings when no details are provided
* Fixed issue retrieving HP warranty records when a large amount of devices are in Workforce Experience.

### 2.4.7 - 2025-04-23

**New Features:**

* In custom dashboards add ability to save spaces between items
* Updated Icons in Custom Dashboard Grid
* Revised Computer Status dashboard to show activity based on last status rather than when an update was released or revised
* Office 365 Support SQL Changes to account for new LTSC channel (2024)
* Improve Table 'Loading' and 'No Data' message appearance.

**Fixes:**

* Fix table page and row count label issues when removing all rows from table (seen in Custom Dashboards)
* Custom Dashboards cannot filter to User Collections in Dashboard Item Tile Filters
* Custom Dashboard Builder grid Items don't represent actual width.
* Table select all doesn't uncheck properly when performing an action with selected items
* SMTP Settings SSL domain error
* Add to Collection errors in various dashboard screens
* Welcome screen always shows wrong logo
* When changing Table Page Size it shows all rows rather than selected amount
* SQL Fix for Slow Software Usage dashboard
* Software Metering Fix to include CE HINT

**Misc Changes**

* Updated Dotnet runtime to 8.0.15

### 2.4.6 - 2025-03-27

This is a bugfix release

**Fixes**

* Fixed issue with saving layout changes in custom dashboards.
* Fixed issue with Local Administrators not being collected when reported in Spanish.
* Fixed installer issue for invalid domain entry error on setup

**Misc Changes**

* Updated Dotnet runtime to 8.0.14

### 2.4.5 - 2025-03-04

This is a bugfix release

**Fixes**

* Add search box to device modal > Software > Inventory & Applications tab
* Collection Filters Set on Custom Dashboard Selections Don't Apply or Save
* Software > Client Inventory Click through doesn't load data unless Inventory Extensions installed
* Update Table Pager so disabled buttons are more distinguishable
* Obfuscate Network Proxy Password in Settings and Welcome page
* Custom Dashboard Role Permissions' reflect actual value
* Removal of delta caching when performing a warranty cache. This should fix missing devices in warranty.
* Fix Issue with SMTP Settings > UseDefaultCredentials not saving, which caused SMTP errors for anonymous email servers.

**Misc Changes**

* Updated Dotnet runtime to 8.0.13

### 2.4.4 - 2025-02-05

This is a bugfix release

**Fixes**

* Fix for Threat analytics click through modal has no data.
* Threat Analytics Vulnerabilities tables order by Base/Temporal Score column.
* Tooltip styling improvements

### 2.4.3 - 2025-01-30

This is a bugfix release

#### Fixes

* Fix Issue with Threat Analytics failing to load due to not handling empty CVE descriptions gracefully.
* Fix Collection filter not taking global filter into account when clicking table row.

### 2.4.2 - 2025-01-27

This is a bugfix release

#### Fixes

* Fix GetHealthReport noisy logs.
* Fix for Single Sign On Lockout issues.
* Enable recovery key renderer and add red icon colour for when key is available but no user permission, added icon tooltips explaining why key isn't accessible.
* Fix issue with sorting table columns that have a transformed value.
* Ensure table column filter icon only shows on filterable columns.
* Fix issue with custom logo display and setting.
* Fix table click though to list modals not taking Global Collection filter into account.
* Added StartDate to warranty table.
* Enable Sort and Filter on table columns where applicable.
* Increased Table font size.
* Fix Device Modal add devices to collection issue.
* Fix Bulk Actions from Client Inventory > Applications Table click through Modal

### 2.4.1 - 2025-01-06

This is a major release.

#### New Features

* Updated Base Framework
* Replaced Table component with new custom table renderer.
* Table export now uses transformed value for time period e.g. Hardware > Storage > PowerOn column shows 7y, 125d, 7h rather than raw value.
* Added option to set more than 2 table column filters per column.
* Added option to set custom IIS Application Pool Identity via Installer during installation/upgrade/modify.
* Added Serial Number column to Hardware > Displays > Connected Displays table.
* Added Documentation links to dashboards.
* Added Server Can't Connect page to display rather than hanging on load.
* Improvements to Software Usage & Metering SQL.

#### Breaking Changes

* Added ability to set Permissions for missing pages that didn't have the ability previously.\
  This means users will no longer have access to these pages as they wont have the required permissions, an admin will need to apply the necessary permissions to the users/roles that require access for the following dashboards:
  * Software > ODBC
  * Software > BrowserExtensions
  * Operating System > Dashboard
  * Operating System > Win11
  * Operating System > LocalAdmins
  * Operating System > Uptime
  * Operating System > UserProfiles
  * Hardware > Wireless

#### Fixes

* Fix issue with Two Factor Authentication token check.
* Fix issue with Warranty key being corrupted on settings upates.
* Fix for Warranty when receiving incompatible data from HP server.
* Fix issue with bulk actions not working on some modals due to missing Computer Online info.
* Added better error handling and logging to Threat Analytics processing.
* Fixed browser extensions dashboard not displaying data in table because of incorrect parsing of InstalledDate.

### 2.3.7 - 2024-11-13

This is an optional bugfix release

#### New Features

* Added ability to change timeframe range for Software usage dashboard. You can now select 1, 3 (default) and 6 month as the daterange for the dashboard
* Sql performance updates

#### Fixes

* Dell warranty fix for ID issue with newer warranty requests
* Filters in custom dashboard that are part of the description now update correctly.
* Fixed custom PMPC client actions not being invoked for a device.

#### Misc Changes

* Updated dotnet runtime to 8.0.11

### 2.3.6 - 2024-10-23

This is an optional bugfix release

#### New Features

* Remove multiple selected devices from a collection
* Add ability to set Custom Names on Custom Dashboard Items
* Global Search updates -
  * Sort by column on load
  * Search Inventory
  * Add export option
* After clicking page refresh disable button for 5 seconds
* Automatic decryption (if permissions granted) of BitLocker Keys if encrypted
* Device Modal shows client boundary group and internet/intranet status
* Add Bulk Actions to CVE Modal

#### Fixes

* Update Vulnerable Nuget Packages
* Tooltip shouldn’t show over portlet button menus
* Changing Dashstat month bug not taking global filter into account
* Bulk action requests fail when request payload is too large
* Editing a Custom Dashboard requires it to be saved with a new name
* German translation for password change message wrong
* Custom dashboard Barchart description shows loading
* Add a CreateCollection Permission to be used when creating collection
* Fix Device Modal tabs on patch insights.
* Intermittent page crash on load due to signal r issue
* Some Windows versions incorrectly showing as expired
* Client Inventory SQL updates to fix missing data issue.

#### Misc Changes

* Updated dotnet runtime to 8.0.10

### 2.3.5 - 2024-09-11

This is an optional bugfix release

#### Features

* Add Selected Devices to Collection now allows multiple Collections to be selected or created.
* Allow Filtering on Client Version Column Client Deployment Modal Table
* Collection Modal Bulk Add Devices to Collection icon change and update to allow comma, new line & carriage return separators on input form
* Update Window 11 Readiness to include GE24H2 (Win11 24H2)
* Update Bitlocker recovery key display to show decrypted if execute permission is granted.

#### Bug Fixes and Misc

* Update dotnet to 8.0.8
* Collection Modal Bulk Add Devices to Collection fixes
* Fix Collection Modal Remove Device from Collection bug when removing more than 1 device.
* Custom Dashboard shouldn't allow saving or editing a dashboard with same name as existing.
* Fix database migration for EU Time zones
* Software Updates Modal Refresh table fix
* Distribution Points List fix when no drive letter found on broken Distribution Point
* Show desktops and laptops on BitLocker TPM stats
* OSD Dashboard bug fixes
* Microsoft Update Dashboard bug fixes

### 2.3.4 - 2024-08-12

This is an optional bugfix release

#### Bug fixes

Fixed an issue for customers using older versions of SQL Server than 2016 SP1 (13.0.4001) not being able to load any dashboards (Incorrect syntax near 'HINT' ERROR).

Fixed the top row of statistics on the Warranty Dashboard.

#### Misc

Updated dotnet to latest version for security bug fixes (8.0.7).

### 2.3.3 - 2024-08-08

This is a required bugfix release

#### Bug fixes

Fixed an RBAC based issue with view more information when clicking on an application on the Software Applications dashboard.

Fix issue with Warranty dashstats not showing correct details

Update logic for SQL Server check that decides whether to include cardinality options

Updates to BitLocker recovery at risk data

### 2.3.2 - 2024-08-06

This is a required bugfix release

#### Bug fixes

Fixed an RBAC based issue with view more information when clicking on an application on the Client Inventory dashboard.

Fixed an RBAC issue when viewing more information about users

Fix clicking on a required update on the device modal and it loading the update details modal

### 2.3.1 - 2024-08-01

This is a major release.

#### New Features

HP Warranty support. Advanced Insights can now surface HP client device warranty data. There is some configuration required which is detailed here:[https://docs.patchmypc.com/installation-guides/advanced-insights-and-patch-insights/external-service-hp-warranty-api](https://docs.patchmypc.com/installation-guides/advanced-insights-and-patch-insights/external-service-hp-warranty-api)

<figure><img src="../../.gitbook/assets/image (2630).png" alt=""><figcaption><p>HP Warranty data in Advanced Insights</p></figcaption></figure>

#### Audit logs

In the Administration node you will find the “Audit logs” area. This lists all activities in the Advanced Insights portal. The list is filterable by user and can be exported.

<figure><img src="../../.gitbook/assets/image (2635).png" alt=""><figcaption><p>Audit log view</p></figcaption></figure>

#### Create collections

You can now create new ConfigMgr collections using Advanced Insights. The Resources - Collections page has a "Create New Collection" button.

<figure><img src="../../.gitbook/assets/image (2632).png" alt=""><figcaption><p>Create New Collection</p></figcaption></figure>

You can also create a collection from a device list and automatically add the selected clients to a new collection or add to an existing collection.

<figure><img src="../../.gitbook/assets/image (2634).png" alt=""><figcaption></figcaption></figure>

#### Delete user profile task

We have added a new function to allow you to delete profiles from client devices. This is useful in support scenarios for outdated or orphaned profiles.

<figure><img src="../../.gitbook/assets/image (2636).png" alt=""><figcaption><p>User profile dashboard with delete function.</p></figcaption></figure>

The delete action is also available in the device view - Users - User Profiles.

#### BitLocker Recovery Key view

For customers with BitLocker MBAM integrated with Configuration Manager we will now allow you to view the BitLocker Recovery Key in Advanced Insights. Users must have the relevant permission in their Advanced Insights role. The key is accessible via the Device View - Hardware - Disks tab.

<figure><img src="../../.gitbook/assets/image-(596).png" alt=""><figcaption><p>Viewing the BitLocker Recovery Key</p></figcaption></figure>

#### Device View export improvements

We now support the export of any of the tables in the device view.

<figure><img src="../../.gitbook/assets/image (2637).png" alt=""><figcaption><p>Export device view data</p></figcaption></figure>

#### Configuration Manger Console Extension

The new Configuration Manager console extension brings Advanced Insights right into the ConfigMgr console. Full documentation and download is here [https://docs.patchmypc.com/installation-guides/advanced-insights-and-patch-insights/configuration-manager-console-extension](https://docs.patchmypc.com/installation-guides/advanced-insights-and-patch-insights/configuration-manager-console-extension)

<figure><img src="../../.gitbook/assets/image (2518).png" alt=""><figcaption><p>Advanced Insights in the ConfigMgr Console</p></figcaption></figure>

#### Log builder for support cases

We have included a new Log Builder application, this is integrated into the Installer wrapper and will execute automatically on failure. It can also be run manually from C:\Program Files (x86)\Advanced Insights\Api\LogCollector\AdvancedInsightsLogDiag.exe. When run it creates a zip file on the desktop with environment details and logs to aid Patch My PC Support in troubleshooting.

#### Optimisations

Modal views with multiple tabs now load the tabs on-click, making initial load faster.

Filters on dashboard pages are now cached and load only once per-page rather than once per-object.

#### Bug fixes

Modal views now all obey RBAC when being accessed via a shared link.

Fix for modal failing to loading via a shared link.

Month-based software updates dashstat now fixed for custom dashboard load.

#### Misc changes

Client secrets for warranty providers are now obfuscated in the UI.

### 2.2.3 - 2024-06-28

This is a minor bugfix release.

#### Fixes

Fix for Software Updates dashboard not loading for some customers.

### 2.2.2 - 2024-06-27

This is a minor release mainly focused on bugfixes.

#### New features

Modal sharing allows users to share select modals for other to see, allowing collaboration between users who are working on a task together.

<figure><img src="../../.gitbook/assets/image (2367).png" alt=""><figcaption><p>Share icon on the top right, which will copy the link directly to your clipboard to be shared.</p></figcaption></figure>

#### Fixes

Fixes for action buttons on device modal for logs and PMPC actions not working correctly\
SQL changes for CPU duplication and device modal\
SQL changes for device resources to ensure obsolete devices are excluded\
SQL changes for device resource popups to show unknown for manufacturer and model rather than null

Fixed warranty recache not working without settings permission.

Fixed textarea font being wrong

Multiple custom dashboards fixes, mainly around filter selection for certain items.

Global filter selection now filters modals when the dashboard has changed.

### 2.2.1 - 2024-06-11

This is a major release.

#### New features

#### Custom Dashboards.

Users can now create a dashboard of their own items from all viewable items for their role. For example, a user can create a dashboard with objects from Resources, Hardware, Software Updates Trend, OSD, all in one view.

<figure><img src="../../.gitbook/assets/image (2254).png" alt=""><figcaption><p>Custom Dashboard Builder</p></figcaption></figure>

Custom dashboards can also be shared with other users or roles (permissions permitting).

#### Revised SQL queries for large performance gains

We have made hundreds of SQL Cardinality statements to ensure SQL performance is consistent across different SQL Cardinality levels.

#### Custom logos

<figure><img src="../../.gitbook/assets/image (2255).png" alt=""><figcaption><p>The Settings Appearance Tab</p></figcaption></figure>

New option to specify custom logos for the identity banner in the Advanced Insights portal. The logo file is what is shown when the menu is expanded, the Icon setting is shown when the menu is minimized.

#### New Dashboards

#### Local Administrators dashboard

<figure><img src="../../.gitbook/assets/image (2256).png" alt=""><figcaption><p>Local Administrators Dashboard</p></figcaption></figure>

The new Local Administrators dashboard requires the Advanced Insights inventory extensions. The dashboard shows the groups and accounts that are members of the local admins group on all devices.

#### OS Uptime dashboard

<figure><img src="../../.gitbook/assets/image (2257).png" alt=""><figcaption><p>OS Uptime Dashboard</p></figcaption></figure>

The OS Uptime dashboard lists each device and its latest uptime.

#### Wireless adapters dashboard

<figure><img src="../../.gitbook/assets/image (2258).png" alt=""><figcaption><p>Wireless Adapters Dashboard</p></figcaption></figure>

The Wireless Adapters Dashboard requires the Advanced Insights Inventory Extensions. This dashboard helps to identify the wireless NICs and associated drivers with the versions. Clicking through will show further details about wirless connectivity on the individual device:

<figure><img src="../../.gitbook/assets/image (2259).png" alt=""><figcaption><p>Wireless detail</p></figcaption></figure>

#### User profile dashboard

<figure><img src="../../.gitbook/assets/image (2260).png" alt=""><figcaption><p>User Profile Dashboard</p></figcaption></figure>

The User Profile Dashboard requires the Advanced Insights Inventory Extensions.

This dashboard shows the details for all profiles on client devices. Profiles which are unused for <90 days are highlighted as "Aged Profiles", "Orphaned Profiles" are profiels on devices for which there are no longer valid accounts.

#### Installer Improvements

Can now reset Admin password using Modify option in Add/Remove Programs. Can also change certificate, CNAME and port number with this option.

#### Software Metering Changes

Prior to this release Software Metering reports required the legacy Configuration Manager Software Inventory Agent to be enabled and performing inventory of any executable you wished to report Metering data for. This is no longer the case, Advanced Insights now uses the InstalledExecutable class, which is part of the Asset Intelligence inventory provider. The legacy Software Inventory agent can be disabled if you were only using it to enable Metering reporting.

#### Bug Fixes

Fixed bug with "Patch My PC Actions" not working for some customers.

#### Misc

Look and feel clean-up

Updated dependencies and DotNet version to DotNet 8. DotNet 7 components can now be removed from Advanced Insights servers (if not required by other applications).

#### Deprecations

Boot Performance dashboard. Microsoft removed the dependent dataset from the Configuration Manager product, so we have had to remove this dashboard.

### 2.1.2 - 2024-04-10

Minor optional release to fix an upgrade issue experienced by users who login via Azure Active Directory (Entra). This release fixes the error "Username '{emailaddress}' is already taken" when logging in.

### 2.1.1 - 2024-03-20

Minor release to permit upgrade for customers on pre-release version of 2.1.0 and to fix minor version numbering error.

### 2.1.0 - 2024-03-19

Major release with changes to infrastructure requirements and new functionality.

#### Updated dependencies

* Dotnet has been update to 7.0.17 for security fixes
* Advanced Insights no longer requires SQL Server for its configuration. Your config will be migrated to a new [SQLite database](https://docs.patchmypc.com/installation-guides/advanced-insights/download-and-install/advanced-insights-sqlite-database) on first load of the dashboard following upgrade. You can then remove the legacy PMPCAdvancedInsights database from your SQL environment.

#### New Functionality

* Major performance improvements in SQL load time for Home dashboard, Software Updates dashboard and Updates page.
* Update Trend dashboard

<figure><img src="../../.gitbook/assets/image (1666).png" alt=""><figcaption><p>Update Trend</p></figcaption></figure>

* This new dashboard provides visibility of deployment compliance trend over time. You can plot how long it took from update release to first install, 50% compliance, 90% compliance and total installation. The chart can be expanded under the cog icon to show total deployment data. On first load the update with most deployment data over the past 30 days will be selected, you can use the filter pickers below the chart to select other updates, date ranges and filter by collection.
* Browser Extensions Dashboard. New dashboard (requires latest inventory extension update)

<figure><img src="../../.gitbook/assets/image (1667).png" alt=""><figcaption><p>Browser Extension Inventory</p></figcaption></figure>

* Warranty dashboard now respects RBAC and Collection filters
* Custom Patch My PC actions available to install update, clear the CCM cache, Repair the ConfigMgr client a "Notify" option to send a message a to a device. These functions use the BGB Channel, so will function over CMG as well as on LAN. They are also available in the Bulk Actions lists, allowing you to bulk send a notification, or clear the ConfigMgr Cache on a list of machines.<br>

<figure><img src="../../.gitbook/assets/image (2043).png" alt=""><figcaption><p>Patch My PC Actions</p></figcaption></figure>

* Draggable modals - you can now move the popup modal views around the screen

#### Bug fixes

* Warranty re-caching now works again
* If the MSRC API has availability issues, we will now load cached data if possible

#### Installer Improvements

* Installer PowerShell custom actions rewritten into C#.
* Installer now includes modification feature to change the SSL certificate which is used for Advanced Insights.
* Dialog text and layout improvements.

### 2.0.3 - 2024-02-15

Minor release primarily for security and browser engine changes

{% hint style="info" %}
On 2024-02-23, an updated installer executable was created to address a failed upgrade issue faced by customers when upgrading from versions older than 1.0.27. If you have upgraded using the previous installer and Advanced Insights no longer loads, please perform a repair on the installation via Add/Remove programs or uninstall and reinstall using this new executable. The new installer is downloadable from [https://patchmypc.com/ai-download](https://patchmypc.com/ai-download)
{% endhint %}

#### Updated dependencies

* Dotnet has been update to 7.0.16 for security fixes
* Ag-grid has been updated to 31.0.1 for bug fixes

#### New features

* Tables page sizes can now be modified\
  ![](<../../.gitbook/assets/image (2026).png>)
* Microsoft version data is now bundled with the application as backup in case docs.microsoft.com is inaccessible
* Added additional info to AD settings, detailing how it works

#### Bug fixes

* Disabled global filter for warranty dashboard.
* Added in additional error messages and checks for AD Auth failures and why
* Fixed potential issue with tables not rendering and future EDGE/Chrome release
* Fixed filters not being applied on search and dashboards
* Multiple SQL changes for speed and accuracy
* "View more data" modals that showed no data are now fixed

### 2.0.2 - 2024-01-17

Minor optional update to add security scope for new graphics dashboard.

### 2.0.1 - 2024-01-16

Version 2.0.1 is a major release of Advanced Insights with breaking changes which require actions by the administrator to deploy the new [Inventory Extensions MSI](https://docs.patchmypc.com/installation-guides/advanced-insights/advanced-insights-inventory-extensions), replacing the legacy PowerShell solution used in version 1.0.

#### Breaking changes

* [Deployment of Advanced Insights extensions](https://docs.patchmypc.com/installation-guides/advanced-insights/advanced-insights-inventory-extensions) now relies on the SMS Provider for Hardware Inventory class extensions, which without correct permissions to the SMS Provider cannot install or update existing classes.
* Advanced Insights API App pool now runs as Local System instead of Network Service as the API Website has inherited the work of the Controller Website which ran as Local System.
* Port 44300 is no longer required for application functionality and firewall rules can be disabled. 44301 is now the only mandatory required port.

#### Deprecated functionality

* Proxy bypass is deprecated as there is no more localhost communication between websites.
* Advanced Insights extension PowerShell package is now deprecated and is no longer supported or recommended. Replaced with WMI Provider.
* Email and SMS based 2FA have been removed, Google (TOTP) based 2FA is the only support 2FA auth solution.

#### Major changes

* Extensions now work using WMI Provider and not PowerShell scripts.
* Application now consists of just the API and Frontend websites.
* Large installer rewrite.
* CNAME support.
* Global collection filter, allowing full dashboard collection filter with persistence between dashboard changes.

<figure><img src="../../.gitbook/assets/image (2019).png" alt=""><figcaption><p>Global Collections Filter</p></figcaption></figure>

* Windows 11 Readiness dashboard.

<figure><img src="../../.gitbook/assets/image (2018).png" alt=""><figcaption><p>Windows 11 Readiness</p></figcaption></figure>

* ODBC Dashboard.

<figure><img src="../../.gitbook/assets/image (2017).png" alt=""><figcaption><p>ODBC Configuration Details</p></figcaption></figure>

* Graphics card dashboard with click through details on device view.

<figure><img src="../../.gitbook/assets/image (2020).png" alt=""><figcaption><p>Graphics Card Inventory Detail</p></figcaption></figure>

* Client actions can now be performed against a list of devices in any data table.
* BitLocker compliance now provides "no compliance" reason.
* Device power state indicator in lists where a device is shown.<br>

<figure><img src="../../.gitbook/assets/image (2016).png" alt=""><figcaption><p>Screenshot of power state icons</p></figcaption></figure>

#### Minor changes

* Targeting latest dotnet 7 version and library updates.
* Remote control is now bundled with the application in the installation directory.
* Additional export functionality for Warranty data.
* Partial CVE Search in global search (MSRC Only).
* Extensions settings page redesign.
* Debug ability to limit amount of concurrent SQL queries being run against the DB

#### Bug fixes

* Revised SQL queries for Content DP List for Application Modal.
* Visual fixes around colours, spacing and layout.
* 2FA enablement in users’ profile is now visible.
* Misc fixes and optimisations.

### 1.0.27 - 2023-11-27

#### Features:

* Patch Insights - Update-focussed reporting solution for non-Premium SKU customers. The same installer is used, the version of Insights shown to the user is dependent on the Patch My PC Licence.

<figure><img src="../../.gitbook/assets/image (1984).png" alt=""><figcaption><p>Patch Insights interface with top-level dashboard and Software Updates dashboards.</p></figcaption></figure>

* CVE Dashboard improvement - BaseScore and TemporalScore tooltips added to describe what these mean for threat analytics.

#### Bug fixes:

**BREAKING CHANGES:**

* Switched Active Directory authentication to use UPN instead of email address for Active Directory users. If your user's UPN is different from their email address, then a new user will be created in Advanced Insights.

**NON-BREAKING CHANGES**

* Fixed bug removing settings inputs for Azure AD if "disabled" is not selected
* Fix issue in Global collection not being set
* Switched to using CNIsOnline for device online check in device modal to more reliably display online status. Also show online status in device modal title
* Fixed settings page not working for non admin role users
* Fixed license revalidate when not an admin user
* Modal fixes for View Chart Data for Servicing channel and Release Version
* Checkbox visibility improved
* Multiple revisions to the SQL queries related to performance
* Multiple smaller fixes

### 1.0.26 - 2023-10-02

#### Installer Improvements

*   Certificates dialog – complete redesign.

    Key certificate properties are shown within the dialog and flag any warnings

<figure><img src="../../.gitbook/assets/image (1740).png" alt=""><figcaption><p>Certificate Selection Dialog</p></figcaption></figure>

*   Upgrade dialog updated.

    Now includes info on the current certificate and if there’s any attributes of the certificate which require attention and an option to change the in-use certificate.

<figure><img src="../../.gitbook/assets/image (1741).png" alt=""><figcaption><p>Upgrade summary screen</p></figcaption></figure>

* Current certificate properties can be viewed in this screen:

<figure><img src="../../.gitbook/assets/image (1742).png" alt=""><figcaption><p>Certificate properties</p></figcaption></figure>

#### Product Improvements

* Support for non-English versions of Windows "Enterprise" in the Operating System support statements
* OSD Dashboard now shows progress for Task Sequences without the standard Apply OS step
* Threat Analytics dashboard now shows an error if SQL Functional Level is not at least 130
* Further proxy fixes

#### Known Issues

* Accessing the welcome page will reset proxy bypass to false, causing the application to fail to render any dashboards for customers who require this setting to be enabled.\
  To fix, please go to Administration -> Settings -> External Services -> Re-enable Localhost Bypass and save -> Restart the controller website via IIS Manager on the server hosting Advanced Insights.

### 1.0.25 - 2023-09-15

#### Product Improvements

* Proxy settings now allow both Localhost via proxy and Localhost proxy bypass. Proxies are now enabled for Localhost by default.
* Fixed application initialisation regression (spinning circle on load).

#### Installer Improvements

* The installer has new logic to exclude selection of certificates with weak signature algorithms ('SHA1', 'SHA1RSA' etc) and _**include**_ certificates with algorithms at SHA256 and above.
* During the IIS Configuration phase, the installer will now add required MIME Types and HTTP Verbs.
  * MIME Types
    * .json - (API, Controller and Warranty site objects)
    * .jsonId - (API, Controller and Warranty site objects)
    * .woff - (Frontend site object)
    * .woff2 - (Frontend site object)
  * HTTP Verbs
    * 'OPTIONS' = True are set automatically under ‘Request Filtering’ for both API and Controller site objects.

### 1.0.24 - 2023-09-13

#### Product Improvements

* Fix for issue with Advanced Insights when installed on the same server as Patch My PC Publisher. Changes to registry permissions in the Publisher led to an exception in the Advanced Insights portal.

### 1.0.23 - 2023-08-30

#### Installer Improvements

* The installer [upgrade experience](../upgrading-insights/) is now shorter. Upgrade will also complete using /q for a completely unattended upgrade.

#### Product Improvements

* Removed faulty Certificates class from custom inventory
* Modified faulty Local Group class to exclude domain controllers
* Improvement to proxy handling for proxy servers which route localhost entries.
* The login page was limited to 32 character passwords, this restriction has been removed
* Warranty tab would not load if General tab had not first been loaded
* Office 365 page load failure

### 1.0.22 - 2023-08-18

#### Installer Improvements

* First install now finds most appropriate free port for the frontend website, will default to 443 if available, then 444, then 44303 and up.
* Certificate selection dialog is now locale independent

#### Product Improvements

* Proxy support has been improved. If the Welcome Experience cannot access api.patchmypc.com it will automatically prompt for proxy details at first use.\
  The proxy types supported are http, socks4 and socks5. Please add the correct protocol to the start of your proxies network address e.g. http://x.x.x.x, socks4://x.x.x.x, socks5://x.x.x.x.\
  Ports can be added at the end of the network address e.g. http://x.x.x.x:1234"
* Software inventory reports failed with application version strings greater than 32 characters.
* Console users and device affinity sometimes missing from device view.
* Connected display view in device view was sometimes incorrect in screen display order.
* Missing data in "Missing Configuration Items" view in Microsoft Updates page.
* NULL Content Sources paths cause exception in Inventory Extensions tab.
* License File handling improved for license refresh scenarios.
* When using AzureAD Authentication first name and surname mapping was incorrect.
* Added functionality to differentiate between workstations and servers on the pending restart reports.
* Data Export function missing from Collections, Connected Displays, Batteries data, Physical storage devices.
* Fixed a bug that caused roles with an AD group to not be assigned to the user if any other roles were set as default.

### 1.0.21 - 2023-07-14

#### Product Improvements

* Bug with Warranty Service when installing on ConfigMgr database host. If you are not affected by this then you do not need to upgrade. Can also be fixed by carrying out the following process:
  1. In IIS Admin go to Application Pools, find the Advanced Insights Warranty App Pool, select it and click Advanced Settings
  2. Scroll down to the Identity property and change it from NETWORK SERVICE to LOCAL SYSTEM and click OK to that change
  3. Browse to %ProgramData%\AdvancedInsights\Data\Warranty and delete the AdvancedInsightsWarranty.db file
  4. Now go back into Advanced Inisghts and go to Administration - Settings - External Services and uncheck the "Warranty - Is Enabled" checkbox. Save this setting.
  5. Now go back to that tab and re-enable Warranty and Warranty Caching. Save this.
  6. Go back to the Warranty Dashboard and click the Bulk Processing dashstat in the top left.

### 1.0.20 - 2023-07-12

#### Installer Improvements

* Installer will install Internet Information Server if it is not already present
* SQL Connection dialog allows user to check permissions to database as well as connectivity
* Certificates dialog excludes a wider range of invalid certificates (checks DNS/SAN names are FQDN)
* Enhanced support for non-English languages (especially French)

#### Product Improvements

* Fixed the following bugs:
* Distribution Point view showing incorrect drive letter
* Device view title not populating with client name
* Inventory script for getting battery health times out
* CVE view does not load when opening CVE tab from Update view
* Remote control helper download link was invalid
* AD authenticating users may have group-assigned roles added multiple times
* Invalid security permissions removed for "Security Analyst" dashboard
* User with access to Collection dashboard has rights to modify collection membership even if that right is not granted
* Unable to see all data in Content Sources - CloudDP - Host table
* Missing descriptive text on OS Boot Performance dashstats
* Task sequence action errors show incorrect year date
* AD integrated environments do not assign default roles if group-assigned roles are applicable
* Dashboards fail to load when installed on French Language server OS
* View Chart Data option on Windows Servicing chart shows correct data

#### New Features / Changes

* Operating System Page now has Pending Restart data
* Software - Client Inventory now includes User Installed Applicaiton info
* Added SMTP Configuration settings
* IIS Application Pool identities are now NETWORK SERVICE and LOCAL SERVICE instead of LOCAL SYSTEM for API, Warranty and Frontend websites. Controller can run under NETWORK SERVICE (requires manual modification) if running on a server which is not the SCCM site server.
* Log files now created in %ProgramData%\AdvancedInsights\Logs folder and with .log extension
* Warranty database now created in %ProgramData%\AdvancedInsights\Data
* Usability improvements to Welcome experience

### 1.0.19 - 2023-06-06

#### Installer Improvements

* Installer will remember last used certificate and SQL server details from this version on - support for silent upgrade for version 1.0.20 onward.
* Previous used certificate is highlighted in certificate dialog to help with setup.

#### Product Improvements

* Fixed bug for device view title not loading correctly in certain scenarios
* Remote control helper download and functionality fixed (see [this document](../requirements-for-advanced-insights-remote-control.md) for details)
* Bug where AD user accounts have roles reassigned at each login is resolved
* Removed unneeded role entries
* Added SMTP configuration settings for email notification to users on account creation and password reset
* Fixed bug with users having rights to add devices to collections via collection dashboard when this right was not granted
* You can now include a default ConfigMgr collection for any role or user. This setting will auto-populate all dashboards with this collection as a filter where appropriate. A user can still select other collections they have access to view if desired.\
  ![](<../../.gitbook/assets/image (1963).png>)

### 1.0.17

Internal build, not released publicly.

### 1.0.18

Internal build, not released publicly.

### 1.0.16 - 2023-05-19

#### Installer Improvements

* Installer now shows details of in-use certificate on upgrade so that re-selecting the correct cert is simpler if that is the correct action. You can still pick a different certificate if required.
* We stop the App Pools on upgrade to try to alleviate issues with upgrade failing because of files in use.

#### Product Improvements

Fixed a bug when navigating to a CVE record from an Update record

### 1.0.15 - 2023-05-16

#### Improvements

* Removed the facility to upload custom logos, as this caused a problem rendering dashboard pages.
* User Role functionality errors required a user to have access to Settings area, this is no longer required.
* New roles did not function as expected and required an AD Group to be assigned, this is now fixed.
* Validation of Active Directory Group name fails when associating a role to a group, this has been fixed.
* CORS errors and dashboard load failure when the front end website is installed on port 443, this is now fixed.
* HP Devices show invalid data in Warranty dashboard. As the HP Warranty API is now deprecated this functionality has been removed.
* Export option missing from Application Compliance views.
* Added username to Application Compliance and Update Compliance view.
* Added collection filters to Hardware dashboards.
* Added RBAC filtering to Collections dashboard.
* Added Average Performance column to Operating System - Boot Performance dashboard.

### 1.0.1 - 2023-05-01

* Initial release of Advanced Insights

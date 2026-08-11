# Preview Releases of Patch My PC Publisher

_Applies to: Patch My PC Publisher V2.x_

Details the production release history for preview versions of Patch My PC (PMPC) Publisher, the most recent release being shown first.

> \*\*Note\*\*
>
> You can find the Preview release notes below, and you can also learn more about the Preview channel here: [Publisher Preview Channel](https://patchmypc.com/preview-channel).

## 2.3.2.476 - 2026-07-22

<details>

<summary>Improvements</summary>

* Added pagination to the Entra ID group picker while retaining selections across pages.
* Significantly improved ConfigMgr folder-browser performance for large folder structures.
  * Previously, loading 1500+ folders could take 5-10 minutes. This now takes a couple of seconds.
* The Cloud tab now remains visible for all license states. Ineligible licenses disable the connection without deleting saved configuration.
* Improved Settings Apply responsiveness and prevented incomplete SQL settings from starting database operations.

</details>

<details>

<summary>Fixes</summary>

* Restored non-blocking warnings when publishing is enabled without selected products.
* Restored vendor-level **Move Application** configuration for ConfigMgr applications.
* Fixed package extraction for republished Intune Win32 applications.
* Intune assignment filter selection now excludes non-Windows and managed-app filters.
* ConfigMgr applications deleted while content remains are recreated during the same synchronization.
* ConfigMgr connectivity is no longer required when application publishing is disabled.
* Fixed a crash when opening device counts after clearing ConfigMgr scan settings.
* Tenant-specific conflicting-process settings no longer overwrite global defaults.
* Corrected conflicting-process timeout conversion and Insert Variable field targeting.
* Hardened settings imports to safely preserve encrypted values and reject unsupported cross-machine secret imports.
* Prevented update prompts from offering versions older than the installed UI or service.
* Restored post-upgrade welcome notifications and improved expired or invalid license guidance.
* SMTP test results and Delivery Optimization information dialogs now appear above progress overlays.
* Disabling logging no longer replaces a custom log-folder path.
* Add/Edit Commands is available when a product uses only additional file or folder script assets.
* Improved license refresh behavior, remaining-days calculation, and ConfigMgr SQL validation.
* Canceling an All Vendors bulk selection now aborts the entire operation.
* Clicking an indeterminate Vendor or All Vendors checkbox now selects all products instead of unselecting all products.
* Fixed false no-products-selected warnings after selecting the first filtered product.
* Fixed selective-sync API requests reporting success when nothing was marked for publishing.
* Fixed Config API errors for unsupported uploads, invalid tenant identifiers, and ports already in use.
* Fixed compatibility failures when an older Newtonsoft.Json assembly is installed in the GAC.

</details>

<details>

<summary>Accessibility and UI</summary>

* Added vertical scrolling to ConfigMgr scan pages and restored the application-list scrollbar.
* Added visible invalid-path feedback to the CVE Import Wizard.
* Added explanations when Scan Query is disabled.
* Kept vendor, product, and webhook checkbox states synchronized across filters and bulk selection.
* Improved Entra ID group messages and text visibility across Light and High Contrast themes.
* Improved filter naming, Cloud deployment indicators, icon theming, button sizing, text rendering, keyboard navigation, and window hover states.
* Added copyable release-note links and consistent Publisher Statistics labels.

</details>

## 2.3.2.287 - 2026-07-13

<details>

<summary>New Features and Improvements</summary>

#### User Interface Enhancements <a href="#h-user-interface-enhancements" id="h-user-interface-enhancements"></a>

* Reorganized the Publisher settings and navigation layout to improve usability and streamline workflows.
* Added a confirmation prompt before running Publishing Service Sync from the **Run Publishing Service Sync** button.
* Improved the behavior of information filters, making it more intuitive to clear and reset filters throughout the Publisher UI.
* Added support for delaying in-place updates for Intune Applications and Updates.

#### Intune Improvements <a href="#h-intune-improvements" id="h-intune-improvements"></a>

* Fixed an issue where the retained-app safeguard could incorrectly prevent valid Intune application re-creation.
* Resolved multiple Intune assignment-related issues.
* Fixed an issue where the Intune application secret could expire after restarting Publisher.
* Fixed preview version display on the About tab.
* Corrected an issue that could extract ZIP file contents to an incorrect folder when using delayed application upgrades.
* Fixed an issue where a stale client secret could be used by the Graph Mail OAuth token provider.

</details>

<details>

<summary>Bug Fixes</summary>

#### Publishing and Synchronization <a href="#h-publishing-and-synchronization" id="h-publishing-and-synchronization"></a>

* Fixed an issue that could trigger a duplicate publish synchronization operation.
* Preserved catalog process lists when the saved process pattern is empty.

#### Application and Service Reliability <a href="#h-application-and-service-reliability" id="h-application-and-service-reliability"></a>

* Resolved a Newtonsoft.Json version mismatch that could cause a `JToken.WriteTo` `MissingMethodException`.
* Updated logging to correctly honor a custom runtime log path and added additional test coverage.
* Fixed validation issues when editing webhooks.
* Consolidated System.Net.Http assembly references to improve reliability.

#### User Interface <a href="#h-user-interface" id="h-user-interface"></a>

* Disabled **Export to CSV** until a query has been executed.
* Fixed license date formatting issues and added support for copying cloud portal links.
* Corrected various UI issues across the **General**, **WSUS**, and **Cloud** tabs.
* Fixed an issue where expanding **Alerts** on the **Advanced** tab could incorrectly redirect to the **About** tab.
* Standardized GroupBox header font sizes throughout the **Advanced** tab.

</details>

<details>

<summary>Accessibility Improvements</summary>

#### Keyboard Navigation <a href="#h-keyboard-navigation" id="h-keyboard-navigation"></a>

* Improved synchronization between grid selections and dropdown selections when using keyboard navigation.
* Added keyboard access support for DataGrid column headers.
* Corrected DataGrid tab navigation and focus traversal behavior.
* Resolved keyboard navigation conflicts throughout the application.

</details>

## 2.3.2.193 - 2026-07-06

<details>

<summary>Enhancements</summary>

* A clearer default tooltip is shown when no code-signing certificate is selected.
* Several Certificate Management UI inconsistencies (text, dialog sizing, and icons) were resolved.
* A new Advanced option hides the Intune Apps and Intune Updates tabs, matching the existing options for WSUS and ConfigMgr. The Advanced "Intune Standalone Options" section is now named "Product Integrations."
* PatchMyPc.log has been reintroduced. It will contain all informational, error, and exception messages. Each component (e.g., ConfigMgr, WSUS, Sync, UI, Licensing) will still have its own log file that contains all log levels listed above, as well as debug logs.
* Removed the obsolete Log Level (Information/Debug) dropdown from General settings; logging is now managed automatically.

</details>

<details>

<summary>Fixes</summary>

* Assignment date/time pickers now default to today at 12:00 AM UTC.
* Fixed availability and deadline times being set identically without warning when choosing a specific date/time.
* "Clear All Filters" now works after reloading a filtered tab.
* Fixed a crash that could occur when running Sync Now in some cases.
* CSV export headers now match the columns shown in the UI for the scan wizards.
* The Publisher no longer creates a stray "Logs" folder on the desktop.
* Fixed a bug that caused the Manage Conflicting Processes list to clear unexpectedly.

</details>

## 2.3.2.54 - 2026-06-23

<details>

<summary>🖥️ Modernized User Experience</summary>

The biggest change in this release is a ground-up redesign of how you interact with the Patch My PC Publisher. The focus is strictly on reducing clutter and speeding up your day-to-day workflow.

* **Streamlined Left-Hand Navigation:** A clean side menu replaces the original tabbed layout, letting you jump between sections instantly.
* **In-Window Integration:** Gone are the days of endless pop-ups. Most configuration dialogs are now embedded directly into the main window.
* **Theme Support:** You can now natively toggle between **Light Mode** and **Dark Mode** depending on your workspace preference.

</details>

<details>

<summary>📊 Improved Application Views</summary>

Managing your applications is much more visual with three distinct layout improvements:

| **View Feature**       | **What it Does**                                               | **Why it Helps**                                                              |
| ---------------------- | -------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Grid View**          | Displays applications as visual cards with key details.        | Allows for optional grouping of app variants to keep things neat.             |
| **Stats View**         | A built-in statistics panel providing high-level app insights. | **Interactive:** Clicking any individual stat instantly filters your results. |
| **Tabbed Assignments** | Splitting assignment types across dedicated tabs.              | Cleaner visual layout when managing large numbers of assignments.             |

> 📍 **Note on the Progress Bar:** The synchronization progress bar has a new home. You can now find it on the **Service Status** page located under the **About** tab.

</details>

<details>

<summary>🔍 Enhanced Filtering and Organization</summary>

Finding the specific products you need takes far fewer clicks.

#### Advanced Filtering

Quickly drill down into our massive catalog to locate specific apps and complex configurations with upgraded, high-performance filters.

#### Separate Product Tabs

Products are now logically split into two dedicated sections to keep custom work isolated from standard vendor catalogs:

* **Catalog Products:** Standard, pre-packaged third-party applications from Patch My PC.
* **Custom Products:** In-house or custom-packaged applications using Patch My PC Cloud

</details>

<details>

<summary>🔔 Alerts and Status Improvements</summary>

* **Dedicated Alerts Pages:** Alerts have been broken out into separate, dedicated views so you can manage notifications without noise.
* **Centralized Service Status:** A dedicated health page housing your live sync progress.

</details>

<details>

<summary>🛠️ New Tools &#x26; Functional Changes</summary>

#### 1. Show Dependencies

You can now view application dependencies directly in the Publisher, minimizing deployment failures down the line.

#### 2. ConfigMgr Detection Script Signing

As an alternative to using your standard WSUS certificate, you can now supply a **custom code signing certificate** specifically to sign ConfigMgr detection scripts.

#### 3. Webhooks Deprecation Notice

> ⚠️ **Important:** You can no longer create or copy legacy Microsoft Teams webhook alerts inside the Publisher. If you have existing legacy webhooks configured, they will continue to function normally for the time being, but planning a migration to modern alerting is highly recommended.

</details>

## 2.2.2.224 - 2026-06-15

<details>

<summary>Fixes</summary>

* Fixed a bug causing tools like the Intune Scan Wizard, Intune App Manager, and Intune Auto-Publishing rules to fail to load all tenants when an MSP had more than 22 tenants configured.

</details>

## 2.2.2.217 - 2026-06-11

<details>

<summary>Improvements</summary>

* Update validation for pre/post script argument configuration.
* Update logging for WSUS update republishing.

</details>

<details>

<summary>Fixes</summary>

* Ensure the Cancel button stops loading Intune applications in the Intune Application Manager.
* Fix a bug that causes the Availability and Deadline time configuration in the Intune assignment manager to reset when reopened.

</details>

## 2.2.2.98 - 2026-06-02

<details>

<summary>Fixes</summary>

* Ensure Auto-Publishing rules are saved as expected for Intune and ConfigMgr scan wizards.
* Refresh button in the Intune Filter Editor view now properly clears the cache and pulls the up-to-date list of filters from Intune.
* Fixed a bug causing the selected products to not show as selected within the Intune Scan Wizard. This could cause a product to be unselected unexpectedly.
* Ensure Azure chunk uploading respects the configured upload timeout.
* Fix a bug causing Selective Sync, and Republish to not process as expected in some cases.

</details>

## 2.1.120.177 - 2026-04-28

<details>

<summary>Fixes</summary>

* Fixed an issue where the _Manage Assignments_ window could not be resized when accessed via right‑click actions in the Intune Apps and Updates tabs. The window can now be resized to more easily view and manage multiple assignments.
* Resolved an issue where the Copy button was no longer visible, allowing customers to once again copy products and customizations between entries.
* Fixed an issue where scrollbars only supported mouse‑wheel scrolling instead of click‑and‑drag interaction in the following areas:
  * WSUS Updates
  * ConfigMgr Application Manager
  * Intune Application Manager
  * Intune Update Manager
* Fixed an issue where an unexpected progress indicator appeared when viewing assignments for a single Intune application, incorrectly showing the total number of applications being loaded before the assignment window opened.
* Confirmed expected behavior when filtering Intune scan results with a count of zero. These views are designed to display only applications detected on devices, while exports remain available for reviewing zero‑count results.
* Fixed an issue that could cause repeated event log errors due to log file access conflicts, helping reduce unnecessary logging and monitoring alerts while the Publisher is running

</details>

## 2.1.120.131 - 2026-04-22

<details>

<summary>Improvements</summary>

* Increase Intune upload timeout to one hour for large files and other enhancements to the Azure upload process.
* When selecting the Use Existing App Registration option, you are now given a choice of Intune tenants to choose from.
* Display Entra groups that have been deleted with a prefix of \[Deleted Group: \<Group ID>] when editing DO Priority.
* Ensure the Publisher gracefully handles the case where its connection is deleted in the cloud.

</details>

<details>

<summary>Fixes</summary>

* Fix a bug causing the user to be unable to add a new language to Manage Conflicting Processes.
* An error message was displayed in the wrong place when editing a webhook.
* Resolve an issue that causes the Publisher to improperly parse the installation command line for WSUS in some cases. This could result in an update being published with an incorrectly formatted installation command.
* Grace period for required assignments can be disabled.
* Republishing an Intune Update retains the icon.
* Pause Product only worked for the first tenant in the list when MSPs had more than one tenant configured.
* Large Intune reports would fail to write to disk, causing an Out Of Memory exception.
* Fixed a bug where some applications would not be found in the local content cache.
* Clicking Browse in the Manage Pre/Post Scripts window would sometimes cause the Publisher to force close.
* When running a sync, Auto Publishing rules would return 0 devices for the Intune Report, even when Devices were present.
* Switched from using JSON to LiteDB for Intune Report Caching to improve report performance.
* Ensure the co-existence status is propagated to the cloud when a product is unselected in Publisher.
* Requirement Architecture was not correctly interpreted by the Publisher when creating Intune Apps.
* Fixed a bug causing products marked for 'Exclude from auto-publishing rules' not to be saved when the product treeview is filtered to enabled products only.
* Addressed bug in Teams webhooks, causing notification to be missing version and other information.
* The SMTP Oauth Test permission button would only ever account for the first tenant configured.
* Fix a bug causing the WSUS Update Modification Wizard to not load in some cases.
* Intune tenant names were not correctly shown in the webhook list under the Alerts tab.
* Ensure the nth-day-of-the-week option for a monthly sync schedule maps correctly to settings.xml.
* The product export feature in the Advanced tab no longer exports duplicate rows for Intune applications and updates.
* Refresh the Intune authentication token before retrieving reports from Intune when performing auto-publishing during synchronization.
* CVE, Classification and Severity data were not populated in Publisher email reports for existing applications that received an update to a new version.
* Ensure the OS requirements are set appropriately for ConfigMgr and Intune Publishing.
* The Package Details would improperly display an error dialog when clicking a link to a package's local content file, even when the content was found. It now shows a success dialogue, and the error dialogue is reserved for when the file is not found

</details>

## 2.1.108.10 2026-03-19

<details>

<summary>Fixes</summary>

* Fix a bug causing products marked for '[Exclude from auto-pubilshing rules](https://patchmypc.com/kb/right-click-options-available-updates/#h-exclude-from-auto-publishing-rules)' not be saved when the product treeview is filtered to enabled products only.
* Fix a bug causing the user to be unable to add a new language to Manage Conflicting Processes global settings.
* Refresh the Intune authentication token before retrieving reports from Intune when performing auto-publishing during synchronization.
* Ensure the list of discovered devices with an application only includes unique device matches within the Intune scan wizard.

</details>

## 2.1.103.1 - 2026-03-16

<details>

<summary>Fixes</summary>

* SMTP Oauth Test permission button would only ever account for the first tenant configured.
* Ensure the nth-day-of-the-week option for a monthly sync schedule maps correctly to settings.xml.
* Resolve an issue that causes the Publisher to improperly parse the installation command line for WSUS in some cases. This could result in an update being published with an incorrectly formatted installation command.

</details>

## 2.1.100.380 - 2026-03-06

<details>

<summary>Improvements</summary>

* When selecting the Use Existing App Registration option for SMTP oAuth, you are now given a choice of Intune tenants to choose from.
* Ensure the Publisher gracefully handles the case where the Publisher connection is deleted from the cloud.

</details>

<details>

<summary>Fixes</summary>

* Clicking Browse in the Manage Pre/Post Scripts window would sometimes cause the Publisher to force close.
* The product export feature in the Advanced tab no longer exports duplicate rows for Intune applications and updates.
* Large Intune reports would fail to write to disk, causing an Out Of Memory exception.
* Intune tenant names were not correctly shown in the webhook list under the Alerts tab.
* Fixed a bug where some applications would not be found in the local content cache.
* Ensure the OS requirements are set appropriately for ConfigMgr and Intune Publishing.

</details>

## 2.1.100.328 - 2026-02-24

<details>

<summary>Fixes</summary>

* Update the retry policy to ensure we wait for a sufficient amount of time for Intune to finish processing an intunewin.
* Fix the WMI query used for getting ConfigMgr console folders. In some cases, this would cause a null reference exception in the PatchMyPC.log.
* Resolve a bug causing an exception to be logged "_An error occurred while reporting: An item with the same key has already been added. \[System.ArgumentException] HResult: -2147024809"_

</details>

## 2.1.100.274 - 2026-02-06

<details>

<summary>Improvements</summary>

* Ongoing improvement to UI validation
* Add a tool to compare the publishing history CSV file to the configured tenants' published Intune packages.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug causing Intune packages to publish to an unexpected tenant in some cases when more than one tenant is configured.

</details>

## 2.1.100.241 - 2026-01-30

<details>

<summary>Features</summary>

* ARM Support for ConfigMgr and Intune Public Preview

</details>

<details>

<summary>Improvements</summary>

* Allow editing of the DO priority for multiple assigned applications at the same time
* Allow for SQL queries to take an extended period of time. A ConfigMgrJobTimeout registry key can be set alongside the SQLTimeoutinSeconds. SQLTimeoutinSeconds is limited to 3600 seconds. ConfigMgrJobTimeout is stored in minutes, and is limited to 60 minutes.
* Scanning Intune for Applications using the Intune Scan Wizard was very slow to process. This now runs in the background periodically and uses Caching, but the first scan can still be slow.
* Intune reports now run periodically in the background and cache for 8 hours to improve query speed.
* Update button behavior in WSUS tab to be consistent with other tabs.
* On startup, the Publisher only waits for supported products to be ready now. If catalog data is needed, then a check for catalog preparedness is ran. This improves UI startup after the service is restarted.
* Numeric text box inputs now handle validation on focus lost.

</details>

<details>

<summary>Fixes</summary>

* Loading more groups in the Intune Assignment Group Selector did not load all groups correctly.
* Keep the count of selected and displayed applications in sync in the ConfigMgr and Intune application managers.
* Fixed a bug related to cancelling the override options on the override win32 application options
* Configuring the Move application to custom folder for ConfigMgr apps did not function as intended.
* Ensure the cloud connection displays disconnected after deleting the connection
* Updating an existing Intune Assignment from Required to Available did not work as intended if the modified assignment groups were All Devices and All Users
* The custom backup path in Publishers Advanced tab could not be reset to default.
* Publisher would crash when importing settings that have Migration configured
* Prompt to save the configuration after changing the limiting collection for ConfigMgr database scan to ensure the collection is used for filtering.
* Connecting to Graph to query Assignment groups was slow.
* Select all and select none in the Intune App Manager did not function as intended

</details>

## 2.1.100.148 - 2026-01-16

<details>

<summary>Fixes</summary>

* User-based x86 apps incorrectly had their detection architecture set to x86 instead of x64

</details>

## 2.1.100.129 - 2026-01-15

<details>

<summary>Fixes</summary>

* Detection script architecture was inferred incorrectly
* ARM Products were evaluated by Auto-Enroll rules when ARM private preview feature was not enabled

</details>

## 2.1.100.115 - 2026-01-14

<details>

<summary>Features</summary>

* Publisher support for ARM64 applications in Intune and ConfigMgr (Private Preview)
* Allow Publisher to send emails using OAuth2. This accounts for the deprecation of SMTP Auth in 2026.

</details>

<details>

<summary>Improvements</summary>

* Update Azure naming to Entra
* Converting ConfigMgr connection options form to modern UI Framework
* Converting ConfigMgr app manager to modern UI Framework
* Upgrade the Intune App Manager and Assignment Manager to modern UI Framework
* Publisher now creates Content Folder and Local Content Paths if they do not exist.
* Publisher now supports files that are compressed server-side with either gzip or deflate compression algorithms.
* Converting Base Install Options form to modern UI Framework
* Improve the accessibility of the Conflicting Processes notification. Buttons can now be selected using the Tab key.
* Load all Intune filters and do filtering client-side to improve performance and reduce reliance on graph api.

</details>

<details>

<summary>Fixes</summary>

* Assignment notification setting now saves properly.
* Fixed bug when the Intune retained application was deleted, even though the publish of the new version failed.
* Fixed bug with the show selected button and naming conventions
* More info link in the Intune Extract Package window is linked to the wrong documentation page.
* Updated the temporary location of the settings.xml file during import to allow the file to properly overwrite the current settings.
* Selective Sync was not always correctly processed during a Sync.
* ensured that when treeview refreshes, cached product selections are updated, and the filter to selected products checkbox is correctly reset to avoid confusion.
* Context Menu bug in webhook settings.
* Ensure long-running operations like scanning the ConfigMgr database or loading the list of WSUS updates do not timeout.
* Publisher no longer allows credentials to be provided for the SMS Provider when it is the local machine.
* Double-clicking an Entra group will now correctly show the group members again
* Fixed bug with cloud connection button enablement
* The Publisher will no longer upgrade a retained ConfigMgr application in place. This prevents nested 'Retained Apps' folders from being generated.
* Publisher settings would sometimes be out of sync with the UI, causing apps to not be processed.
* Ensure we populate the list of configured Distribution Point Groups within the ConfigMgr options.
* Prevent the Publisher from indefinitely requesting a cloud access token when the connection has been deleted from the Patch My PC portal.
* The "Run installation and uninstall program as 32-bit process on 64-bit clients" option is now set as expected when needed.
* Folders set for Local Content Path, Content Folder, and Log Folder will all be created if they do not exist.
* Ensure auto-enabled applications and updates have their detection-related properties appropriately set.
* In some cases, restoring the Publisher settings from backup would place files on the desktop unexpectedly.
* Remove the error message when the user exits the cloud connection dialog.
* Ensure the Server and Database names are saved to settings before querying ConfigMgr database in ConfigMgr Scan Wizard
* Fix issues with the filtered view
* Resolve an issue causing the CVE Import Wizard to not load updates.
* Fix the query used when updating dependencies for ConfigMgr applications. This ensure the Publisher appropriately copies forward dependencies when a new version is published.
* Logs can now be collected on a root directory
* Publisher self update release notes linked to an old page.
* No longer possible to configure filters on excluded assignments for Intune apps and updates
* Update the route used when querying, stopping, and starting ConfigMgr components.
* Product selections made in the Intune Scan Wizard did not persist after clicking Save & Close or Apply in Publisher UI.
* Ensure that the limiting collection is saved to settings correctly before querying ConfigMgr
* Fix log save location on the collect logs button to save to selected folder not parent folder
* Fix a bug where ConfigMgr update "Maximum run time" was not used by the Conflicting Processes notification.

</details>

## 2.1.99.247 - 2025-12-18

<details>

<summary>Features</summary>

* ARM64 Application Support in Intune and ConfigMgr (Private Preview)
* OAuth2 Email Support – Publisher can now send emails using OAuth2, preparing for the deprecation of SMTP Auth in 2026 (Docs coming soon)
  * Note: For MSP instances of the Publisher, when the option to 'Use existing app registration' is selected, the first tenant in the list will be used. This will be improved in the future to use each tenant's configured app registration to send email.

</details>

<details>

<summary>Improvements</summary>

* Updated Azure naming to Microsoft Entra
* Converted ConfigMgr Connection Options form to the modern UI framework
* Converted ConfigMgr App Manager to the modern UI framework
* Upgraded Intune App Manager and Assignment Manager to the modern UI framework
* Publisher now creates Content Folder and Local Content Paths if they do not exist
* Added support for server-side compressed files using gzip or deflate algorithms
* Converted Base Install Options form to the modern UI framework
* Improved accessibility for Conflicting Processes notifications – buttons can now be selected using the Tab key
* Performance boost: Load all Intune filters and apply filtering client-side to reduce reliance on Graph API

</details>

<details>

<summary>Fixes</summary>

* Fixed issue where Intune retained application was deleted even if publishing the new version failed
* Corrected More Info link in Intune Extract Package window
* Updated settings.xml import process to properly overwrite current settings
* Fixed Selective Sync not always processing correctly
* Ensured TreeView refresh updates cached product selections and resets filter checkbox
* Fixed Context Menu bug in webhook settings
* Corrected clickable area for Use Existing App Registration checkbox
* Prevented timeouts during long-running operations like ConfigMgr DB scans or WSUS updates
* Blocked credentials for local SMS Provider
* Double-clicking an Entra group now correctly shows members
* Fixed cloud connection button enablement
* Prevented nested folders by stopping in-place upgrades of retained ConfigMgr apps
* Resolved UI sync issues causing apps to not process
* Populated Distribution Point Groups list correctly in ConfigMgr options
* Stopped indefinite cloud token requests after deleting connection from Patch My PC portal
* Corrected 32-bit process option for install/uninstall on 64-bit clients
* Ensured auto-enabled apps and updates have proper detection properties
* Fixed issue where restoring settings from backup placed files on desktop unexpectedly
* Removed error message when exiting cloud connection dialog
* Saved Server and Database names before querying ConfigMgr DB in Scan Wizard
* Fixed dependency query for ConfigMgr apps to copy forward dependencies correctly
* Updated Publisher self-update release notes link
* Corrected route for ConfigMgr component queries and actions
* Fixed Intune Scan Wizard product selections not persisting after Save & Close
* Ensured limiting collection is saved before querying ConfigMgr
* Fixed bug where ConfigMgr update Maximum Run Time wasn’t used in Conflicting Processes notification
* Triggered migration sync after enabling migration
* Fixed issues with filtered view
* Corrected log save location for Collect Logs button

</details>

## 2.1.56.2 - 2025-10-23

<details>

<summary>Improvements</summary>

* Update the way that Scriptrunner executes PowerShell scripts to improve compatibility with WDAC.
* Optimize the payload sent up to Patch My PC Cloud for Migration.

</details>

<details>

<summary>Fixes</summary>

* In some cases, the in-memory instance of settings would become corrupted. Restarting the service would resolve the issue.
  * This resolves issues with syncing Intune products. The bug showed in several ways, but the log lines include an "Object reference not set to an instance of an object"
* Fixed a bug where the Preview version of the Publisher would not install if the WSUS feature was not installed.

</details>

## 2.1.52.2 - 2025-10-16

<details>

<summary>Improvements</summary>

* WSUS Updates can no longer be enabled when no connection to WSUS is available.

</details>

<details>

<summary>Bug Fixes</summary>

* ⁠In ConfigMgr, some OS requirements instances did not have a CI\_UniqueId for some customers. This caused ConfigMgr applications to fail to create.
* Fixed a bug where processing an MSI would extract the MSI installer icons to C:\Temp\Icon.ico.
* Ensure Scriptrunner only deletes the desktop shortcut if requested.
* The Publisher allowed you to save an SMS Provider configuration where the SMS Provider was the local machine, and credentials were provided. You cannot use credentials to connect to a local machine via WMI.
* Ensure the Manage Conflicting Process notification shows the appropriate language for an application update vs. an application install.
* Account for ConfigMgr applications that have content instances with a file size of 0.
* Ensure that newly selected products from a ConfigMgr or Intune scan wizard are correctly displayed in the treeview when filtered to enabled products.
* Ensure that localhost, and similar values such as 127.0.0.1, and . are allowed in the SMS Provider field.

</details>

## 2.1.50.32 - 2025-10-02

<details>

<summary>Fixes</summary>

* Performing a full resync of Migration data from Patch My PC Cloud would cause Publisher's service to crash unexpectedly.
* Fixed a bug causing ConfigMgr console folders to fail to create from within the Publisher UI.
* Fixed a bug where apps would have assignments be listed multiple times when opening DO priority editor with multiple apps selected.
* Publisher would try to connect to WSUS if Publishing WSUS Updates was Disabled.

</details>

## 2.1.50.11 - 2025-09-26

<details>

<summary>Fixes</summary>

* Fixed the URL for some of the More Info links on the Advanced Tab.
* The copy button now shows as expected in the Intune Updates tab when there are no WSUS Updates selected.
* The Publisher will now correctly query the configured SMS Provider, with credentials if provided, when retrieving the list of available SMS Providers.
* Added validation back to Advanced Tab folder fields.
* Ensure folder browse dialogs open at the correct path from the Advanced Tab.

</details>

## 2.1.50.6 - 2025-09-26

<details>

<summary>Fixes</summary>

* Fixed a bug where installing the latest Publisher preview build, 2.1.50.2, would fail when WSUS was not installed on the device - This would affect Intune only and ConfigMgr only customers.

</details>

## 2.1.50.2 - 2025-09-25

<details>

<summary><strong>Improvements</strong></summary>

* Azure secret expiration alerts now display the date, time, and timezone.
* The Manage Conflicting Process branding banner is handled more consistently during a ConfigMgr application sync, with the logo updating for each application if it has changed.
* Validation on the Manage Conflicting Processes globalization form has been enhanced.

</details>

<details>

<summary><strong>Bug Fixes</strong></summary>

* Right-click options no longer appear when interacting with an empty **All Custom Products** treeview node, as no actions are applicable.
* The Migration feature no longer extracts the MSI installer icon to `C:\Temp\Icon.ico`.
* Connecting to the cloud or enabling migration without a configured SMS Provider no longer causes a crash.
* The **Selective sync** option no longer appears checked on vendor or all products nodes based on the state of a previously selected node.
* Hardware and OS requirements now correctly carry forward for Intune applications and updates, including minimum OS, memory, logical processors, and CPU speed. Patch My PC continues to maintain OS architecture.
* Argument validation has been improved in the **Add custom pre/post scripts** form.
* Assignments created in the Intune Dynamic Assignments UI now display correctly without requiring all related forms to be closed.
* Rapidly switching filters and toggling expand/collapse no longer triggers unhandled exceptions.
* Intune Dynamic Assignment Rules now accept names with a single character.
* It's no longer possible to set an Intune naming convention without a token at the All Products or Vendor level, which previously caused all products to share the same name.
* Right-click options now apply to the correct treeview, even when filtered to enabled products.
* Form validation in the Scan Wizards now behaves as expected.
* Return codes for custom applications are now handled consistently within the Publisher UI.
* Custom products no longer incorrectly show as having customized return codes in the right-click menu when none are configured.

</details>

## 2.1.46.2 - 2025-09-18

<details>

<summary>Improvements</summary>

* Improved how Publisher handles multiple ScopeIds when querying SMS\_Application.CI\_UniqueID
* Improved how Publisher handles updating flags for things like Republish and SelectiveSync to ensure that settings.xml does not get overwritten / reset to default.
* Updated CVE links in Publisher reports to link to the new CVE website, [www.cve.org.](https://www.cve.org)
* Improve how selective sync handles selections at the vendor and All Vendors level.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where Publisher would fail to create a ConfigMgr app if the app had previously been deleted but not fully cleaned up by ConfigMgr.
* Fixed a bug where Publisher would still perform a sync if the license had expired in some scenarios.
* Fixed a bug where sorting by Created date in the Intune Filters view did not work.
* Fixed a bug that caused the Intune App Manager window to hang when editing ESP assignments.
* Fixed a bug where Publisher would not correctly write failures due to missing local content to patchmypc.log
* Fixed ability to copy and click links and other data in the Package Details view of applications.

</details>

## 2.1.43.12 - 2025-09-12

<details>

<summary><strong>Improvements</strong></summary>

* Improved column header names in Intune Scan CSV export to match Intune Scan Wizard headers.
* Improved publisher logging for Migration feature to be clearer which application is currently being processed.
* Improved English in Pause Product Updates popup.
* Added additional event handler for Migration to allow full resync to be initiated from Cloud.
* Improved Publisher Migration model to store which version of Patch My PC Publisher inventoried each application.
* Improved grammar in Intune App Manager window.

</details>

<details>

<summary><strong>Bug Fixes</strong></summary>

* Fixed a bug where certain columns in the Intune App Manager window were not read-only.
* Fixed a bug where Migration SignalR hub was not correctly initialized in Migration Helper causing Publisher to not correctly process metadata for ConfigMgr apps
* Fixed a bug where sorting by Date in the Intune Application Manager window would provide inconsistent results with large datasets
* Fixed a bug which caused the Publisher to error when copying ConfigMgr applications. This resolves the error 'Uninstall Content not found in Contents collection.'
* Fixed a bug where sorting by date in the Manage Assignments group selector would provide inaccurate sorting.
* Fixed a bug where the Publisher would refresh the UI before saving, causing settings to not save.

</details>

## 2.1.43.1 - 2025-09-11

<details>

<summary>Improvements</summary>

* Resync the list of applications when a user clicks Apply or Sync Now.
* Improved handling of missing v\_Add\_Remove\_Programs ConfigMgr view in the ConfigMgr Scan Wizard.
* Add an additional SHA1 column that can be added to the Show Package Details window.
* Improved logging to be clearer when settings.xml is read or write-locked for varying operations.
* Improved logging to be clearer when sending test webhook notifications.
* Added additional information in product export CSV.
* Improve handling of postponed apps when apps cannot be copied to target directories.
* %Version% variable now will be used if configured, regardless of the status of global overrides.
* Improved the Publisher email report and logging to better indicate if the local content is outdated and needs to be redownloaded.
* Improved logging to show whether or not the Publisher service is running when opening the UI.
* Allowing selective syncs at the all products level.
* Showing the tenant/app type in the selective sync popup.
* Added tenant column to webhook list in the Alerts tab.
* Minor UI Enhancements/Fixes.

</details>

<details>

<summary>Bug Fixes</summary>

* Fixed an error relating to default language selection in Manage Conflicting Processes.
* Fixed a bug where the column header selection menu would not show for the Webhook list in the Alerts tab.
* Fixing UI bug where user couldn't save webhooks without unselecting one of the scope items.
* Fixed a bug causing inconsistent column widths for Teams webhook notifications.
* Fixed a bug where the Publisher may select the incorrect SMS\_Content instance in some cases when searching for a previous ConfigMgr application.
* Fix bug in teams and email notifications where allusers and alldevices were shown as "excluded"
* Fixed bug where Publisher log would suggest connection to SMS provider had no password when one had been provided.
* Fixed a bug where opening the UI while a sync was running would throw an exception that indicated an error with reading the Settings file.
* Add logic to have Publisher auto-create postponed binaries folders if configured.
* Fixed bug affecting Intune apps export in the Intune App Wizard.
* Fixed a bug where additional text added to the Publisher's email report was too small to read.
* Fixed a bug where new selections from the ConfigMgr scan wizard are not selected in the treeview when you click Ok.

</details>

## 2.1.36.132 - 2025-08-19

<details>

<summary><strong>Bug Fixes</strong></summary>

* Fixed a bug where the list of Non-Migratable Reasons was not correctly initialized, causing the error list sent to the Cloud to be empty.
* Fixed a bug where additional files, folders, and Patch My PC defined pre/post-scripts were not processed when updating existing ConfigMgr applications.
* Fixed a bug where null objects in Migration metadata were not correctly handled.
* Fixed a bug where some Migration file errors were not properly caught and handled.
* Fixed a bug causing Package.xml to be deleted when updating a ConfigMgr application in place.
  * You may see an error similar to 'Object reference not set to an instance of an object' or 'Length cannot be less than zero. Parameter name: length'
  * To fix an affected application, you will need to delete the application and its content, as the Package.xml file is no longer properly populated with a PackageId.

</details>

## 2.1.36.128 - 2025-08-14

<details>

<summary>Improvements</summary>

* Added better error reporting for Migration feature when processing ConfigMgr applications.
* Enabling publisher to allow users to override win32 app options for intune apps and intune updates.
* Updated the process for saving logs to use a SaveAs to allow users to customize the location and filename of the saved logs.
* Enhanced the notifications to include included/excluded status.
* Added a notification to the ConfigMgr scan wizard to notify users when there are SQL errors.
* Improved how Publisher displays information around misconfigured items and items that require manual content to ensure the warning does not consume the entire screen.

</details>

<details>

<summary>Bug Fixes</summary>

* Fixed a bug where detection scripts some times got stuck processing on ARM devices.
* Fixed a bug where publisher did not account for customer publisher license update ring being empty.
* Fixed an issue where Selective Sync (Publish Now) would not take into account postponed configmgr app updates, causing all postponed app updates to be processed regardless of Selective Sync enablement.
* Fixed a bug where Publisher would leave behind files from older versions of an application.
* Fixed an issue where Migration feature could not be enabled.

</details>

## 2.1.36.115 - 2025-08-07

<details>

<summary>Bug Fixes</summary>

* Fixed a bug that caused ConfigMgr applications to fail to publish if the Publisher does not have permission to read device collection information.

</details>

## 2.1.36.111 - 2025-08-06

<details>

<summary>Improvements</summary>

* When enabling Migration in Publisher, send ConfigMgr ScopeId to cloud.
* Added validation to Publisher to ensure apps with over 16MB of metadata only have top level data sent to cloud for migration. (Content will not be hashed and stored)
* Improved new product selection filters performance.
* If an application being processed for Migration has more than 1000 files, mark it as not supported as Patch My PC Cloud has a limit of 1000 files per deployment.

</details>

<details>

<summary>Bug Fixes</summary>

* Fixed a bug where settings could not be saved if product selection filter was active.
* Fixed issue where Migration log file would not incremement in whole numbers. (e.g. 0.1 > 0.2, instead of 1 > 2)
* Fixed an issue where ConfigMgr apps could not be published if the device count could not be read from ConfigMgr.
* Fixed an issue where UI anchors were not set correctly on new icons, causing them to move around the UI.
* Fixed an bug where product selections could not be copied between tabs when the new product selection filter was enabled.
* Fixed an issue where product selection did not persist after a save when the product selection filter was enabled/disabled.

</details>

## 2.1.36.90 - 2025-07-16

<details>

<summary>Features</summary>

* Add support for ECDSA code signing certificates.

</details>

<details>

<summary>Improvements</summary>

* Add a filter button to only show products that are selected in the Publishers UI.
* Trigger search in Entra ID Group Search window when pressing Enter key.
* Present a warning when importing a code signing certificate if ConfigMgr is set to automatically manage your code signing certificate.
* Improve performance when Publisher is processing ConfigMgr apps for migration.
* Add additional fields, related to user install statistics, to the Intune Application Manager.
* Modernised the icons in the Publishers UI.

</details>

<details>

<summary>Fixes</summary>

* Fixed issue where ScriptRunner was not correctly appending MSI and MSP installers with /qn (Introduced in Preview release 2.1.36.80)

> \#### Remediation Options:
>
> To resolve this issue, please choose one of the following options:
>
> 1\. \*\*Update to the latest Preview Release (Version 2.1.36.90)\*\*
>
> 1\. In the Publisher, navigate to the About tab.
>
> 2\. You may already have the "Install preview builds" option checked \*\*(1)\*\*
>
> 3\. If the "Currently Installed Version" is 2.1.36.80 \*\*(2)\*\* and the "Latest Available Preview Version" is 2.1.36.90 \*\*(2)\*\*, click "Upgrade Now" \*\*(3)\*\*\\
>
> \\
>
> \_\*\*Note:\*\* If the "Install preview builds" option is not checked \*\*(1)\*\*, please check it and click "Apply" and version 2.1.36.90 will be offered. You can now select "Upgrade Now"\_.<br>
>
> 2\. \*\*Roll back to the latest Production Release (Version 2.1.36.0)\*\*\\
>
> If you do not wish to remain on the Preview Release channel, uncheck the "Install preview builds" checkbox on the About tab in the Publisher and click "Apply".
>
> 1\. Download the latest Publisher production release from [https://patchmypc.com/msi](https://patchmypc.com/msi)
>
> 2\. Follow [this guide](https://patchmypc.com/kb/backup-restore-publisher-settings/#h-backup-the-publisher-settings) to create a backup the Publisher settings (not required to roll back but recommended)
>
> 3\. Uninstall Patch My PC Publisher from Add/Remove Programs (your settings will be preserved)
>
> 4\. Install the Publisher production build MSI you downloaded in step 1
>
> \*\*Important:\*\* Regardless of the option you choose, you will need to \*\*re-publish any applications that were published using version 2.1.36.80\*\* to ensure the correct installation parameters are applied.
>
> If you need assistance or have any questions, please visit our Technical Support page at [https://patchmypc.com/technical-support/](https://patchmypc.com/technical-support/) to open a support case.

</details>

## 2.1.36.80 - 2025-07-09

<details>

<summary>Features</summary>

* Migration from ConfigMgr to Patch My PC Cloud.
  * Read only for Enterprise+ customers.
  * Read/Write for Enterprise Premium customers.
* Add a progress bar to the Publisher UI. It will display the current application or update being processed.

</details>

<details>

<summary>Improvements</summary>

* Ensure the scrollbar on the Intune application scan wizard only shows when needed.
* Improve the logging of PowerShell-based detection and requirement script signing.
* On new installs the PatchMyPC.log file is stored in the Logs subfolder of the installation directory.
* Write the name of the account used to run PatchMyPCService to the publishers log file.
* Amended the rolled over log file extension from .lo\_ to .log.
* Log username of active user when using Manage Conflicting Processes to kill processes.
* Improved logging when ScriptRunner calls PowerShell scripts.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused [Manage Conflicting Processes](https://patchmypc.com/kb/manage-conflicting-processes-when-updating/) to fail to close running applications in some scenarios.
* Fixed the URL for the Patch My PC logo in webhook alerts.
* Fixed a bug that would allow a configuration of maximum application runtime that conflicted with the Manage Conflicting Process notification runtime.
* Fixed a bug that caused the filtering of Intune groups to hang the UI
* Fixed a bug where rolled over log files were not cleaned up according to retention settings.

</details>

## 2.1.36.35 - 2025-06-12

<details>

<summary>Improvements</summary>

* Add an [IntuneReportsRequestTimeout registry option](https://patchmypc.com/kb/registry-publisher-config#h-change-the-timeout-for-intune-reports) to set the timeout for Intune reports. The default value is five minutes.
* Update tooltips in the Publisher UI for Manage Conflicting Process timeouts to reflect Intune changes.
* If the code signing certificate is not found, then WSUS updates will not process.
* If the code signing certificate is not found and ConfigMgr detection script code signing is enabled, then ConfigMgr apps will not process.
* Improve the handling of UINotificationSettings.xml for Manage Conflicting Processes. They are now generated per session.
  * XML per session prevents access denied errors that can occur when one user creates a file and another non-admin user later attempts to edit it.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where the Publisher may select the incorrect SMS\_Content instance in some cases when searching for a previous ConfigMgr application.
  * This fix addresses the alert “Unable to process \<Application Name>. PackageId… does not find an application with a matching content source path…”
  * Refer to this [KB article](https://patchmypc.com/kb/packageid-found-does-not-find-an-application-with-matching-content-source-path/) for more information.
* Fixed a bug that caused customers to see an error message if ScriptRunner tries to display a notification while Focus Assist is enabled.
* Fixed a bug that caused Postponed binaries to fail to process when custom applications are enabled and the PostponedBinaries folder does not exist.

</details>

## 2.1.35.23 - 2025-04-29

<details>

<summary>Improvements</summary>

* When processing a ConfigMgr app, the Publisher will validate that the PackageId found in a package.xml maps to an application deployment type with a matching content source path.
* If a ConfigMgr application copy fails, the left-behind content is also removed.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused the MCP User Notification Timeout not to be translated from minutes to seconds when written to package.xml. The result is a notification being open for 5 seconds instead of 300 seconds, for example.
  * Note: To fix existing apps or updates with this issue [Republish the App or Update](https://patchmypc.com/when-and-how-to-republish-third-party-updates).
* Fixed a bug that resulted in an error when attempting to save a MCP User Notification Timeout Setting.
* Fixed a bug that caused postponed custom ConfigMgr applications to not publish as expected.
* Fixed a bug where the option to select the ConfigMgr folder within the [ConfigMgr application creation options ](https://patchmypc.com/application-creation-options)was unavailable.

</details>

## 2.1.33.44 - 2025-4-9

<details>

<summary>Improvements</summary>

* Allow a maximum run time of 1440 minutes for Manage Conflicting Processes for Intune.
* Add the user name, user domain, device name, session ID and Windows OS version to the PatchMyPC-Sriptrunner.log.
* Collect additional information regarding certificate validation failures.
* Add Japanese localization text for Manage Conflicting Processes.
* Stop processing a ConfigMgr application if the copy operation for retention fails. This ensure we do not edit an existing app unless the copy succeeds.
* Added the total sync time to the PatchMyPC.log
* Improved logging when there is a cloud connection, but no Intune deployments in the cloud.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused some right-click options, such as setting an update to metadata only, to take a long time to apply when set at the ‘All Products’ level.
* Fixed a bug that caused the Publisher to fail to load the complete list of selected products from settings.
* Fixed a bug causing the Publisher to fail to process selections from the CVE Import Wizard.
* Fixed a bug that caused the treeview searchbox not to retain the previous search text.
* Fixed a bug causing scriptrunner not to expand placeholder arguments such as %CURRENTDIR% when parsing command line arguments.
* Fixed a bug causing errors similar to ‘Mutex access requested by GetIntuneAppProductFlags but a timeout occurred while waiting for mutex to be released’
* Fixed a bug that caused custom applications to fail if they had two files with the same name inside their content.

</details>

## 2.1.29.60 - 2025-1-17

<details>

<summary>Features</summary>

* Scriptrunner will now expand environment variables provided in custom command line arguments and pre-post script arguments. Additionally the below variables are available.
  * %PRODUCTNAME%
  * %VERSION%
  * %VENDORNAME%
* Add support for Patch My PC to configure the ‘Run installation and uninstall program as 32-bit process on 64-bit clients’ option within ConfigMgr. This will not be a customer exposed option in the Publisher, but something that Patch My PC can set to ensure applications install as expected.

</details>

<details>

<summary>Improvements</summary>

* The search functionality in the product treeviews now consider custom applications. Previously the list of custom products would not be included in the search.
* Improved logging during a Publisher synchronization for products that are marked [end-of-life](https://patchmypc.com/how-products-are-handled-at-end-of-life-eol-or-become-incompatible) by Patch My PC.
* Update some labels and logging to be in line with the latest terminology used in Intune.
* The Update ID and Update Title are now written to the PatchMyPC-Scriptrunner log file.
* The username of the user who performed a save in the Publisher is now written to the event log, and to the PatchMyPC log file. Additionally an empty file with a GUID name is included in the CAB so the save event can be matched to CAB file.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused the service not to start if no settings.xml file existed.
  * This only impacted preview builds and did not ship to production.
* Fixed a bug where the metadata of the settings backup CAB file was using absolute paths, making the CAB appear empty when viewed through Windows explorer.
  * This only impacted preview builds and did not ship to production.
* Fixed a bug where cloud Product Selections were only displayed in the Publisher if the product was both deployed in the cloud, and selected in the Publisher. Products which are not selected in the Publisher will now properly show as managed by the cloud if a deployment exists.
* Fixed a bug causing the CVE Import tool not to load.
  * This only impacted preview builds and did not ship to production.

</details>

## 2.1.29.42 - 2024-12-19

<details>

<summary>Features</summary>

* Support applications in the catalog that download a zip file.
  * Idea: [PATCHMYPC-I-1463](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1463)
  * Note: Additional backend and procedural changes are needed before this will be used. The Publisher can consume a catalog with software that downloads a zip file. We will not add any products like this until Q1-Q2 2025.

</details>

<details>

<summary>Improvements</summary>

* Improve how the Publisher reads and writes settings.
  * Prevent the Publisher from overwriting user setting changes while a sync is happening. Previously, if a user was in the UI and clicked save while a sync was running, the user’s changes could be lost.
  * Prevent the Publisher from losing Intune configuration due to an abandoned mutex.
* If found, the ‘Collect Logs’ button will now include the WSUS softwaredistribution.log.
* Improve the product search function in the Publisher to keep the search box open when no match is found.
* Scriptrunner has improved logic for handling the log location for user-based installations. If the default values are left in the Publisher, the log path will be updated to a user-writable location. This includes the scriptrunner log and the installer log.
* Updated Publisher settings backup retention to retain settings from previous weeks and months.
* Update the Swedish translation for Manage Conflicting Processes based on customer feedback.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where Graph queries would fail if they contained a date-time filter and the machine running the Publisher had the OS set to specific cultures.
* Fixed a bug where a ‘BaseInstallOnlyNotForUpdating\_’ prefix would appear when using the %OriginalName% variable.
* Fixed a bug where an invalid logging path was allowed, causing the Publisher not to log anything to disk.
* Fixed a bug where canceling out of the Dynamic Assignments form would still apply the settings.
* The test email for SMTP configuration had a blank subject and body.
* Fixed a bug causing the Manage Assignments form to hang while resolving Entra group names in some scenarios.
* Fixed a bug where the Publisher would include non-Windows applications in the scan results for Intune auto publishing.
* Fixed a bug that caused webhook summary notifications not to respect the tenant filter.
* Fixed a bug that caused the Publisher to attempt to code sign Patch My PC defined scripts when the code signing option was disabled in the Publisher.
* Fixed a bug that caused the install time offset for Intune assignments to be displayed incorrectly in some cultures.

</details>

## 2.1.28.9 - 2024-10-25

<details>

<summary>Fixes</summary>

* Revert changes in Scriptrunner for the execution of PowerShell scripts. The scripts will be called using the -File parameter.
  * The changes that improve WDAC support will be re-evaluated for a future release.
  * Note: Products published with version 2.1.28.6 Scriptrunner may not correctly execute PowerShell scripts with arguments.
* Revert the changes for translating Manage Conflicting Process notifications by default. We are returning to the original behavior. It will not be translated if the customer does not include a language in their configuration.

</details>

## 2.1.28.6 - 2024-10-24

<details>

<summary>Improvements</summary>

* The Win32AppId is now included in the PatchMyPC-PublishingHistory.csv file.
* Improved the handling of signed scripts when publishing. Sometimes, the Publisher would fail to replace a file and throw an exception. We now ensure the destination file is deleted before moving in the updated file.
* Scriptrunner now calls PowerShell scripts without using the -File parameter. This improves compatibility in environments that use WDAC.

</details>

## 2.1.28.2 - 2024-10-03

<details>

<summary>Improvements</summary>

* Intune Updates will now have the icon for the product associated with them.
* If the customer does not provide translations for a given language and this language is pre-translated by Patch My PC, we use those strings when we display the UI notification for [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications).
  * This results in the default behavior of the notifications being translated to the locale of the device if Patch My PC provides a translation.
* Added Czech, Finnish, and Norwegian translations for [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications).
* Fixed Danish translation for [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications).
* Imported banner images are stored in the installation directory of the Publisher instead of referencing the source file.
* Removed the references for the SSRS reports and replaced them with [Advanced Insights](https://patchmypc.com/advanced-insights/overview).

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused the synchronization to stop if a tenant failed authentication. This impacted Publisher with an MSP license and a multi-tenant setup.
* Fixed a discrepancy between the PowerShell detection scripts and the ScriptRunner detection logic.
* Fixed a bug with the filtering options for webhook notifications. The notifications should now be correctly filtered when the summary option and scope are set. For example, ‘Send alerts as each product is published…’ is unchecked, and only ‘Include Intune update notifications’ is checked.

</details>

## 2.1.26.7 - 2024-08-29

<details>

<summary>Improvements</summary>

* Add support for passing additional headers when downloading binaries. This is metadata maintained by Patch My PC.

</details>

<details>

<summary>Fixes</summary>

* Update Intune detection to account for registry detection checking for a nonexistent property. We now allow a NotEquals check for a property that might not exist. Previously, this would cause an unhandled exception.

</details>

## 2.1.26.5 - 2024-08-07

<details>

<summary>Features</summary>

* Added support for Microsoft Teams Workflows as a new webhook provider option. With the announced [retirement of Office 365 connectors within Microsoft Teams](https://devblogs.microsoft.com/microsoft365dev/retirement-of-office-365-connectors-within-microsoft-teams/), we now support the new Workflow options. Our Teams notifications have been updated with new ⁠[Adaptive Card](https://learn.microsoft.com/en-us/adaptive-cards/) templates.

</details>

<details>

<summary>Improvements</summary>

* Configured [return codes](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#manage-return-codes) are updated on sync for ConfigMgr applications, Intune applications, and Intune updates. If there is a mismatch between the settings in the Publisher and the published application, then the return codes from the settings will be applied. It is no longer necessary to republish a product to update the return codes.

</details>

<details>

<summary>Fixes</summary>

* Fix a bug that caused republishing a custom ConfigMgr application with additional files to fail in some scenarios.
* Fixed a bug where the return codes in settings could be duplicated if the treeview was refreshed, or you switch tenants in a multi-tenant setup.

</details>

## 2.1.24.7 - 2024-06-14

<details>

<summary>Features</summary>

* Manage return codes
  * Idea: [PATCHMYPC-I-556](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-556)

</details>

<details>

<summary>Improvements</summary>

* Use a temporary staging directory for binary downloads when processing ConfigMgr applications
* Improved handling of the cloud connection.
* Improved how ConfigMgr content is resolved to ensure we choose non-retained applications if present.
* The tooltip and icon for Manage Conflicting Processes suggested configurations are now more contextual.
  * If configured to Kill or Notify, the tooltip and icon are removed
  * If configured to Skip, the icon is shown, and the tooltip says, “Manage Conflicting Processes is recommended for this product and will be configured to Skip by default”
  * If configured to ‘Perform the installation,’ the icon is shown, and the tooltip says, “Manage Conflicting Processes is recommended for this product but is currently not configured”

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused the ‘Prevent the end-user from opening an application while the application is updating’ feature to not work for ConfigMgr or Intune applications in some instances.

</details>

## 2.1.22.25 - 2024-05-21 <a href="#features" id="features"></a>

<details>

<summary>Features</summary>

* Implement coexistence
  * Coexistence ensures the customer is aware when a product is already managed by Intune Apps for Patch My PC Cloud.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused a circular reference when processing Intune dependency relationships with greater than 2 layers.
* Fixed a bug that caused ConfigMgr applications to be copied for retention even if the current version fails to download.
* Ensure proper wildcard support for ? in detection.

</details>

## 2.1.22.7 - 2024-04-30 <a href="#features" id="features"></a>

<details>

<summary>Features</summary>

* Support for ‘Allow available uninstall’ in Intune
  * Idea: [PATCHMYPC-I-3213](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-3213)

</details>

<details>

<summary>Improvements</summary>

* Improve our regex usage in the detection of applications published by Patch My PC.
  * The regex string is now stored in base64 in the PowerShell script to prevent Intune from clobbering UTF8 characters.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused custom applications with a main file larger than 2GB to fail to process.

</details>

## 2.1.21.13 - 2024-04-03 <a href="#features" id="features"></a>

<details>

<summary>Features</summary>

* It is now possible to adjust the chunk size used for uploading chunks to Azure. It can be [adjusted between 2MB and 12MB](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#AzureUploaderChunkSize).

</details>

<details>

<summary>Improvements</summary>

* PowerShell detection scripts no longer call whoami. This resolves issues where the PATH environment variable may have conflicting whoami processes.
  * The ‘[recreate detection](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#RecreateDetection)‘ right-click option can be used to generate new scripts with this change. Otherwise, products will have the script updated when a new version is released.
* Product selections are stored and matched based on a product Id
* A message box will appear when a ‘[latest](https://patchmypc.com/products-multiple-versions-patch-my-pc#topic2)‘ product is selected. This message box contains a brief note about how products with multiple versions are handled and provides a help button for [more info](https://patchmypc.com/products-multiple-versions-patch-my-pc#topic2).
* Improve how we search for ConfigMgr application content.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused a null reference exception if a recommended pre script, and a recommended post script were configured on a product.
* The configured proxy will be used to get an access token during cloud connection creation.
* Disconnecting from the cloud tab did not save to settings.

</details>

## 2.1.21.2 - 2024-03-20 <a href="#features" id="features"></a>

<details>

<summary>Improvements</summary>

* When creating the cloud connection in the Publisher, the System Default browser will now be used.
  * If needed, the embedded web browser can still be used with a [registry flag](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#MsalUseEmbeddedWebView).
* The ‘[Collect Logs](https://patchmypc.com/logging-options#collectlogs)‘ button now collects all PowerShell detection scripts modified within the last 7 days. The scripts are renamed to have a .txt extension before being added to the zip file.
* Icons in the product treeview now indicate if the product requires local content, or is configured to skip the install if running by default.
  * ![image (2).png](<../../.gitbook/assets/image-(2) (1).png>)

</details>

## 2.1.20.2 - 2024-02-27 <a href="#features" id="features"></a>

<details>

<summary>Fixes</summary>

* Cloud features were not using the configured proxy. The proxy configured in the Publisher will now be used.

</details>

## 2.1.19.33 - 2024-02-15 <a href="#features" id="features"></a>

<details>

<summary>Improvements</summary>

* Use less memory when uploading .intunewin files to Intune.
* Improve the user experience when the ConfigApi is not available
  * The UI can now start without the ConfigApi being available. A popup message will still appear indicating it cannot be reached.
  * When this is not available, the cloud features of the Publisher will be disabled.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused some right-click options to not clear their state as expected for custom apps.
* Editing Manage Conflicting Process options did not light up the Apply button.
* Fixed a bug that caused the Publisher to fail to retry when uploading chunks to Azure.
* Fixed a bug where a custom application download may compare hash against an older version of the custom application’s hash.

</details>

## 2.1.19.22 - 2024-02-02 <a href="#features" id="features"></a>

<details>

<summary>Improvements</summary>

* Improve how the list of custom products is queried from the cloud.
* Improve the cloud connection flow to account for the EU region.
* Various typo corrections in the UI and in the log.
* Improve logging for retained ConfigMgr applications.
* Expand out aggregate exceptions when they are logged.
* Improved user experience both for a disconnected cloud configuration and an empty custom app list.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that made connecting to an EU Patch My PC cloud customer inconsistent.
* Fixed a bug causing the copy between tab options not to work as expected when custom applications are configured.
* Fixed a bug where ESP associations would copy between the Intune Apps and Intune Updates tab.
* Improved how .intunewin files are handled to ensure we can process large files.

</details>

## 2.1.18.55 - 2023-12-22 <a href="#features" id="features"></a>

<details>

<summary>Improvements</summary>

* Implement an attempted reconnect when a WMI query fails against the SMS provider.
* Improved scriptrunner logic for finding uninstall strings. DisplayVersion will now have any "-" or "\_" replaced by a "." when searching for uninstall strings. This matches the behavior of our script based detection.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused a Null Reference Exception when exiting the [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) configuration in the Intune apps or Intune updates tab.
* Fixed a bug that caused the [custom naming convention](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#IntuneNamingConvention) for ConfigMgr applications to be overwritten during a sync in some cases.
* Fixed a bug where the authorization token can expire when connecting to Custom Apps, requiring a service restart.
* Fixed a bug where Right-Click selections for "All Products" on the "Intune Apps" tab would be lost when custom apps was enabled.

</details>

## 2.1.18.48 - 2023-12-08 <a href="#features" id="features"></a>

<details>

<summary>Features</summary>

* Ability to create Custom App updates and base installs
  * Idea: [PATCHMYPC-I-1303](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1303)
  * [Setup docs](https://docs.patchmypc.com/installation-guides/preview-custom-apps)
  * The feature is in public preview.
  * Custom Applications are supported in the ConfigMgr apps, Intune apps, and Intune updates tabs.
  * The Publisher must have ‘[Install preview builds](https://patchmypc.com/preview-channel)‘ checked in the About tab.
  * A license with one of the below subscription levels is required.
    * Enterprise Plus
    * Enterprise Premium
    * MSP

</details>

<details>

<summary>Improvements</summary>

* Update the default login authority for Intune. It is now [https://login.microsoftonline.com](https://login.microsoftonline.com/)
  * This will not affect existing Intune configurations. It is only a change to the defaults for a new connection.

</details>

<details>

<summary>Fixes</summary>

* Fix logging during the creation of Intune products when local content lookup fails. The Publisher would incorrectly log that the existing application would be deleted.
* Fixed a bug causing Enforced Uninstall Arguments to be ignored for ConfigMgr apps. This resulted in some ConfigMgr apps being created with an uninstall that may not work as expected. The next sync after the Publisher is updated will fix these products’ uninstall configuration.
* The connection name is now required in the Cloud tab.

</details>

## 2.1.18.42 - 2023-12-05

<details>

<summary>Features</summary>

* Add support for configuring Win32 application max runtime in minutes

</details>

<details>

<summary>Improvements</summary>

* \*\*\* Report lines have been updated.
  * As the catalog grows and the number of syncing products increases, our \*\*\* report line has gotten too long! CMTrace does not parse the line, and it will not show it. To prevent this, we have split up the report line into one line per type. Below is an example.
* Implement certificate pinning. All requests to Patch My PC domains will have the certificate validated.
* Implement a safety check prior to deleting a ConfigMgr application. In some instances, the SMS provider returns an empty list of apps instead of a connection exception. To account for this we ensure at least one Site is returned by the SMS provider prior to application deletion.
* ConfigMgr script size is reduced. No functional changes. This should help with metadata download issues over CMG.
* Add support for the ? wildcard character in detection.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused a new install of Patch My PC Publisher to be in ‘Intune Only Mode’ regardless of the checkbox state.
* Servers are no longer included in Intune device counts.
* Resolved a race condition which caused the additional webhook filtering options to be unavailable in some instances.
* Improved download engine logging to include the URL when the download fails. This was a regression that is now resolved.
* The logging path for Intune [Manage Installation Logging](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#install-logging) incorrectly defaulted to the ConfigMgr path. It is now corrected to the Intune default path for logging.
* For some sync schedules, the ‘Next Sync’ time displayed in the General tab was in UTC instead of local time. The correct time should now be displayed.

</details>

## 2.1.18.27 - 2023-11-07

<details>

<summary>Features</summary>

* Support detecting software that translates DisplayName
  * Idea: [PATCHMYPC-I-1335](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1335)
* Implement Publish Now for Custom Apps

</details>

<details>

<summary>Improvements</summary>

* Improve some popup notifications to direct the user to the correct tab.
* Improve cleanup during service shutdown.

</details>

<details>

<summary>Fixes</summary>

* Fixed a dead ‘More Info’ link for WSUS certificate management.
* Fixed a bug causing dependencies to be removed from an Intune Win32 application when republishing.
* Fixed a bug where publish now and delayed ConfigMgr apps did not work as expected.

</details>

## 2.1.17.27 - 2023-09-29

<details>

<summary>Improvements</summary>

* OK button has been changed to ‘Save and Close’
  * Open to feedback on this change. We have received a fair number of reports that it is unclear the ‘OK’ button will close the UI.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where multiple threads could access some components of settings at the same time, causing a race condition.

</details>

## 2.1.17.11 - 2023-09-14

<details>

<summary>Fixes</summary>

* Fixed a bug where the 'Change Visibility' option for WSUS updates would not work if the WSUS DB is called something other than SUSDB.

</details>

## 2.1.16.59 - 2023-09-01

<details>

<summary>Improvements</summary>

* Improve cleanup of files during the synchronization of Intune.
* Updated the “Enabled” header of CSV exports in scan wizards to be less specific.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused the right-click menu at the root to sometimes not display correctly.
* Fixed a bug with ‘Selective Sync’ where Intune Apps and Intune Updates were swapped
  * This would not cause the wrong thing to be published, but it might cause something to not be published at all during a selective sync.

</details>

## 2.1.16.54 - 2023-08-29

<details>

<summary>Features</summary>

* Sync only selected apps/updates during a sync
  * Idea: [PATCHMYPC-I-468](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-468)

</details>

<details>

<summary>Improvements</summary>

* Implement a new download engine across all components.
* Detection method improvements.
  * Support parsing version numbers that use – or \_ instead of .
* Improved logging regarding installer downloads and sourcing.
* Use CSV-based reporting endpoints for detected software per-computer.
  * This should prevent 429 responses when getting the list of devices with an application.
* WMI connection test to SMS provider prior to deleting ConfigMgr content.

</details>

<details>

<summary>Fixes</summary>

* On the ConfigMgr Apps tab, if the option «Add the executable name in the deployment type’s install behavior» is enabled, the Manage Conflicting Process is automatically enabled to kill processes.
* Fix crash when sorting some columns in the [Manage Assignments tool](https://patchmypc.com/intune-application-manager-utility).
* Fixed a bug that would cause a republished Intune product to have the content for the latest version, and the metadata for version n-1.
  * This would occur if the republish flag is set, and there is new version of the application in the catalog.
* The list of Intune assignment filters is now filtered to Windows.
* Fixed a bug where in some scenarios the republish flag would not be removed after a sync.
* Fix a possible null reference exception when loading assignments for bulk delivery optimization edits.
* Fixed a bug where the custom logging path maybe reset to defaults instead of inheriting the expected value.

</details>

## 2.1.16.16 - 2023-08-04

<details>

<summary>Features</summary>

* Allow the management of Delivery Optimization configuration for Intune assignments.
  * Idea: [PATCHMYPC-I-2071](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2071)
  * Note: Existing DO configuration on an assignment will also carry forward now when a new version of the software is Published.
* The [Intune Application Manager Utility](https://patchmypc.com/intune-application-manager-utility) now has some multi-select bulk options.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where the wrong ID property was shown in the ‘[Show Package Info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo)‘ tool for the update ID.
* Fixed a bug where Manage Conflicting Processes may be enabled if [‘Add the executable name in the deployment type’s install behavior’](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#install-behavior) is enabled. This is unexpected behavior that will no longer occur.

</details>

## 2.1.15.3 - 2023-06-16

<details>

<summary>Improvements</summary>

* Update the Intune [Application Manager Utility](https://patchmypc.com/intune-application-manager-utility) to use the [aggregate reports](https://learn.microsoft.com/en-us/mem/intune/fundamentals/reports-export-graph-available-reports) for both the collection of applications, as well as application extended info. This prevents a 429 when retrieving the data.

</details>

<details>

<summary>Bug Fixes</summary>

* Updated Publisher to reflect changes in Graph API schema. This should resolve issues with the [Patch My PC Intune reports](https://patchmypc.com/power-bi-reports-for-microsoft-intune-third-party-updates).

</details>

## 2.1.14.21 - 2023-06-02

<details>

<summary>Improvements</summary>

* Updated the [Intune Scan Wizard](https://patchmypc.com/scan-intune-for-supported-products) to use [graph report export endpoints](https://learn.microsoft.com/en-us/mem/intune/fundamentals/reports-export-graph-available-reports). This will prevent the Publisher from getting a 429 return code when scanning for discovered applications.
* The product treeviews are now sorted by Vendor and then Product Name automatically.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where the sorting of products in the email report was in reverse alphabetical order.

</details>

## 2.1.14.11 - 2023-05-17

<details>

<summary>Improvements</summary>

* Updated some graph calls to use a smaller page size. This reduces the chance of receiving a 429 or 503 response from graph.
  * The page size is configurable from 1-999 in the Advanced tab of the Publisher.

</details>

## 2.1.14.8 - 2023-05-16

<details>

<summary>Features</summary>

* Add support for .cmd files in pre/post-scripts.
  * Idea: [PATCHMYPC-I-2745](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2745)

</details>

<details>

<summary>Improvements</summary>

* The Update ID is now an available column in the [Show package info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo) tool.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where a ConfigMgr application’s supersedence relationship was lost when the application was upgraded in place.

</details>

## 2.1.13.6 - 2023-04-04

<details>

<summary>Improvements</summary>

* Adjusted log levels of some lines to assist with troubleshooting.
* Update context menu items to reflect new labels in ConfigMgr for featured apps.
* Update several labels in the UI to be more clear on their functionality.
* The ability to set ‘Prevent the end-user from opening an application while the application is updating’ is now only allowed at the per-product level. This setting is only needed in specific scenarios, and enabling it for all products can be problematic.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where Intune device counts are not reporting properly.

</details>

## 2.1.12.33 - 2023-03-08

<details>

<summary>Features</summary>

* Add support for creating an Available assignment for All Devices. This was previously not supported by Intune. Support has been added, and the Patch My PC UI now allows it as well.

</details>

<details>

<summary>Enhancements</summary>

* Added the option to import CAB files when importing tenants.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where an exception may occur if deleting a large number of Intune Applications using the Intune Application Manager Utility
* Fixed a bug where some data exports would result in malformed date time strings. This occurred if a culture used the same character for the number group separator and for time parts.
* Fixed a bug where ConfigMgr detection script logging did not use an invariant date-time format. This could cause CMTrace to fail to parse the logs.
* Fixed a bug where Manage Conflicting Process logging did not use an invariant date-time format. This could cause CMTrace to fail to parse the logs.
* Fixed a bug where the option to abort an uninstall if the prescript failed caused an argument parsing exception.
* Fixed a bug where the automatic backup of setting changes would fail in certain cultures due to a date-time parsing issue.
* Fixed a bug where custom naming conventions were copied between tabs. We no longer copy naming conventions when copying products between tabs.

</details>

## 2.1.12.22 - 2023-01-31

<details>

<summary>Features</summary>

* Email and Webhook notifications now include information about delayed ConfigMgr applications during each sync.
  * Idea: [PATCHMYPC-I-1862](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1862)

</details>

<details>

<summary>Improvements</summary>

* Email and Webhook notifications are now sent when a delayed ConfigMgr application fails to download. Previously a notification would only happen if the Publishing failed after the delay.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where PowerShell scripts for Intune were created with an encoding of UTF8 with BOM. They are now encoded as UTF8 without BOM, which is the recommended encoding based on [Microsoft documentation](https://learn.microsoft.com/en-us/mem/intune/apps/apps-win32-add).
* Fixed a bug where a malformed ConfigMgr folder item (SMS\_ObjectContainerItem) would be created the first time the Publisher moved a ConfigMgr application. The result was a folder that could never be deleted.
* Fixed a bug where having a product marked with [exclude from auto-publishing rules](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#exclude-from-scanning) and a [custom naming convention](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#IntuneNamingConvention) or [pause](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#pause-product-updates) set would cause invalid XML to be generated.
* Fixed a bug where the Collect Logs feature would fail if a company name contained characters that are invalid for file names.
* Fixed a bug where PatchMyPC Scriptrunner logging did not use an invariant datetime format. This could cause CMTrace to fail to parse the logs.

</details>

## 2.1.11.10 - 2023-01-06

<details>

<summary>Features</summary>

* Intune option added to ‘Copy requirements’ for Intune products. This can be configured globally, per vendor, or per product.
  * Idea: [PATCHMYPC-I-1501](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1501)
* Recreate Detection right-click option for Intune
  * Idea: [PATCHMYPC-I-2605](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2605)

</details>

<details>

<summary>Improvements</summary>

* If a PMPC-defined pre or post-script is missing from the content source for ConfigMgr applications then the Publisher will redownload it during a sync, or republish.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where non-Windows devices may show up in the [Intune scan wizard](https://patchmypc.com/scan-intune-for-supported-products) drill-in.
* Fixed a bug where republishing an Intune product would cause the application to be deleted from Intune if retention was also enabled and set to zero.
* Fixed a bug where the Publisher would not check the WSUS certificate validity unless at least one WSUS update was selected.
* Fixed a bug where the requirements for Workstation or Server OS would not be set for postponed ConfigMgr applications.

</details>

## 2.1.11.2 - 2022-12-20

<details>

<summary>Features</summary>

* Enable Right-Click Options for MSP based updates
  * Idea: [PATCHMYPC-I-614](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-614)

</details>

## 2.1.10.9 - 2022-12-06

<details>

<summary>Improvements</summary>

* Improved the content of alerts when additional files or folders are missing when Publishing a product
* The ‘Configure SMS Provider connection’ button is no longer highlighted if unconfigured in WSUS Standalone Mode.
* Improved the logging for SMTP initialization and error handling.
* All titles in the email report now link to release notes if available.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where the Publisher would not add a PMPC-defined script to an existing product.
* Fixed a bug where Scriptrunner did not append the provided Silent Uninstall Arguments to MSI uninstalls.
* Fixed a bug where some UI listviews had a broken filter.
* Fixed a bug where Manage Conflicting Process window may be offset from the bottom right corner.

</details>

## 2.1.9.27 - 2022-11-07

<details>

<summary>Improvements</summary>

* Improved how running processes are enumerated for [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) making the popup more responsive.
* Implemented a ‘retry’ in the event of failure for many critical interactions with Azure via Microsoft Graph.
* The Publisher will delete files from the download cache if there is a hash-mismatch for the file. This makes the root cause of Publishing failure easier to identify.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where the [UseGSInstalledSoftware](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#topic3) registry option would cause the ConfigMgr database scan to never perform a query.
* Fixed a bug where a failure to download an icon would cause a product to fail to publish.

</details>

## 2.1.9.17 - 2022-10-27

<details>

<summary>Improvements</summary>

* Add the ability to limit the number of threads used during the upload of Intune packages.
  * [Documentation](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#AzureUploaderMaxThreadCount)
* Adding more logging around proxy configuration and failures.
* Scriptrunner will now log out a comma-separated list of all public desktop shortcuts if the installing product is configured to delete desktop shortcuts.
  * This is to help troubleshoot when icons for applications are not deleted.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where some network operations would not use the configured proxy.
* Fixed a bug where the code signing of ConfigMgr detection scripts may fail to validate the digital signature on the endpoint.

</details>

## 2.1.9.7 - 2022-10-21

<details>

<summary>Improvements</summary>

* Added a filter for Superseded to the [Modify Updates Wizard](https://patchmypc.com/modify-published-third-party-updates-wizard).
* Adjusted some log levels and log text to be clearer.
* Added additional logging when the proxy settings are loaded in the event of a failure.
* Added the option to customize the number of parallel threads to use when performing an upload of an intunewin file to Intune.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where whitespace at the beginning or end of the Organization Name for [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) would cause the property to fail to parse correctly.
* Fixed a bug where old setting backups would not rename properly, causing an error during settings backup in some cases.

</details>

## 2.1.6.37 - 2022-09-28

<details>

<summary>Improvements</summary>

* Added a missing tooltip to the ConfigMgr scan wizard button in the ConfigMgr tab.
* Added clarity to the ‘copy’ button tooltips in the Publisher.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where All Devices and All Users assignments created in the Manage Assignments UI could be created with the wrong intent.
  * Note: If you created any new assignments in the Manage Assignment UI while on build 2.1.6.35 please check that they are correctly configured.
  * All Devices assignments default to ‘Uninstall’ intent.
  * All Users assignments default to ‘Required’ intent.

</details>

## 2.1.6.35 - 2022-09-23

<details>

<summary>Features</summary>

* Allow the same Azure group to be assigned multiple times for Intune assignments. This allows a group to be used as both an include, and an exclude.
  * Idea: [PATCHMYPC-I-2322](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2322)
* Pass variables into pre and post-scripts.
  * Note: the %ProductName% and %VendorName% variables are Base64 encoded when they are passed to the pre and post-scripts. It will need to be decoded. Patch My PC will provide a sample PowerShell snippet to decode the resulting parameter.
  * Idea: [PATCHMYPC-I-1348](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1348)
* Extract content from ConfigMgr applications.
* Extract content from WSUS updates.
* Allow any app to have ‘conflicting processes’ configured
  * Idea: [PATCHMYPC-I-1699](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1699)

</details>

<details>

<summary>Improvements</summary>

* Improved child-form handling in some cases, so they now open in the center of the parent form.
* Multi-selection views, such as selecting application scopes or categories, now use a consistent form that allows filtering.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where the wrong URL was used for Microsoft Graph batch requests in some cases.
* Fixed a bug where the buttons in Managed Conflicting Process may not fit the text in some translations.
* Fixed a bug where the ConfigMgr app options window is not resizable.
* Fixed a bug where the Manage Conflicting Process Organization Name would not be set when a ConfigMgr application was revised.
* Fixed a bug where settings could not be saved if the internet was unreachable.
* Fix some typos

</details>

## 2.1.6.2 - 2022-08-26

<details>

<summary>Features</summary>

* Starting with this build, Patch My PC Publisher now requires a minimum of Microsoft .NET Framework 4.6.2.
* Intune package extraction
  * It is now an option to store the encryption keys used to create the Intune package files (.intunewin). This is configurable in the Advanced tab of the Publisher.
  * With the keys stored, you can use the [Intune Application Manager](https://patchmypc.com/intune-application-manager-utility) to download and extract the content of the Patch My PC published Intune applications and updates.
* Webhooks can now be granularly scoped based on several criteria listed below. (Requires Enterprise+)
  * Idea: [PATCHMYPC-I-1871](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1871)
  * Webhook Provider:
    * Slack or Teams is now selectable per webhook allowing the customer to send notifications to both based on their needs.
  * Notification Level:
    * All
    * Error
    * Success
  * Notification type:
    * Update notifications
    * ConfigMgr app notifications
    * Intune app notifications
    * Intune updates notifications
    * Alert notifications
      * Low disk space, certificate expirations, license expirations etc.
  * Specific product
    * Scope a webhook to a specific product, such as notifying the network team of VPN application updates being published.
  * Specific tenants
    * If using multi-tenancy, you can specify the tenant a webhook is scoped to.
* Allow variables to be used to customize the ConfigMgr application name and localized application name. This provides parity with the Intune feature for customized names. Variables available are below.
  * %VendorName%
  * %ProductName%
  * %Version%
  * %OriginalName%
* ConfigMgr application retention now has the option to remove Administrative Categories from retained ConfigMgr applications.
  * Idea: [PATCHMYPC-I-2181](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2181)
* ConfigMgr security scopes now have the option to enforce the selected scopes. The Publisher will remove all non-selected scopes from the application when Publisher.
  * Idea: [PATCHMYPC-I-2328](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2328)
* Allow any product to have Manage Conflicting Processes configured
  * Idea: [PATCHMYPC-I-1699](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1699)

</details>

<details>

<summary>Improvements</summary>

* Intune synchronizations will now happen in parallel for multi-tenancy. Up to 20 tenants synchronize at a time for this build.
* Improve the speed of uploading packages to Intune.
* Refactor email report template.
  * The background is now transparent so that it will match the theme of the email client it is opened in.
  * The code used to generate the template has been refactored to simplify future changes.
* PatchMyPC-Scriptrunner will now factor in the major version filter when available when searching for uninstall strings. This improves the accuracy of uninstalls in some cases.
* Added tooltips to some right-click options that describe why they are disabled in some cases.
* Improved the error handling within the Intune Assignments forms regarding permissions for managing Assignment Filters.
* Format the dates using ISO 8601 formatting when doing the Intune App export for PowerBI reporting. This improves international support.
* Improved the accessibility of the WSUS Options form.
* Improve error messaging and logging for unhandled exceptions.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where the settings backups were stored in a non-sortable format. This bug was introduced in preview 2.1.6.1.
* Fixed a bug where the filters were not applied in the scan wizards when filtering the data. This bug was introduced in preview 2.1.6.1.
* Fixed a bug where the ConfigMgr database scan may throw an exception due to a malformed query. This bug was introduced in preview 2.1.6.1.
* Fixed a bug where the logging option to copy failed logs to a share was not retained. This bug was introduced in preview 2.1.6.1.
* Fixed a bug where failing to copy additional files did not cause an Intune product to fail to publish.
* Fixed a bug where localization files for Manage Conflicting Processes may not be copied correctly in some cases.
* Fixed a bug where the WSUS Options window was not scrollable.
* Fixed several UI navigation bugs on the main form.
* Adjusted encoding of detection and requirement scripts to use UTF8. Some scripts were failing to sign with the previous encoding.
* Fixed a bug where the Manage Conflicting Process Organization Name was not retained when republishing a ConfigMgr application

</details>

## 2.1.6.1 - 2022-07-05

<details>

<summary>Features</summary>

* ConfigMgr and Intune scan wizard allow drill into list of devices where the software was detected
  * Idea: [PATCHMYPC-I-2042](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2042)
* Ability to enforce timestamping, making it a terminating error for the publishing of a product
  * Idea: [PATCHMYPC-I-2112](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2112)

</details>

<details>

<summary>Improvements</summary>

* When exceptions are thrown in the Manage Assignments form they are now handled better by presenting a popup with the exception and a link to related documentation.
* Main form accessibility has been improved.
  * Accessibility names are assigned to many controls to provide context
  * Alt-codes are added to most buttons that did not have them before
  * Right-click options are now accessible via the Apps keyboard button or shift-F10
* When a default Patch My PC provided translation exists for a language selected in [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) it will now automatically populate the text upon adding the language.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug that caused the Paused products section in the email alert to be empty.
* Fixed a bug where we would not put back the version on retained applications if the configuration was set to remove the version from application names and update existing application metadata.
* Fixed a bug in the [Intune application manager](https://patchmypc.com/intune-application-manager-utility#topic3) tool that caused an unhandled exception if you attempt to edit an assignment with a deadline in the past.

</details>

## 2.1.5.1 - 2022-06-09

<details>

<summary>Improvements</summary>

* Setting [Delete Desktop Shortcut…](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#delete-shortcut) or [Disable Self-Updater](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#disable-updates) at the vendor level will now display the list of affected products similar to when these selections are made at the All Products level.
* Updated language in the Update Republish message box to reflect new UI changes for Advanced WSUS options.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where a sync may run multiple times back to back.
* Fixed a bug where Intune authentication did not use the configured proxy.
* Fixed a bug where [republishing](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#republish-updates) an Intune application or update would not update the code signing configuration of the detection script. Republishing an Intune application or update will now update the detection and requirement scripts and code signing configuration as needed.

</details>

## 2.1.4.2 - 2022-05-31

<details>

<summary>Improvements</summary>

* Adding German and Dutch translations to [Manage Conflicting Processes](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#manage-conflicting-processes)
* Intune Filter viewing and configuration is now available in all instances of managing Intune Win32 assignments in the Publisher.
* All setting backups are now in a .CAB format. The import setting option now allows for .XML or .CAB import to ensure we support importing older setting files.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where scriptrunner may fail to find the uninstall string in the registry for some products.
* Fixed a bug where scriptrunner may fail to validate an installation after the installer completes causing a 3-minute delay after the installation completes.
* Fixed a bug where [Pause](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#pause-product-updates) does not account for postponed binaries. If there is an existing postponed binary it will publish even if a pause is set.
* Fixed a bug where some publishing summarization info was miscounted in the PatchMyPC.log file.
* Fixed a bug where the Publisher would leave behind an empty folder when Publishing a ConfigMgr application and the download fails.
* Fixed a bug where a version number would be appended to the current ConfigMgr application instead of the retaining application if the download fails. This bug affected customers who had the ‘Do not include version…’ option configured as well as the ‘Retain…’ option.

</details>

## 2.1.4.1 - 2022-05-19

<details>

<summary>Features</summary>

* Include server name in Publisher upgrade notification email and Teams/Slack notification.
  * Idea: [PATCHMYPC-I-2136](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2136)

</details>

<details>

<summary>Improvements</summary>

* The [Delete desktop shortcut…](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#delete-shortcut) right-click option now removes shortcuts from the user desktop for user-based applications.
* The SMS provider button is now highlighted in the WSUS options if the SMS provider is not configured.

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where an empty Intune tenant is written to settings causing errors when the Publisher attempts to query the invalid tenant.
* Fixed the layout of the [Add MST transformation file](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#mst-transform) form.
* Fixed a bug where we may fail to query for Distribution Point groups if the name or description is DBNull instead of an empty string.
* Fixed a bug where the ConfigMgr SUP sync would not start after a Patch My PC Sync if only updates using local content were published.
* Fixed a bug where the Intune auto-publishing may fail in some cases when right-click options are configured.

</details>

## 2.1.3.5 - 2022-04-27

<details>

<summary>Features</summary>

* Certificate Authentication for Azure App Registration
  * Idea: [PATCHMYPC-I-1540](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1540)
* Option to pause creation of updates or applications for specifics products
  * Idea: [PATCHMYPC-I-1554](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1554)
  * Requires Enterprise Plus
* Allow per-tenant branding for Manage Conflicting Process
  * Applies to Multi-tenant private preview

</details>

<details>

<summary>Improvements</summary>

* Add an operator dropdown in the filter options for Intune and ConfigMgr scan wizards
* Improve Manage Conflicting Process configuration window to better support scaling

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where PatchMyPC-Scriptrunner may throw an exception during log cleanup if the folder does not exist
* Fixed a bug where the publishing summary in the PatchMyPC.log would not include products published from the local content repository
* Fixed a bug where changes to Intune assignments are applied even if the assignment form is cancelled
* Fixed a bug where the Manage Conflicting Process window would not show up when the product install is triggered via Company Portal as a non-admin user
* Fixed a bug where ConfigMgr app retention setting right-click option is not checked when configured
* Fixed a bug where the Updates (WSUS) tab could be used while on an Intune license

</details>

## 2.1.3.4 - 2022-03-28

<details>

<summary>Features</summary>

* Validate the hash of pre/post scripts on sync as well as during a republish.
  * Idea: [PATCHMYPC-I-1946](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1946)
* The Collect Logs button now prepends the file name with the company name from the license.
  * Idea: [PATCHMYPC-I-1904](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1904)
* The email report now converts size to a readable format such as MB or GB instead of bytes.
  * Idea: [PATCHMYPC-I-1331](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1331)
* Support for Intune Filters
  * Idea: [PATCHMYPC-I-1434](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1434)
  * Requires Enterprise Plus

</details>

<details>

<summary>Improvements</summary>

* PatchMyPC.log file now includes the timestamp for the catalog that is processed.
* When a download happens we now write the redirected URL to the PatchMyPC.log as well as in the PatchMyPC-DownloadHistory.csv.
* The Publisher will now retry every 10 seconds up 12 times when saving Package.xml for ConfigMgr applications. This helps account for file locks caused by antivirus.
* Email report has been updated (dark mode)

</details>

<details>

<summary>Fixes</summary>

* Fixed a bug where illegal characters were allowed in file paths, such as a custom log path.
* Fixed a bug where an application may report being automatically enabled during every sync in some scenarios.
* Fixed a bug where the [Manage Conflicting Process](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) UI would not show up for a user-based application.
* Fixed a bug where the [Manage Conflicting Process](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) UI would not show for an Intune application when the user is not an Administrator.
* Fixed the Collect Logs button so it takes into account custom log paths as defined in the Publisher.
* Fixed a bug causing enter to close the group search form for Manage Assignments when in the group input textbox.

</details>

## 2.1.3.3 - 2022-02-23

### Improvements

* CSV files are now saved with UTF-8 formatting.

### Fixes

* Fixed a bug where Intune ADR (private preview) would publish both an Application and an Update.
* Fixed a bug where we might fail to match a running process with Manage Conflicting Processes if the case of the process name did not match.

## 2.1.3.2 - 2022-02-08

### Fixes

* Fixed a bug where a corrupt backup settings file may cause the Publisher update to fail.
  * Patch My PC has determined the scope of impact and will reach out to Preview customers who are impacted.

## 2.1.3.1 - 2022-02-07

### Fixes

* Fixed a bug where the timestamp configuration was reverted to disabled, and the server blank for customers with preview builds enabled. The timestamp configuration will be reverted to the last known good configuration for impacted customers.
  * Note: If updates or applications were published while on preview 2.1.2.1, or if you are a preview customer on 2.1.3.0, then the updates and PowerShell scripts would not be timestamped during this time. This preview restores a valid timestamp

## 2.1.2.1 - 2022-01-28

### Features

* Support for maintaining application dependencies in Intune
  * Checkbox added to Intune Options window: “Update application dependencies from previously created applications when an updated application is created”
  * Idea: [PATCHMYPC-I-1326](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1326)

### Improvements

* When republishing an Intune application or update there is now a prompt asking if assignments should be recreated. The newly recreated assignments would have a deadline and available time relative to the sync when the republish happens.

### Fixes

* Fixed a bug where republishing a ConfigMgr application would remove existing application dependencies, supersedence, and requirements the customer may have added.
* Fixed a bug where the Manage Conflicting Process option to use the ConfigMgr application max run time for the notification timeout would not work for a republished ConfigMgr application.
* Fixed a bug where republishing an Intune application or update might remove existing assignments.
* Fixed a bug where we may fail to put back the version on the name of retained ConfigMgr applications in some scenarios.
* Fixed a bug where the Manage Conflicting Process UI may fail to identify conflicting processes causing it not to show.
* Fixed a bug where the Manage Conflicting Process UI may default to a 5-hour timeout for ConfigMgr applications in some scenarios.
* Fixed a bug where delayed ConfigMgr applications may publish one day early.
* Fixed a bug where the IsFeatured flag would not be set for a republished Intune application.
* Fixed a bug where the Publisher would fail to validate a ConfigMgr source path if there were Deployment Packages with an empty source path.
* Fixed a bug where the Publisher may delete a content folder during republishing if the binary was missing from the local content repository.
* Fixed a bug where the Manage Conflicting Process UI notification would fail to display if the user DateTime format and the system DateTime format were conflicting, causing DateTime parsing failures.
* Fixed a bug where the Manage Conflicting Process notification timeout setting may not be read correctly from settings.xml.

## 2.1.1.2 - 2021-12-06

### Improvements

* Updated to the latest Patch My PC logo.

### Fixes

* Fixed a bug where the Republish feature may cause multiple republish actions to occur if the customer performs the operation on multiple tabs.
* Fixed a bug where ‘disabling’ a tab with the checkbox at the top would cause the settings to be lost if the Publisher was closed.
* Fixed a bug where the alert webhooks may be duplicated during a setting import.
* Fixed a bug where some unsupported right-click options might be enabled by the auto-enable product’s rules.
* Fixed a bug where conflicting process notification timeout setting was not being read properly from settings.xml causing the setting to not apply.

## 2.1.1.1 - 2021-11-18

### Features

* Collect Logs button added to the Publisher. Will create a .zip file of files useful for troubleshooting.
  * Idea: [PATCHMYPC-I-1750](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1750)

### Improvements

* If the ConfigMgr applications are configured to remove the version from the name, and there is application retention configured we will now append the version to OLD versions of the app. This is to ensure that there is only one application with the same name.
* Improved the initial configuration process for adding Patch My PC Software Updates to an environment. This involves attempting to restart the WCM component after an initial Patch My PC update is published. This expedites getting the Patch My PC category into ConfigMgr so it can be selected.
* The Publisher will send an alert if the catalog failed to download.
* The Publisher can now process FTP links for downloads.

### Fixes

* Fixed a bug where the /SyncNow switch for the Publisher would not work if an instance of the Publisher was already running.
* Fixed a bug where multiple assignments for the same group may attempt to be created in Intune.
* Fixed a bug where the Organization Name specified for the Manage Conflicting Process window would not be populated for ConfigMgr applications.
* Fixed a bug where the icon would not be set for a republished Intune application.
* Fixed a bug where the republish ConfigMgr application feature would not validate the hash of existing additional files which caused edited files to not be copied during a republish.
* Fixed a bug where republish ConfigMgr application would not set the expected OS requirements.
* Fixed a bug where ‘Override manual assignment changes’ is checked for an Intune product, and there is an ‘exclude’ assignment which would cause the Publisher to fail to process all assignments.

## 2.1.0.2 - 2021-10-22

### Features

* Allow customized [Managed Conflicting Process](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) popup notifications, including support for localization.
  * Idea: [PATCHMYPC-I-1296](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1296)

### Improvements

* It is now possible to ‘Manage ESP assignments’ from within the [Intune Application Manager](https://patchmypc.com/intune-application-manager-utility).

### Fixes

* Fixed a bug where the Publisher would fail to parse a command line that had a parameter that occurred more than once. This would cause a content update every sync.

##

## 2.1.0.1 - 2021-10-13

### Features

* Clicking a ‘localhost’ download URL in [show package info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo) will validate the local content.
  * Idea: [PATCHMYPC-I-1363](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1363)
* Option to “Republish” ConfigMgr and Intune Applications
  * Idea: [PATCHMYPC-I-1353](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1353)

### Improvements

* ConfigMgr database scan button is now available on the ConfigMgr apps tab as well as the Updates tab.
* ScriptRunner will always use Intune-based folders when executing from an Intune app installation.
* ScriptRunner will now monitor for child processes during the uninstall of software. This ensures that uninstalls which spawn child processes do not exit immediately and cause a detection error.
* Prevent using a ConfigMgr source path that could cause paths to exceed the 256 Windows path limit.
* Fixed a bug where publishing would proceed even if a custom script failed to be processed.

### Fixes

* Fixed a bug where Recreate Detection Script option for ConfigMgr would cause the wrong ‘Installation Behavior’ to be set for user-based apps.
* Fixed a bug where the Publisher and ScriptRunner would fail to parse a parameter with nested quotes and spaces.
* Fixed a bug where PreventStart UI would fail to be bypassed when a SYSTEM launched a conflicting process potentially leaving behind Image File Execution Option registry keys.
* Fixed a bug where retained applications may be updated unexpectedly when both postpone app and retain app are configured.
* Fixed a bug where the Publisher would run a sync every time ‘Apply Changes’ is clicked and the schedule is set to hourly.

## 2.0.9.2 - 2021-09-09

### Improvements

* Text boxes within the UI now implement an autocomplete for file paths and URLs.
* The [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) notification will now display ‘update’ based language for an Intune Update. For example, the button will say ‘Close and Update’ instead of ‘Close and Install.’

### Fixes

* Fixed a bug where the ConfigMgr [source folder validation](https://patchmypc.com/smsprovider-connection-and-source-folder-options#Source-Folder-Validation) would perform a partial match, such as \\\server\source\_apps being considered a conflict for \\\server\source. We now append a trailing slash to the comparison.
* Fixed a bug where the ‘Prevent Start…’ option for [Manage Conflicting Process](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) would throw an access denied error instead of the desired message box.
* Fixed a bug where assignments would be copied from Intune app to Intune updates when the copy between tabs is used.
* Fixed a bug where custom return codes set in the catalog were not processed for updates by the Publisher.
* Fixed a bug where ConfigMgr applications would be revised every sync when the Manage Conflicting Process option is set to an option other than ‘Notify’

## 2.0.9.1 - 2021-08-27

### Features

* Improve conflicting process timeout options
  * ConfigMgr and Intune timeout increased to their respective maximums, minus a 15-minute buffer.
    * ConfigMgr App Max: 705 minutes
    * Intune Max: 45 minutes
  * New option to use ‘maximum run time’ from the respective update or app.
    * ConfigMgr Update Max: Will use configured update ‘max run time’ as configured in ConfigMgr for the update.
      * Note: Update max run time must be edited **before** the update is deployed for a client to recognize the change.
    * ConfigMgr App Max: Will use the configured deployment time ‘max run time.’
    * Intune App/Update Max: Will use the maximum run time of an Intune Win32 app (60 minutes minus the 15-minute buffer).
  * Idea: [PATCHMYPC-I-1516](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1516)
* Send an alert if the Publisher failed to auto-update.
  * Idea: [PATCHMYPC-I-1254](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1254)
* Send an alert when the Publisher is updated
  * Idea: [PATCHMYPC-I-791](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-791)
* Add time zone to Teams/Slack Webhook notification
  * Idea: [PATCHMYPC-I-856](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-856)
* Split out notification settings to allow Error notifications and Information notifications to go to different webhooks
  * Idea: [PATCHMYPC-I-1536](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1536)

### Fixes

* Fixed a bug where the Publisher would throw an exception if a ConfigMgr scope is deleted, but still associated with a product in the Publisher.
* Fixed a bug where Intune email reports would not include the warning regarding missing local content for applications

## 2.0.8.2 - 2021-08-05

### Improvements

* The Publisher will not delete the local content for a product if the publishing of the product failed.
* The Publisher will automatically revise an update if the applicability rules or description is updated in the catalog.

### Fixes

* Fixed a bug where the Manage Conflicting Process window may not show the proper process name in the list of conflicting applications.
* Fixed a bug where the Publisher did not respect the ConfigMgr app retention settings when the delay in-place upgrade feature was also in use.
* Fixed a bug where Intune apps and updates would not use the temp content download directory specified in the advanced tab.
* Fixed a bug where the Publisher would revise ConfigMgr apps every sync in certain cultures (The known issue was with Russian, but could impact others).
* Fixed a bug where the alert webhook configured for Slack may revert to a Teams webhook causing malformed messages.

## 2.0.8.1 - 2021-07-30

### Features

* Double-clicking a product in the Publisher will now bring up the ‘[Show Package Info…](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo)‘ tool.
  * Idea: [PATCHMYPC-I-1521](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1521)
* The Publisher will now check the permissions associated with the token for the Azure App Registration and provide more specific errors and logging. Additionally, the ‘Test’ button now presents a more information UI for permission validation.
  * Idea: [PATCHMYPC-I-1509](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1509)
* Log current working directory in PatchMyPC-ScriptRunner.log
  * Idea: [PATCHMYPC-I-1504](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1504)
* Export the list of enabled products and their right-click configurations to a CSV. This option is available in the Advanced tab of the Publisher. Only enabled products are exportable.
  * [PATCHMYPC-I-1064](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1064)
* Publisher will validate the ConfigMgr application source path. A path is considered invalid if it is not a UNC path, or if the path is in use by a Software Update Deployment Package. Existing invalid configurations will not be impacted, but there will be an alert via email or Teams if alerts are enabled.
  * Idea: [PATCHMYPC-I-1299](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1299)

### Improvements

* Added tooltips to fields in the scan wizards to improve accessibility.

### Fixes

* Fixed a bug where the Manage Conflicting Process UI may continue to append text instead of having a countdown when it is set to ‘Do not allow user deferral…’
* Fixed a bug where pre/post uninstall scripts would only copy into the ConfigMgr source during a new application publisher. Scripts will now be copied into the source during the sync after the configuration change.
* Fixed a bug where the Intune Assignment UI would allow an invalid grace period/restart/snooze configuration.
* Fixed a bug where PatchMyPC-ScriptRunner would create an invalid command line for an MSI uninstall in some cases.

## 2.0.7.2 - 2021-07-09

### Fixes

* Fixed a bug where user-based ConfigMgr applications may not have the Application Experience configuration properly configured.

## 2.0.7.1 - 2021-07-07

### Features

* Manage Conflicting Process ‘Close and Update’ button will now call the CloseMainWindow first. If the conflicting application is still running after 20 seconds we fall back to the Kill method.
  * This gives the user 20 seconds to respond to any ‘save’ prompts or other app-closing windows.
  * Idea: [PATCHMYPC-I-1277](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1277)
* Pre/Post scripts for uninstall
  * Idea: [PATCHMYPC-I-550](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-550)
* Manage Conflicting Process settings also apply to uninstall. This ensures that a user will be prompted to close software for the uninstall as well.
  * Idea: [PATCHMYPC-I-1430](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1430)
* Allow multiple webhooks so alerts are posted to multiple endpoints.
  * Idea: [PATCHMYPC-I-1301](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1301)
* MSI uninstall performed by Scriptrunner will append REBOOT=ReallySuppress to the uninstall command.
  * [PATCHMYPC-I-1332](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1332)
* MSI uninstall performed by Scriptrunner will generate an MSI log file if logging is configured for the application in the Publisher.
  * Idea: [PATCHMYPC-I-1492](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1492)
* The [Show Package Info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo) wizard will now show the file size from the catalog.
  * Idea: [PATCHMYPC-I-1461](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1461)

### Improvements

* If publishing an update fails with timestamping then we will attempt to publish again without timestamping.
* Improved connection testing to patchmypc.com:443 during publisher sync.
* During Publisher sync the WSUS cleanup for ‘Unneeded update files’ will now run.

### Fixes

* Fix user validation of the input fields for pre/post script when the file does not exist.
* Fixed Intune detection script which was looking for a non-existent ‘dn’ property.
* Fixed Intune detection script so that it will parse invalid version parts that exceed a 32-bit signed integer.
* Fixed ConfigMgr detection script so that the RegKeyDetection work as expected for enhanced detection based on additional registry key values.
  * Script Version: 3.1
* Fixed a bug where double-clicking an item in the Intune App Manager would cause an ‘Index out of Range’ unhandled exception. This now opens the Manage Assignment wizard as expected.
* Fixed a bug where ConfigMgr applications with only user-based deployment types would have the checkbox set to allow installation during a task sequence, which is not allowed.
* Fixed a bug where the UI notification log file may not be created if the folder does not exist.

## 2.0.6.1 - 2021-06-24

### Features

* Allow the scheduling of the Modify Updates Wizard for Update Cleanup (unreferencedpackagefolders)
  * Idea: [PATCHMYPC-I-797](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-797)
* Fill out ‘Disk Space Required’ for Intune apps.
  * Idea: [PATCHMYPC-I-1466](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1466)
* Intune app manager will filter by PMPC published apps by default, providing a drop-down to select non-PMPC or all apps.

### Fixes

* Further improvements to CM log format for culture compatibility.

## 2.0.5.1 - 2021-06-15

### Features

* Add support to re-sign updates.
  * Idea: [PATCHMYPC-I-1271](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1271)
  * Doc: [Re-sign updates](https://patchmypc.com/modify-published-third-party-updates-wizard#resign)
* Use windows native methods for signing PowerShell scripts.
  * Can be disabled with a registry key as noted [here](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#LegacySign).

### Improvements

* PowerShell detection scripts will use regex to extract the version from the displayVersion field to account for vendors that put more than the version in the field.
* Set ErrorAction to SilentlyContinue for extra regkey validation checks to suppress errors in the event the key does not exist.
* Add a delay in Scriptrunner if the main installer exits in less than 2 seconds. This is to account for installers that spawn child processes.

## 2.0.4.3 - 2021-06-02

### Features

* Add option to update Intune assignments on sync.
  * New checkbox at the bottom of the Manage Assignments wizard to ‘Override manual assignment changes…’
  * Idea: [PATCHMYPC-I-1297](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1297)
* Add title of application or update to the Manage Assignments wizard.
  * Idea: [PATCHMYPC-I-1420](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1420)
* Notifications are presentation mode aware
  * Idea: [PATCHMYPC-I-1248](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1248)

### Improvements

* When a product is double-clicked in the [show package info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo) tool the applicability rule will be shown.
* Improve the message which displays when an incorrect configuration is saved.
* Code changes in preparation for user-based applications.

### Fixes

* Fixed a bug where the Manage Conflicting Process window would not appear when a ConfigMgr application was deployed as required and the checkbox for ‘Allow user interaction…’ was not checked.
* Fixed a bug where Intune role scope tags would not be updated on sync for Intune Updates.
* Fixed a bug where the configured proxy may not be used for the Intune connection during publisher sync.

## 2.0.4.2 - 2021-05-19

### Features

* View and customize Conflicting Processes list
  * Idea: [PATCHMYPC-I-1382](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1382)
* The UI notification for Conflict Processes now lists all processes which are conflicting in a dropdown. This is to make it more clear what software will be closed.

### Improvements

* Publisher SMTP alerts for the creation of ConfigMgr apps, Intune apps, and Intune updates will all now show the CVE information. Previously only the WSUS updates would show this information.
* Added notes to the pre/post script window to help clarify the feature functionality.

### Fixes

* Fixed a bug where software may be marked for revision during every sync of the Publisher. This would occur when PreventConflictingProcessRestart was in use and the KillProcess was set instead of Notify.
* Fixed a bug where the 'Exclude from Auto-Publishing' option for Intune apps and Intune updates may not work as expected causing excluding software to still be published if found.

## 2.0.4.1 - 2021-05-05

### Features

* Send alerts to Slack
  * Idea: [PATCHMYPC-I-684](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-684)
  * Note: Slack notifications are a work in progress.
* Reverted a Scriptrunner change which flagged the exe to always run as Administrator. This is in preparation for supporting user-based applications in Intune and ConfigMgr.

### Fixes

* When a user or admin category was selected on a ConfigMgr application the Publisher would create a revision of the application every synchronization. Now a revision will only be created if a user or admin category needs to be added.
* Improved logging when checking access to timestamp.digicert.com if a proxy is defined

## 2.0.3.1 - 2021-04-22

### Features

* Added support to add a future Home Lab subscription
  * Idea: [PATCHMYPC-I-1213](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1213)
* Added a new context menu in the Intune Application Manager
  * ![](../../.gitbook/assets/image-\(1907\).png)

### Improvements

* Improved logging

## 2.0.3.1 - 2021-04-22

### Features

* Added support to add a future Home Lab subscription
  * Idea: [PATCHMYPC-I-1213](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1213)
* Added a new context menu in the Intune Application Manager
  * ![](../../.gitbook/assets/image-\(1907\).png)

### Improvements

* Improved logging

## 2.0.3.1 - 2021-04-22

### Features

* Added support to add a future Home Lab subscription
  * Idea: [PATCHMYPC-I-1213](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1213)
* Added a new context menu in the Intune Application Manager
  * ![](../../.gitbook/assets/image-\(1907\).png)

### Improvements

* Improved logging

## 2.0.2.2 - 2021-04-19

### Features

* Define ConfigMgr scopes inside the Publisher service
  * Idea: [PATCHMYPC-I-962](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-962)
  * Note: This requires updated permissions. The ‘Import Role’ option in the Publisher will import the role with proper permissions or you can refer to this [article](https://patchmypc.com/permissions-required-in-sccm-for-base-installation-packages-from-patch-my-pc).

### Improvements

* The Intune and ConfigMgr scan wizard ‘Export’ buttons now prompt for whether the filter should be applied to the export.
* Improve how Timestamping is handled in some scenarios.

### Fixes

* Connections to Intune may not respect the proxy configuration set in the Publisher.
* ‘Show Package Details…’ right-click option would not load as expected.
* CVE Wizard would not load as expected.
* SSRS dashboards would report a negative % for compliance in some scenarios. The reports can be reinstalled if you are affected by following the same process as the initial install which will overwrite the reports.

## 2.0.2.1 - 2021-04-14

### Features

* Added the Usage Statistics group in the General tab that will show usage statitics
  * Idea: [PATCHMYPC-I-1343](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1343)
* Changed the license input to display only the 20 character license id and not the full license URL

### Improvements

* Improved the speed of Intune application deletion by using batch calls to Microsoft Graph
* Options related to WSUS have been moved from the Advanced tab to the Options button in the Updates tab

### Fixes

* The classification field in the Intune Apps Manager is not populated for Updates
* Update revision doesn’t take account of republished updates

## 2.0.1.4 - 2021-03-30

### Features

* Change description text and icon for Intune Win32 applications
  * Idea: [PATCHMYPC-I-1158](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1158)
* Retain N-X apps in ConfigMgr when set to ‘Create a new application…’ is enabled.
  * Idea: [PATCHMYPC-I-1266](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1266)
* Retain N-X apps in ConfigMgr when set to ‘Update existing application…’ is enabled.
  * Idea: [PATCHMYPC-I-1265](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1265)

### Improvements

* The scan wizard found application count is now updated to reflect applications found with the specified filter.
* Scriptrunner will now clean up leftover ‘Image File Execution Options’ registry keys. This helps prevent unexpected blocking of application launch in the event scriptrunner crashes and leaves behind some of these keys. We have also update the [Manage Conflicting Processes docs](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications#UpdateInProgress) to provide additional information for this scenario.

### Fixes

* Fixed a bug where assignments may not be added to an existing Intune Win32 application during Publisher sync.
* Fixed a bug where the Publisher UI would crash if the ‘Modify Updates Wizard’ was launched on a computer which does not have the WSUS role.
* Fixed a bug where only the first 1000 Intune applications are returned which can cause Application lookup failures via Microsoft Graph.

## 2.0.1.3 - 2021-03-18

### Features

* Intune Scoping Support
  * There is a [new right-click option](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#Manage-RoleScopeTags) for Intune applications and updates which lets you ‘Manage scope tags.’
  * Scope tags will be copied from the previous PMPC application or update to the new version during a Publisher sync.
  * Requires new permission to be added to the Azure App Registration
    * DeviceManagementRBAC.Read.All
  * Idea: [PATCHMYPC-I-1029](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1029)

### Improvements

* Wait to delete local content repository files until the end of the Publisher sync if the option to ‘Delete the update file in the local repository after publishing’ is selected.
  * In some cases, customers had the same binary needed for two different publish actions, and the second publish would fail because the binary had been deleted.
* In the DownloadHistory.csv file, we now include the purpose of the download and the port.

## 2.0.1.2 - 2021-03-11

### Features

* ConfigMgr right click option to set OS type requirement – client vs. server
  * Idea: [PATCHMYPC-I-1255](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1255)

### Improvements

* Scriptrunner will now automatically prompt for elevation when executed.
* Improve how settings are saved to prevent losing your Publisher configuration in some scenarios such as no disk space.
* The UI Notification feature for conflicting processes will now exit with an exit code 1602 if the installation is snoozed or a timeout occurs. Previously it was 1618 which could cause very frequent reevaluation.

### Fixes

* Fixed a bug where we may fail to parse a package.xml file that contains special characters such as an ampersand.
* Fixed a bug where the DownloadUrl and MoreInfoUrl columns were not sortable in the ‘Show Package Info’ UI.
* Fixed a bug where the UI may crash if there is a large number of Azure AD Groups being retrieved and the UI is closed before the query completes.
* Fixed a bug where some right-click options such as Manage Categories, Manage ESP profiles and Manage Naming Convention may not propagate from the root, or vendor level to a newly enabled product.

## 2.0.0.5 - 2021-03-01

### Fixes

* Fixed a bug where some Intune App and Intune Update scripts were missing a parenthesis causing an error during execution.

## 2.0.0.4 - 2021-02-26

### Fixes

* Fixed a bug introduced in version 2.0.0.1 preview where the ‘Disable Self-Updater’ option would be enabled during a synchronization even if the user has not selected this option.
  * If you are on a 2.\* preview build you will want to review your right-click selections for ‘Disable Self-Updater’.
  * The backup settings.xml can be used to determine which products had this erroneously enabled. Please contact support if you need assistance in determining what products had this enabled where it previously was not.

## 2.0.0.3 - 2021-02-26

### Improvements

* Global options for the User Notification now moved into right-click option for Conflicting Processes
  * Logo
  * Company Name
* WSUS Certificate status now updated when the Show Certificate button is pressed.

### Fixes

* Fixed a bug in the ConfigMgr detection script where software may be incorrectly detected in some scenarios.
  * Only impacted version v2.7 of the script which was available briefly.
  * Script Version: 2.8

## 2.0.0.2 - 2021-02-24

### Features

* Use Scriptrunner to uninstall MSIs
  * Idea: [PATCHMYPC-I-1083](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1083)

### Improvements

* Increase the max delay for the ConfigMgr Apps feature to 32 days.
* Intune Application Manager button is now available in the Intune Apps and Intune Updates tab directly, as well as in the Intune Options.
* ConfigMgr detection scripts now validate architecture and installation type of of the software being detected.
  * This feature was in place for Intune scripts and has been integrated into the ConfigMgr scripts.
  * Script Version: 2.7

### Fixes

* Fixed a bug where the new Conflicting Process settings may not be saved for ConfigMgr applications.
* Fixed a bug where the company logo may not show in the Conflicting Process UI for Intune clients.
* Fixed a bug where the Conflicting Processes deferral count would allow more than the configured number of deferrals.

## 2.0.0.1 - 2021-02-22

### Features

* Interactive user notifications that allow the user to be prompted to close conflicting software
  *   Has a range of options for customizing the deferral options.

      (Documentation will be released when this feature is in production)
  * Idea: [PATCHMYPC-I-438](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-438)
* Delete N-# applications / updates in Intune
  * There are new settings available in the ‘Intune Options’ which allows you to specify retention for Intune Applications and Intune Updates. The valid values are between 0 and 10.
  * Idea: [PATCHMYPC-I-967](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-967)
* InstallPackage as the default behavior for ScriptRunner
  * When the PatchMyPc-ScriptRunner.exe is double-clicked it will default to searching for package.xml in the same directory and performing /InstallPackage which allows PMPC application install to be launched without running them from the command line.
  * Idea: [PATCHMYPC-I-1170](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1170)
* Apply Intune naming convention to existing applications and updates during a Publisher sync
  * Idea: [PATCHMYPC-I-1175](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1175)
* Set ‘Featured App’ flag on Intune apps via right-click options
  * Idea: [PATCHMYPC-I-1188](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1188)

### Improvements

* Only one instance of the Publisher is allowed to run at a time. If a second user runs the Publisher they will receive an error message and the Publisher will close.

### Fixes

* Fixed a bug where adding file based right click option to a ConfigMgr application would not trigger a revision in some cases.
  * Examples: MST, Pre/Post Script, Additional files
* Fixed a bug where the Intune detection and requirement script might fail to work as expected if there are invalid registry properties on an object in the registry.

## 1.9.9.5 - 2021-01-27

### Improvements

* Update right-click option text to accurately reflect functionality.
  * Exclude from being enabled during automated SCCM/Intune inventory scans
    * Renamed to: Exclude from auto-publishing rules
  * Add/Manage pre/post update installation scripts
    * Renamed to: Add/Manage pre/post scripts
  * Patch My PC defined pre/post update installation scripts
    * Renamed to: Patch My PC defined pre/post scripts

### Fixes

* Fixed a bug with the new Log Retention feature of Script Runner where it may unnecessarily trigger an ‘Update Content’ on ConfigMgr applications. (actually fixed this time)

## 1.9.9.4 - 2021-01-26

### Improvements

* The warning message box that pops up if the Enrollment Status Page right-click option is invoked without proper Azure App Registration Permission now has a ‘Help’ button which links to the permission KB article.
* The pre and post script ‘browse’ buttons now will open to the location of the currently selected script if found.

### Fixes

* Fixed a bug where the Intune Scan or ConfigMgr Scan would happen if the respective ‘Auto-Enable’ option was enabled, but the feature itself, such as Intune Updates, was disabled.
* Fixed a bug where the Teams notifications for auto-enable would not contain details regarding the software.
* Fixed a bug where the auto-enable feature of Intune Scanning may cause duplicate Win32 apps to be published within Intune.
* Fixed a bug where conflicting right-click options could be selected in the scan wizards.
* Fixed a bug with the new Log Retention feature of Script Runner where it may unnecessarily trigger an ‘Update Content’ on ConfigMgr applications.

## 1.9.9.3 - 2021-01-19

### Features

* Sign PMPC provided pre/post scripts with local WSUS Code Signing certificate
  * Idea: [PATCHMYPC-I-959](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-959)
* ScriptRunner now deletes log files older than X days according to the setting in Advanced Tab.
  * Idea: [PATCHMYPC-I-1105](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1105)

## 1.9.9.2 - 2021-01-13

### Features

* Add an additional Right-Click option for x86 OS requirement for x86 application installers
  * Idea:[ PATCHMYPC-I-779](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-779)

### Improvements

* Improved vertical scrollbar behavior for Scan Wizards

### Fixes

* Fixed a bug where an Enrollment Status Page may have a mobileAppId listed twice when making the Graph PATCH API call. This would cause a 400 status code, and cause the API call to fail.

## 1.9.9.1 - 2021-01-12

### Features

* Modify Autopilot Enrollment Status Page profiles.
  * Update ESP profiles when an application is updated. This will ensure the latest application version is associated with your ESP.
    * New [Checkbox in Intune Options](https://patchmypc.com/intune-application-creation-options#Update-ESP) to enable.
  * Select profiles an application should be assigned to with a new [right-click option](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#Manage-ESP).
  * Requires updated [App Registration Permissions](https://patchmypc.com/intune-authentication-using-azure-app-registration).
    * DeviceManagementServiceConfig.ReadWrite.All
  * Idea: [PATCHMYPC-I-673](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-673)
* Support for MSP Patching via Intune.
  * Idea: [PATCHMYPC-I-1147](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1147)
* ScriptRunner will use QuietUninstallString when found for application uninstallation.
  * Idea: [PATCHMYPC-I-930](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-930)

### Improvements

* PatchMyPC-ScriptRunner has improved logic for UninstallPackage.
  * Now factors in SystemComponent and QuietUninstallString when searching the registry.
* Intune Scan Wizard updated to match the ConfigMgr scan wizard.
  * Can include zero-count applications in results and export.
  * Filtering options updated.
* The ‘Exclude from auto-enroll…’ option now exists for Intune Apps and Intune Updates.
* Scan Wizards will now automatically allow vertical scrolling if needed.
* Implement a retry when performing some ‘POST’ operations to Microsoft Graph to improve Intune Win32 app creation reliability.

### Fixes

*   Fixed a bug where the certificate option would be enabled while in

    ‘Intune Only’ mode.
* Fixed a bug where the Intune Graph token used by features such as Intune App Category selection would expire if the Publisher UI was open for a long time.
* Fixed a bug where unnecessary calls were made to renew the Graph API token when performing Graph Batch queries.
* Fixed a bug where the ConfigMgr ‘Recreate Detection’ option would not set the MSI product code for the newly generated script.
* Fixed a bug where the ConfigMgr ‘Recreate Detection’ option would not set the VersionInclude for the newly generated script.

## 1.9.8.1 - 2020-12-17

### Features

* [Customizable Naming Convention](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#IntuneNamingConvention) for Intune Applications
  * Idea: [PATCHMYPC-I-961](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-961)

### Fixes

* Adjust certificate signing validation for Patch My PC signed files.

## 1.9.7.3 - 2020-12-11

### Features

* Manage categories for Configuration Manager applications
  * User Categories: Viewable to users in Software Center
  * Admin Categories: Viewable to administrators in the Configuration Manager Console
  * Idea: [PATCHMYPC-I-780](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-780)

### Improvements

* During a Publisher sync, the Settings.xml will be automatically updated according to SupportProducts. This improves the experiences when Patch My PC makes metadata changes that impact some of the application configurations such as detection.

## 1.9.7.2 - 2020-12-07

### Features

* ScriptRunner now has a new custom variable, %CurrentDir%
  * This variable may need to be put in double-quotes or the entire parameter may need to be in double quotes depending on the application. Examples of this are below.
    * Config=”%CurrentDir%\Config.ini”
    * “Config=%CurrentDir%\Config.ini”
  * Idea: [PATCHMYPC-I-985](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-985)

### Improvements

* The Intune Application Manager now has a button for ‘Manage Assignments’
* Improve how ScriptRunner handles version parts that exceed the 32 bit signed integer max.
* Improve [CVE Import Wizard](https://patchmypc.com/how-the-cve-import-wizard-works-for-matching-cve-ids) CVE-ID matching
* Improve logging associated with delayed application publishing
* The[SSRS report dashboards](https://patchmypc.com/free-software-update-compliance-dashboard-reports-for-microsoft-sccm) now include a parameter for Deployed.

## 1.9.6.2 - 2020-11-20

### Features

* Manage Intune categories for created and updated Intune applications and updates.
  * Note: Currently, existing applications/updates in Intune will not have their categories modified. The categories will only be modified when a new Win32 application is published such as when new software is selected, or a new version is released.
  * Idea: [PATCHMYPC-I965](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-965)
* Clicking a ‘digest’ in the Modify Published Updates Wizard, or the Package Details wizard will now open the respective VirusTotal page.

### Improvements

* Sorting by ‘Selected’ in Modify Published Updates Wizard now sorts by the checked state.
* The Configuration Manager detection script now handles invalid version parts better. Some vendors use DateTime stamps in their version. This can end up being a value larger than a 32 bit integer causing the version cast to fail.

### Fixes

* Fixed a bug where the console version check for UninstallContent setting was incorrect.

## 1.9.6.1 - 2020-11-16

### Fixes

* Fixed an issue where copied Intune Assignments for newly published Intune software would not have their custom available time, and deadline time adjusted relative to the new publish date.
* Fixed an issue where Intune Assignments would be created without a deadline or available time if the ‘copy assignment’ option was not configured.
* Fixed an issue where the maximum value for restart notification would not allow a value greater than 201.

## 1.9.5.2 - 2020-11-10

### Changes

* Win32 Intune applications will no longer be created as featured

### Improvements

* Improved the speed at which the catalog is extracted for the CVE Import Wizard

## 1.9.5.1 - 2020-11-09

### Features

* New feature that allows [viewing, and exporting package details](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo).
  * Idea: [PATCHMYPC-I-1037](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1037)
  * The below information can be viewed for the currently synchronized catalog.
    * Title (Including version)
    * File Name
    * Command-line
    * Download URL
    * Digest

### Improvements

* Improved the speed at which the catalog is processed. This will improve the loading speed of the CVE Import Wizard, the new Package Details Feature, and the Modify Updates Wizard.

## 1.9.3.3 - 2020-11-03

### Features

* Updates published via the CVE Import Wizard will now have a Teams and Email alert if enabled.
* Scan Configuration Manager Database wizard updated.
  * Supports Filtering
  * Can optionally show, and export, applications whose count is zero.
    * Idea: [PATCHMYPC-I-828](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-828)
  * General UI improvements such as tooltips, alt-shortcuts, empty field validation.

### Improvements

* Certificate selection for Intune code signing will now additionally search the WSUS store if it is found.
* The Product Name has been added to the PatchMyPC-DownloadHistory.csv generated in the installation directory of the publisher.
* Improved the method used to gather PackageID from newly published Applications.

### Fixes

* Fixed a bug where an application may fail to publish on versions of Configuration Manager older than 1706.
* Fixed a bug where the publisher would fail to find applications published to a folder containing square brackets
  * For Example: \\\server\sources\\\[PMPC]Applications
* Fixed a bug where the TLS port for SMTP alerts may show as 587 in the UI, even when a custom port is set. The port in the UI will now accurately reflect the saved settings.

## 1.9.3.1 - 2020-10-26

### Features

* The first preview release of our CVE import/matching features based on UserVoice [**Feature Request for CVE Import automation**](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-916)
  * You can launch the CVE import feature in the Updates tab by clicking the new document lock icon
  * If you have any feedback on the first preview release, leave a comment at [https://ideas.patchmypc.com/ideas/PATCHMYPC-I-916](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-916)

### Fixes

* Fixed an issue where Intune assignments may not set the correct delayed deadline
* Fixed an issue where older versions of the ConfigMgr console may receive error: Method not found: 'Void Microsoft.ConfigurationManagement.ApplicationManagement.MsiInstaller.set\_UninstallSetting(Microsoft.ConfigurationManagement.ApplicationManagement.UninstallContentSetting)'.

## 1.9.2.3 - 2020-10-13

### Improvements

* The PatchMyPC-ScriptRunner.exe will retry MSI based operations if a 1618 exit code is returned by the installer. The result is a reduction in failed installs due to Windows Installer being unavailable.
  * Maximum three retries, with 1 minute in between.

## 1.9.2.2 - 2020-10-08

### Features

* Update the PatchMyPC-ScriptRunner.exe to use the CCM client log directory defined in the registry by default
  *   Check

      “HKEY\_LOCAL\_MACHINE\\\SOFTWARE\\\Microsoft\\\CCM\\\Logging\\\\@Global”

      \> LogDirectory, and fallback to ‘%windir%\\\ccm\\\logs’
  * Idea: [PATCHMYPC-I-911](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-911)

### Improvements

* Log out the in-progress count of updates and applications as they are processed.
  * Previously the in-progress count was only logged if the log level was set to debug. It is now logged with informational level logging.
* Improve the PatchMyPC-ScriptRunner.exe to have better logic when searching the registry for uninstall strings

### Fixes

* Configuration Manager application detection script fixed to supported PowerShell 2.0.
* Fixed an issue where republishing a WSUS update would also cause the equivalent Intune Update to republish as well.

## 1.9.2.1 - 2020-10-07

### Features

* Application update in-place vs. create new application configurable at the individual product level.
  *   Idea:

      [PATCHMYPC-I-209](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-209)
* Support for user-based installations for Configuration Manager applications, as well as Intune Applications and Intune Updates.
  *   Idea:

      [PATCHMYPC-I-801](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-801)
  * Note: We still need to add user-based software to the catalog, but the publisher now has support for this so that we can begin adding some user-based software.
* Option to not append the republished date tag to republished updates.
  *   Idea:

      [PATCHMYPC-I-876](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-876)
  * This is now a configurable checkbox in the advanced tab.
* Intune Scan Wizard now has the option to[automatically enable Intune Updates based on scan data](https://patchmypc.com/scan-intune-for-supported-products#CurrentFeatures).

### Improvements

* Updated the PowerShell script for Intune applications and updates to improve compatibility with constrained language mode.

## 1.9.1.1 - 2020-09-24

### Improvements

* Publisher code changes to better support our [Proactive Customer Care](https://patchmypc.com/proactive-customer-care) program

### Fixes

* Fixed an issue where the [Intune Application Manager Utility](https://patchmypc.com/intune-application-creation-options#topic5) would throw a terminating error if Intune applications were found with an empty ‘Notes’ field.

## 1.9.0.1 - 2020-09-18

### Features

* Added an option to disable WSUS publishing using a checkbox at the top of the ‘Updates’ tab. This allows the Update publishing feature to be disabled while still retaining all products and settings. This can be helpful if you need to sync only Applications, Intune Applications, or Intune Updates, but don’t want to lose your selected Updates and configurations.
* Added a right-click option to open the help page that details the right-click options.
* During synchronization, the Publisher will check if the WSUS code signing certificate is expired or near expiration and add a message in the email report.
* During synchronization, the Publisher will check if the WSUS code signing certificate is in the required Windows Cert stores and add it if needed.
* SMTP port automatically set to 587 when ‘Use TLS’ is selected, and to 25 when ‘Use TLS’ is unselected. The port can still be manually edited to account for any port, but the common port for the protocol is set by default.

### Improvements

* Add additional known errors in the log, providing a link to a KB article that may assist with solving the known error.
* Display additional info in the Certificate information wizard on whether the certificate is found in the expected Windows Cert stores.
* SMTP port default to 25 instead of 587 when the feature is in a non-configured state.
*   The Publisher will retry several times when the rename of a folder during an SCCM application upgrade fails. This should help prevent

    ‘Access Denied’ errors that are caused by file locks.

### Fixes

* Fixed an issue where, sometimes, the SupportedProducts.xml file cannot be read during a synchronization.
* Fixed an issue where a machine with a large number of CPU cores may experience high CPU load when running the Intune Scan Wizard.

## 1.8.7.1 - 2020-08-27

### Improvements

* Improved the copying of right-click options from the Updates tab, to the ConfigMgr Apps tab, or the Intune Apps tab.

### Fixes

* Fixed an issue where the Publisher would falsely report that it was not installed on a Software Update Point in some scenarios.
* Fixed an issue where the Intune Updates product list was not reloaded during publisher sync in some scenarios.

## 1.8.5.1 - 2020-08-19

### Features

* You can now [automatically create the security role](https://patchmypc.com/permissions-required-in-sccm-for-base-installation-packages-from-patch-my-pc) for allowing the publishing to create Configuration Manager applications.

## 1.8.4.3 - 2020-08-14

### Features

* Add Anonymous authentication method to send emails.
  * User voice [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-817)
* Intune updates use the description in the SDP for the title.
  * User voice [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-915)
* Split the «Delete Intune Application when a new release is published» option to allow to choose the behavior for Apps and Updates independently.
  * User voice [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-913)

### Improvement

* Add a button to export data in the Intune Apps Manager.
* Add a column to show Classification in the Intune Apps Manager.
* Allow to show «Applications only», «Updates only» are «All» in the Intune App Manager.
* Display the Publisher service's status on the 'About' tab.
* Download timeout is now logged out in minutes and seconds, instead of milliseconds.
* Implement log rollover for Intune detection and requirement scripts.
* Send an MS Teams message and add a line in the Email report if the server runs low on disk space on the PMPC installation or the Wsus Content drive.
* Support for the Contains string operator when searching for an AAD Group.
* The Publisher will notify the user if the installation drive is running low on disk space.
* The Publisher will notify the user if the Publisher is installed on the Site Server, and the server is not also a Software Update Point.
* Tooltips added to buttons on Intune Apps and Intune Updates tabs.
* When several files with the same name are found in the Local Content repo, and subdirectories, we try to identify the right one with the expected digest before falling back to downloading.

### Fixes

* Fixed an issue where custom options are not correctly copied between two tabs when copying enabled products from one tab to another.
* Fixed an issue where reserved characters were not working as expected when searching for Azure AD Groups
* Fixed an issue where the Publisher may display a warning that the certificate is incorrect or missing when it's within 30 days of the expiration date.

## 1.8.4.2 - 2020-08-04

### Features

* Support for Intune Updates
  * [https://patchmypc.com/third-party-patch-management-for-microsoft-intune-now-available](https://patchmypc.com/third-party-patch-management-for-microsoft-intune-now-available)

## 1.8.3.1 - 2020-07-16

### Fixes

*   Changed how Unreferenced Package Folders are found. If third party updates are set to display in WSUS, then they might show up as

    'Unreferenced' by the WSUS content cleanup tool. The publisher now correctly display the list of unreferenced contents.

## 1.8.2.6 - 2020-07-07

### Improvement

* Add even more logging to the Application update, and creation processes to assist with troubleshooting.
* Code optimization and cleanup for Applications

### Fixes

* Fixed a bug where the Publisher service would never timeout during content downloads in some scenarios. This could cause the service to hang.
  * See the [HTTP Download Timeout section](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#HTTP-Timeout) for more information regarding the timeout. The default value is a 15 minute download timeout.

## 1.8.2.5 - 2020-07-02

### Improvement

* Detection script now accounts for user based installs when needed.
* Detection script checks if running as SYSTEM using the SID instead of username.
* Add additional logging to the Application update, and creation processes to assist with troubleshooting.
* Add a new known error to assist with identifying and resolving TooManyCategories for WSUS.

### Fixes

* Fixed a bug where some system cultures would result in incorrect command line parsing.
* Fixed a bug where an Application's content would not be updated when a right click option was selected in some scenarios.

## 1.8.2.4 - 2020-06-26

### Features

* Add an Intune Scan Wizard allowing you to auto-enroll applications based on Intune App scanning
  * [https://patchmypc.com/scan-intune-for-supported-products](https://patchmypc.com/scan-intune-for-supported-products)
* Add all options available in the 'User Experience' for Applications to a new Context Menu option for base installs.
  * [https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#app-user-experience](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#app-user-experience)
  *   User voice

      [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-803)

### Improvement

* Enabled CTRL+F functionality in the Intune tab.
* Product download will fallback to the Internet in case of digest mismatch in local content repository.
  *   User voice

      [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-802)
* Display third party vendor/product count in the Update Modification Wizard.
* Deprecate WSUS v3

### Fixes

* Fixed a bug where the "Exclude from autoenrollment' option was unable to be changed on a product when the setting was configured at the vendor level.
* Fixed a bug where the publishing service could not publish a postponed application if it contained an HTML escaped character.
* Fixed a bug where the Intune Authentication URL was being overwritten by the Intune Scane Wizard

## 1.8.2.3 - 2020-06-25

### Features

* Add an Intune Scan Wizard allowing you to auto-enroll applications based on Intune App scanning
  * [https://patchmypc.com/scan-intune-for-supported-products](https://patchmypc.com/scan-intune-for-supported-products)
* Add all options available in the 'User Experience' for Applications to a new Context Menu option for base installs.
  * [https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#app-user-experience](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#app-user-experience)
  *   User voice

      [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-803)

### Improvement

* Product download will fallback to the Internet in case of digest mismatch in local content repository.
  *   User voice

      [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-802)
* Display third party vendor/product count in the Update Modification Wizard.
* Deprecate WSUS v3

### Fixes

* Fixed a bug where the "Exclude from autoenrollment' option was unable to be changed on a product when the setting was configured at the vendor level.
* Fixed a bug where the publishing service could not publish a postponed application if it contained an HTML escaped character.

## 1.8.2.2 - 2020-06-11

### Improvements

*   We now use a FIPS compliant algorithm when creating Intune applications

    **Fixes**
* Fixed an issue where the checkbox in the MSI installer to enable Intune only mode may not be applied after the installation

## 1.8.2.1 - 2020-06-10

### Fixes

* Fixed issue where the republish option no longer showed for "All Products" and Vendor nodes
* Fixed issue where incorrect workstation counts were shown on certain SSRS reports

## 1.7.9.3 - 2020-05-29

### Features

*   SCCM Database Scan now has option to \["Auto-enable products as

    'Metadata Only' if found, but threshold is not met"]\([https://ideas.patchmypc.com/ideas/PATCHMYPC-I-565](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-565))

    **Fixes**
* Fixed issue where a customer with an expired Intune only license could be stuck in a messagebox loop.

## 1.7.9.2 - 2020-05-26

### Features

* Enhances the display in the Update modification wizard when there is a lot of updates.
* Cache binary for postponed updates allows postponed updates to be published after the download link has changed.

## 1.7.9.1 - 2020-05-22

### Features

*   [Custom right-click options](https://app.gitbook.com/custom-options-available-for-third-party-updates-and-applications) applied at the All Products level will now be retained when the UI is closed, and future products are enabled. UserVoice Idea:

    [Retain the Logging Options in View when Saved at the All Products Level](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-742)
*   Added support for Server 2019 in the [SSRS dashboards](https://app.gitbook.com/free-software-update-compliance-dashboard-reports-for-microsoft-sccm)

    **Fixes**
* Fixed some issues where some links may not work in the SSRS dashboards

## 1.7.8.1 - 2020-05-18

### Features

* Allows creating a self-signed certificate with the private key marked as non-exportable.
* Added new subscription state reporting using Teams or STMP emails

## 1.7.7.1 - 2020-05-13

### Features

*   Added like, dislike, and feedback button in the title bar of the settings tool.

    **Fixes**
* List unreferenced package folders don’t list any folders in some WSUS configuration
*   Added a workaround to handle SCCM apps published with an unsupported language

    **Improvements**
* Web domains of downloaded icons are listed in the DownloadHistory.csv file.
* Added several help links in the UI.
*   Improved logging for known errors linking to KB articles

    **Changes**
* The option to fallback to ConfigMgr package publishing when an application can’t be published as an SCCM application has been removed in the UI due to not being needed
* SQL query default timeout is now 90 seconds from 30 seconds.
* Removed from the UI the option to generate a CSV file with publishing info. The option is always enabled and the file path can be configured with the registry settings : HKEY\_LOCAL\_MACHINE\\\SOFTWARE\\\Patch My PC Publishing Service:PublishingHistoryCSVFolder

## 1.7.6.3 - 2020-04-27

### Features

*   Adds a new column, UpdateEnabled, to the resulting CSV from the SCCM Scan Database Wizard -

    (Idea: [PATCHMYPC-I-645](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-645))
*   UI improvements to the Base Install options

    **Fixes**
* Fixed an issue where double quotes in the command line argument for software updates would not be retained.

## 1.7.6.2 - 2020-04-22

### Fixes

* Fixed an issue where adding multiple Intune assignments with customer deployment deadlines may cause the publisher UI to crash

## 1.7.6.1 - 2020-04-21

### Features

*   Intune assignments created during an application creation or update are now reported in Teams notifications and email alerts

    (Idea:

    [PATCHMYPC-I-700](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-700))
*   Adds a line in the log to specify Intune AppIDs (old and new release) during an application updating (Idea:

    [PATCHMYPC-I-723](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-723))
*   Improves how Azure AD groups are retrieved (Set page limit to 999). We will also now display O365 groups. Adds the ability to search a group based on the group name starts with (Idea:

    [PATCHMYPC-I-718](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-718))

    **Fixes**
* Fixed an issue where the WSUS Maintenance for unreferenced updates would not return folders when the name is longer than 80 characters
* Fixed an issue where file coping during publishing would fail when a file is referenced more than once (e.g., in additional files and pre-command script)

## 1.7.4.2 - 2020-04-08

### Fixes

* Dropdown filters could be edited in the update modification wizard
* Trying to import a KSP CNG based code-certificate leads to an error
* OS requirements were added during an SCCM application upgrade even though they were already there
* The application deployment type Install behavior was not set during the application publishing if the KillProcess option was not enabled

## 1.6.6.1 - 2020-03-03

### Improvements

* Improved the Microsoft Intune options. The options are now available in the Intune Apps tab and not the Advanced tab.
* Improved the installation options for enabling Microsoft Intune only publishing.

## 1.6.4.1 - 2020-02-20

### Improvements

* Adds a new application management tool for SCCM in the application options menu. You can now bulk delete applications created from Patch My PC or bulk delete deployments for applications.
* Changed title format for republished updates to be more granular
* Included updated DLLs for Compression.cab from Wix
* When an update is republished, all previous republished updates can be superseded by the new update that is republished.
* Add email, teams, and logging notifications when an update cannot be revised.

### Fixes

* Fixed an issue where the right-click option for manage logging may display the correct information

## 1.5.9.7 - 2020-02-04

### Improvements

* Use env variables instead of hard-coded path in PowerShell detection script.
*   Other fixes and improvements.

    **Changes**
* Rename Intune preview to Intune Release Candidate.

## 1.5.9.6 - 2020-02-03

### Features

* You can now select a custom code-signing certificate from the computer's personal certificate store. A full WSUS installation is no longer required for code-signing the detection method script used for Intune.
*   Applications will no longer be duplicated in the event the deployment type's source folder was deleted.

    **Fixes**
* Bug fixes and other improvements

## 1.5.9.5 - 2020-01-27

### Fixes

* Fixed an issue where you may receive an error: An error occurred while updating a package in SCCM: OpenDatabase,DatabasePath,OpenMode

## 1.5.9.4 - 2020-01-13

### Improvements

* No longer perform WSUS service checks when the WSUS publishing is disabled for Intune only scenarios.

## 1.5.9.3 - 2020-01-10

### Features

* You can now create assignments for Win32 applications in Microsoft Intune
* The authority URL for Microsoft Intune will be prepopulated
* The publishing service can now be installed on Windows 10 (x64) for a Microsoft Intune only setup.

## 1.5.9.2 - 2020-01-02

### Features

* Added support for creating Microsoft Intune Win32 applications in preview mode.

## 1.5.8.3 - 2019-11-28

### Features

* You can now set a custom folder for temporary downloads of the software update and application content
* You can now set a custom folder for the log save location

## 1.5.8.2 - 2019-11-27

### Features

* You can now trigger a full and delta software update point synchronization from the advanced tab

## 1.5.8.1 - 2019-11-26

### Improvements

* You can now test the SMS Provider connection under SYSTEM-level context

## 1.5.6.1 - 2019-11-21

### Improvements

* Files downloaded for publishing updates are now cached and reused for applications within the same sync cycle
* Support to publish applications in other languages than en-US

## 1.5.5.3 - 2019-11-19

### Changes

* Minor changes to support product renaming for Firefox, Nitro Pro, Nitro Enterprise, and Node.js

## 1.5.5.2 - 2019-11-18

### Improvements

* Improved the accuracy of the SCCM application scan feature to better differentiate between x86 and x64 products based on UserVoice [Improve accuracy of 32/64-bit count results of SCCM Database scan](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-461)

## 1.5.5.1 - 2019-11-12

### Features

*   You can now send Microsoft Teams publishing alerts using a webhook

    **Improvements**
*   The software update point synchronization will be triggered after the update synchronization task rather than waiting for the updates and applications sync.

    **Fixes**
* Minor bugs fixes

## 1.5.4.7 - 2019-10-24

### Fixes

* Minor bugs fixes

## 1.5.4.6 - 2019-10-23

### Features

* You can now configure a custom application name, localized application name, localized application description, and icon

## 1.5.4.5 - 2019-10-21

### Fixes

* Fixed an issue where the UI may crash when enabling a large number of products

## 1.5.4.4 - 2019-10-21

### Features

* You can now exclude products at the vendor level from being enabled in automatic scanning
*   You can now press F4/Shift+F4 keys to go to the next/previous when searching products or vendors

    **Improvements\\**
* When disabling updates, we will now create a RegKey is it doesn't exist to disable self-updates
* Improved logging
* Add support to auto-popular the uninstall command line for 25+ applications in SCCM

## 1.5.4.3 - 2019-10-17

### Features

* You can now enable your software update point to sync when updates are published when your software update point is on a remote site system.
* Preserve User Categories when updating Apps in SCCM
*   Preserve Admin Categories when updating an SCCM application

    **Changes**
*   Set default download timeout to 100 seconds from 30 seconds.

    **Improvements**
* Improved logging for varias actions including download percentages
*   Allows searching backward for products and vendors when clicking

    (Shift+F3)
* Remove leading and trailing spaces in catalog URL, sms provider server name, application source folder path, and timestamp server URL

## 1.5.4.2 - 2019-10-11

### Features

* You can now increase the [HTTP download timeout](https://app.gitbook.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service)

## 1.5.4.1 - 2019-10-10

### Fixes

* Fixed an issue where a custom command line may not be processed if it contained double quotes and a space.

## 1.5.3.5 - 2019-10-07

### Features

* Create a CSV file at the end of each synchronization with a summary of what was published, revised, created
*   You can now set the max log size between 1-10 MB

    **Improvements**
*   Add several log entries when sync fails

    ([EventID=3001-3005](https://app.gitbook.com/windows-event-logging-details-for-patch-my-pc-publishing-service))
* Improved the PowerShell detection method scripts to handle invalid DWORD entries better fixing a "Specified cast is not valid." error message
* Add new[advanced options to improve SQL queries](https://app.gitbook.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service) for large organizations.
* Improve the version comparison in the PowerShell detection method script

## 1.5.3.2 - 2019-10-01

### Features

* Added an option to show and delete unreferenced WSUS folders in the UpdateServicesPackages folder
* Added an option to show/hide already enabled products in the SCCM scan
* Added the ability to start a sync by running the PatchMyPC-Settings.exe with argument /SyncNow (the UI is not displayed)
*   Log events in the Windows event log (Starting/ending sync, success/fail publishing updates)

    **Fixes**
* Distribution point groups containing apostrophe were ignored during distribution
* Various bug fixes

## 1.5.2.7 - 2019-09-19

### Fixes

* Fixed an issue where application detection method scripts may fail on devices with PowerShell version 2. The following output error would be logged to appdiscovery.log
  * Unexpected token '.0' in expression or statement.
  *
    * CategoryInfo : ParserError: (.0:String) \[], ParseException
  *
    * FullyQualifiedErrorId : UnexpectedToken
  * CScriptHandler::DiscoverApp failed (0x87d00327).
  * Deployment type detection failed with error 0x87d00327.
* The select application folder dialog may crash when SmsProvider name is empty are unreachable
* The select application folder dialog may try to connect to SMSProvider with a username and password even if the checkbox is unchecked

## 1.5.2.6 - 2019-09-18

### Features

* You can choose a custom folder in the applications node of the console to move applications to upon creation or updating automatically.

## 1.5.2.5 - 2019-09-16

### Features

* You can now include custom folders for updates and applications.
* You can now specify the subject name when creating a self-signed certificate.
* Display the count of updates and selected updates in the update modification wizard

## 1.5.2.3 - 2019-09-14

### Fixes

* Bug fixes

## 1.5.2.2 - 2019-09-13

### Improvements

* PatchMyPC-ScriptRunner.exe files are updated when SCCM applications are upgraded.
* You can now Import/Export settings from the advanced tab.
* Added the ability to delay updating an application in-place for 7 days after release.

## 1.5.1.2 - 2019-09-04

### Improvements

* If SMTP emails are enabled, we will now include any newly enabled products from the automated SCCM inventory scans.
* If there are pending settings changes unsaved, you will be prompted if you want to save the settings when performing a synchronization.

## 1.5.1.1 - 2019-09-04

### Features

*   You can now configure any custom pre-update script to run before checking any processes to close or skip

    **Improvements**
* Improved logging

## 1.5.0.3 - 2019-08-30

### Features

* Added options to Kill or Skip installations when auto-enrolling new products.
* Application names are now clickable for applications published, and links to the vendors release notes.

## 1.5.0.2 - 2019-08-29

### Features

* Added right-click option for products to be excluded from being automatically enabled during automated SCCM inventory scans.

## 1.5.0.1 - 2019-08-27

### Features

*   You can now automatically enable products to be enabled based on them being detected in the SCCM database.

    **Fixes**
* Fixed an issue where applications may fail to install on Windows 10 when using Latvia language.
* Fixed an issue where you may get an email about the license being expired when in trial-mode.

## 1.4.2.3 - 2019-07-22

### Fixes

* Fixed an issue where the option to copy the installation log to a secondary folder on installation failure would not work correctly.

## 1.4.2.2 - 2019-07-22

### Improvements

* Added an option to copy the installation log to a secondary folder on installation failure.

## 1.4.2.1 - 2019-07-19

### Fixes

*   Updated the detection method script for applications to resolve the following error (Access to the path

    'C:\\\Windows\\\CCM\\\Logs\\\PatchMyPC-SoftwareDetectionScript.log' is denied.) that would occur in AppDiscovery.log in certain builds of Configuration Manager.

## 1.4.1.1 - 2019-07-18

### Features

* Added an option to include abitrary files in the pre/post script dialog box.

## 1.4.0.2 - 2019-07-12

### Fixes

* Fixed an issue where the SSRS report RDL files may fail to upload to SQL Server Reporting Services.

## 1.4.0.1 - 2019-07-10

### Fixes

* This update contains improvements to help support the future release of the application creation feature.

## 1.3.9.5 - 2019-07-09

### Fixes

* Fixed an issue in build 1.3.9.4 where applications may fail to update with error: property DisplayInfo.DisplayInfo.DefaultLanguage: Language En does not match any data in the set

## 1.3.9.4 - 2019-07-09

### Improvements

* Added the application option to "Allow clients to use distribution points from the site's default boundary group."

## 1.3.9.3 - 2019-07-08

### Improvements

* Added support to code-sign the PowerShell detection method script using the WSUS Signing Certificate. This option is enabled by default.
* Organized the Base Install Options dialog.

## 1.3.9.2 - 2019-07-03

### Improvements

* Improved the detection method PowerShell script processing speed for all application deployment types.

## 1.3.9.1 - 2019-07-02

### Features

*   The base installation feature now creates applications in SCCM rather than legacy packages.

    **Improvements**
* You can now configure an offset (in days) for the sync schedule. Based on customer idea: [Schedule Patch Tuesday +1 (Offset From Date)](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-138)
*   When using a custom pre/post update script, it will be run before any Patch My PC defined script. Based on customer idea:

    [Run custom pre-update scripts before any PatchMyPC defined scripts](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-177)
* Added an option to configure the "Install Application Task sequence setting" in the Application Rules options. Based on customer idea: [Change Install Application Task sequence setting during creation](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-184)
*   Added an option to not include the version number in the application name. Based on customer idea: [Application creation: applications without version numbers](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-186)

    **Changes**
* The installed version of the publishing service and whether you have opted into the preview channel will be reported.

## 1.3.7.1 - 2019-06-06

### Fixes

*   Fixed an issue where if you switch from the general tab to the update rules tab very quickly on open the products enabled may reset and the Settings.xml would need to be restored from the

    \\\\\Backup folder.

    **Improvements**
* Added an option to prefix the computer name to the installation log file name to allow you to use a shared path and receive unique log file names for each device.

## 1.3.5.1 - 2019-05-24

### Fixes

* Fixed an issue where if you are using a 24-hour time format in an EN-US server operating system the saved schedule may not reflect correctly in the sync schedule.

## 1.3.4.4 - 2019-05-20

### Fixes

* Bug fixes

## 1.3.4.3 - 2019-05-20

### Features

* Added a new right-click context menu item to add MST transformation files for MSI based product installers.
* Right-clicking on a product will now display the installer technology the product uses (MSI, EXE, or MSP)

## 1.3.2.3 - 2019-04-30

### Fixes

* Fixed an issue where the UI may show not responding for a short period of time on initial open.

## 1.3.2.2 - 2019-04-30

### Improvements

* We will now cache the list of supported products, so in the event, the settings tool can't download the latest products, it will use the last cached copy.
*   When the settings tool is opened, if any products are previously enabled that now have a Patch My PC defined recommended and required Pre/Post script(s) those scripts will be saved in the settings.xml automatically.

    **Features**
* Added support for required Pre/Post-Scripts

## 1.3.2.1 - 2019-04-26

### Improvements

*   When there is a product enabled that requires a [manual content download](https://patchmypc.com/local-content-repository-for-licensed-applications-that-require-manual-download) the product name(s) will be included in the prompt.

    **Features**
* Added support for recommended Pre/Post-Scripts

## 1.2.5.12 - 2019-04-09

### Improvements

* Added subscription level and licensed device count based on feedback in the SCCM slack group.
* We removed the two columns displaying the distribution point group and description in the base installation options dialog.
*   Change the error return for 404 download errors.

    **Fixes**
* Fixed an unhandled exception when you enable base packages when no catalog URL is set.

## 1.2.5.11 - 2019-04-05

### Improvements

* Changes to improve the performance of the license validation check.

## 1.2.5.9 - 2019-04-02

### Improvements

* Revisions to packages are now included in email reports.

## 1.2.5.8 - 2019-04-02

### Improvements

* When using the Scan SCCM for Managed Applications feature, the database server, database name, and connection account details will be retained after a successful query.

## 1.2.5.7 - 2019-04-01

### Improvements

* Split our the following products to be major version specific to allow more specific selection.
  * ESET Endpoint Security
  * ESET File Security
  * Royal TS
  * SketchUp
  * Skype
  * TeamViewer
  * Telerik Progress TestStudio Ultimate
  * VMware Workstation
  * VMware Workstation Player
  * VMware Workstation Pro
  * VirtualBox
  *   WinZip

      **Fixes**
* Miscellaneous fixes

## 1.2.5.6 - 2019-03-29

### Fixes

* Fixed an issue where updated installation packages are not added in the email report
* Fixed an issue where superseded applications may not publish into SCCM
* Miscellaneous fixes

## 1.2.5.5 - 2019-03-28

### Features

* When a package is created for a 64-bit product, the requirements will be configured on the program to only install on 64-bit operating systems
*   If a package fails to be created, the distribution attempt to SCCM distribution points will no longer be performed.

    **Fixes**
* Miscellaneous fixes

## 1.2.5.4 - 2019-03-27

### Features

*   Added an option to change the subject name for email notifications

    **Fixes**
* Fixed an issue where SCCM package creation is malformed when updates are configured to be republished.
* Fixed an issue where products are still listed in the SCCM application scan when the Include Products Already Enable in Scan is not checked.
* Miscellaneous fixes

## 1.2.5.3 - 2019-03-27

### Features

*   Added an option to include text in the body of the email notifications.

    **Fixes**
* Miscellaneous fixes

## 1.2.5.2 - 2019-03-26

### Features

* Disabled the delete option for published updates in the modify published updates wizard.
  * To enable the Delete button, create a new DWORD registry value: Computer\HKEY\_LOCAL\_MACHINE\SOFTWARE\Patch My PC Publishing Service:EnableDeleteUpdates = 1. We only recommend using this option when working with our support team.
*   Added an option to disable timestamping. We generally do not recommend using this unless there is a specific use case. To disable timestamping you can create a DWORD registry value:: HKEY\_LOCAL\_MACHINE\SOFTWARE\Patch My PC Publishing Service:DisableTimestamping = 1

    **Fixes**
* Miscellaneous Bug fixes

## 1.2.5.1 - 2019-03-25

### Features

* Added the new option to enable the creation of base installation packages in SCCM.
* Other feature improvements and bug fixes

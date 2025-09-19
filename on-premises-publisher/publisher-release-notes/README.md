# Publisher Release Notes

_Applies to: Patch My PC On-Premises Publisher_

Details the production release history for Patch My PC's (PMPC's) On-premises Publisher, the most recent release being shown first.

## 2.1.36.0 - 2025-05-05

### Improvements <a href="#improvements" id="improvements"></a>

* When processing a ConfigMgr app, the Publisher will validate that the PackageId found in a package.xml maps to an application deployment type with a matching content source path.
* If a ConfigMgr application copy fails, the left-behind content is also removed.

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a bug that caused the MCP User Notification Timeout to not be translated from minutes to seconds when written to package.xml. The result is a notification being open for 5 seconds instead of 300 seconds, for example.
  * Note: To fix existing apps or updates with this issue [Republish the App or Update](https://patchmypc.com/when-and-how-to-republish-third-party-updates).
* Fixed a bug that resulted in an error when attempting to save a MCP User Notification Timeout Setting.
* Fixed a bug that caused postponed custom ConfigMgr applications to not publish as expected.
* Fixed a bug where the option to select the ConfigMgr folder within the [ConfigMgr application creation options ](https://patchmypc.com/application-creation-options)was not available.

## 2.1.35 - 2025-04-23

### Improvements <a href="#improvements" id="improvements"></a>

* Allow a maximum run time of 1440 minutes for Manage Conflicting Processes for Intune.
* Add the user name, user domain, device name, session ID and Windows OS version to the PatchMyPC-Sriptrunner.log.
* Collect additional information regarding certificate validation failures.
* Add Japanese localization text for Manage Conflicting Processes.
* Stop processing a ConfigMgr application if the copy operation for retention fails. This ensure we do not edit an existing app unless the copy succeeds.
* Added the total sync time to the PatchMyPC.log
* Improved logging when there is a cloud connection, but no Intune deployments in the cloud.

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a bug that caused some right-click options, such as setting an update to metadata only, to take a long time to apply when set at the ‘All Products’ level.
* Fixed a bug that caused the Publisher to fail to load the complete list of selected products from settings.
* Fixed a bug causing the Publisher to fail to process selections from the CVE Import Wizard.
* Fixed a bug that caused the treeview searchbox not to retain the previous search text.
* Fixed a bug causing scriptrunner not to expand placeholder arguments such as %CURRENTDIR% when parsing command line arguments.
* Fixed a bug causing errors similar to ‘Mutex access requested by GetIntuneAppProductFlags but a timeout occurred while waiting for mutex to be released’
* Fixed a bug that caused custom applications to fail if they had two files with the same name inside their content.
* Fixed a bug that caused email reports to erroneously indicate a pause product for tenants that do not have the product enabled.

## 2.1.33 - 2025-02-13

### Features <a href="#features" id="features"></a>

* Support applications in the catalog that download a zip file.
  * Idea: [PATCHMYPC-I-1463](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1463)
  * Note: Additional backend and procedural changes are needed before this will be used. The Publisher can consume a catalog with software that downloads a zip file. We will not add any products like this until Q1-Q2 2025.
  * Scriptrunner will now expand environment variables provided in custom command line arguments.
  * Add support for Patch My PC to configure the ‘Run installation and uninstall program as 32-bit process on 64-bit clients’ option within ConfigMgr. This will not be a customer exposed option in the Publisher, but something that Patch My PC can set to ensure applications install as expected.

### Improvements <a href="#improvements" id="improvements"></a>

* Improve how the Publisher reads and writes settings.
  * Prevent the Publisher from overwriting user setting changes while a sync is happening. Previously, if a user was in the UI and clicked save while a sync was running, the user’s changes could be lost.
  * Prevent the Publisher from losing Intune configuration due to an abandoned mutex.
* If found, the ‘Collect Logs’ button will now include the WSUS softwaredistribution.log.
* Improve the product search function in the Publisher to keep the search box open when no match is found.
* Scriptrunner has improved logic for handling the log location for user-based installations. If the default values are left in the Publisher, the log path will be updated to a user-writable location. This includes the scriptrunner log and the installer log.
* Updated Publisher settings backup retention to retain settings from previous weeks and months.
* Update the Swedish translation for Manage Conflicting Processes based on customer feedback.
* The search functionality in the product treeviews now consider custom applications. Previously the list of custom products would not be included in the search.
* Improved logging during a Publisher synchronization for products that are marked [end-of-life](https://patchmypc.com/how-products-are-handled-at-end-of-life-eol-or-become-incompatible) by Patch My PC.
* Update some labels and logging to be in line with the latest terminology used in Intune.
* The Update ID and Update Title are now written to the PatchMyPC-Scriptrunner log file.
* The username of the user who performed a save in the Publisher is now written to the event log, and to the PatchMyPC log file. Additionally an empty file with a GUID name is included in the CAB so the save event can be matched to CAB file.

### Fixes <a href="#fixes" id="fixes"></a>

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
* Fixed a bug where cloud Product Selections were only displayed in the Publisher if the product was both deployed in the cloud, and selected in the Publisher. Products which are not selected in the Publisher will now properly show as managed by the cloud if a deployment exists.

## 2.1.29 - 2024-11-03

### Improvements <a href="#improvements" id="improvements"></a>

* Intune Updates will now have the icon for the product associated with them.
* Added Czech, Finnish, and Norwegian translations for [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications).
* Fixed Danish translation for [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications).
* Imported banner images are stored in the installation directory of the Publisher instead of referencing the source file.
* Removed the references for the SSRS reports and replaced them with [Advanced Insights](https://patchmypc.com/advanced-insights/overview).
* The Win32AppId is now included in the PatchMyPC-PublishingHistory.csv file.
* Improved the handling of signed scripts when publishing. Sometimes, the Publisher would fail to replace a file and throw an exception. We now ensure the destination file is deleted before moving in the updated file.

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a bug that caused the synchronization to stop if a tenant failed authentication. This impacted the Publisher with an MSP license and a multi-tenant setup.
* Fixed a discrepancy between the PowerShell detection scripts and the ScriptRunner detection logic.
* Fixed a bug with the filtering options for webhook notifications. The notifications should now be correctly filtered when the summary option and scope are set. For example, ‘Send alerts as each product is published…’ is unchecked, and only ‘Include Intune update notifications’ is checked.

## 2.1.28 - 2024-09-26

### Improvements <a href="#improvements" id="improvements"></a>

* Updated [telemetry](https://patchmypc.com/telemetry-data-collected-when-using-the-publisher) to include the list of selected products.

## 2.1.27 - 2024-09-10

### Features <a href="#features" id="features"></a>

* Added support for Microsoft Teams Workflows as a new webhook provider option. With the announced [retirement of Office 365 connectors within Microsoft Teams](https://devblogs.microsoft.com/microsoft365dev/retirement-of-office-365-connectors-within-microsoft-teams/), we now support the new Workflow options. Our Teams notifications have been updated with new ⁠[Adaptive Card](https://learn.microsoft.com/en-us/adaptive-cards/) templates.

### Improvements <a href="#improvements" id="improvements"></a>

* Configured [return codes](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#manage-return-codes) are updated on sync for ConfigMgr applications, Intune applications, and Intune updates. If there is a mismatch between the settings in the Publisher and the published application, then the return codes from the settings will be applied. It is no longer necessary to republish a product to update the return codes.
* Add support for passing additional headers when downloading binaries. This is metadata maintained by Patch My PC.

### Fixes

* Fix a bug that caused republishing a custom ConfigMgr application with additional files to fail in some scenarios.
* Fixed a bug where the return codes in settings could be duplicated if the treeview was refreshed, or you switch tenants in a multi-tenant setup.
* Update Intune detection to account for registry detection checking for a nonexistent property. We now allow a NotEquals check for a property that might not exist. Previously, this would cause an unhandled exception.

## 2.1.26 - 2024-07-25

### Other

* Signed the installer with our renewed code-signing certificate.

## 2.1.25 - 2024-06-26

### Features <a href="#features" id="features"></a>

* Manage return codes
  * Idea: [PATCHMYPC-I-556](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-556)

### Improvements <a href="#improvements" id="improvements"></a>

* Use a temporary staging directory for binary downloads when processing ConfigMgr applications
* Improved handling of the cloud connection.
* Improved how ConfigMgr content is resolved to ensure we choose non-retained applications if present.
* The tooltip and icon for Manage Conflicting Processes suggested configurations are now more contextual.
  * If configured to Kill or Notify, the tooltip and icon are removed
  * If configured to Skip, the icon is shown, and the tooltip says, “Manage Conflicting Processes is recommended for this product and will be configured to Skip by default”
  * If configured to ‘Perform the installation,’ the icon is shown, and the tooltip says, “Manage Conflicting Processes is recommended for this product but is currently not configured”

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a bug that caused the ‘Prevent the end-user from opening an application while the application is updating’ feature to not work for ConfigMgr or Intune applications in some instances.
* If a product is renamed, the requirement rules for Intune Updates may not update as expected. This applies to custom applications and Patch My PC catalog applications. The old requirement rule for an Intune Update would be left behind. The requirement rules should now be maintained as expected when a product is renamed.

## 2.1.24 - 2024-05-30

### Fixes <a href="#fixes" id="fixes"></a>

* If the temporary file location configured in the Publisher does not exist, we now fall back to the system temporary directory. Previously, if this directory did not exist the PatchMyPcService would fail to start.
* Fixed a bug where the secrets, such as the Intune application registration secret, would not be saved in the correct format on the first UI open for a new install.

## 2.1.23 - 2024-05-29

### Features <a href="#features" id="features"></a>

* Support for ‘Allow available uninstall’ in Intune
  * Idea: [PATCHMYPC-I-3213](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-3213)
* Implement coexistence
  * Coexistence ensures the customer is aware when a product is already managed by Intune Apps for Patch My PC Cloud.

### Improvements <a href="#improvements" id="improvements"></a>

* Improve our regex usage in the detection of applications published by Patch My PC.
  * The regex string is now stored in base64 in the PowerShell script to prevent Intune from clobbering UTF8 characters.
* Enable the ‘[Manage Installation Logging](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#install-logging)‘ option at the root of Customer Apps if at least one product supports it.
* Enable the ‘[Manage application update and retention](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#new-application)‘ option for Custom apps on the ConfigMgr tab.

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a bug that caused custom applications with a main file larger than 2GB to fail to process.
* Fixed a bug that caused a circular reference when processing Intune dependency relationships with greater than 2 layers.
* Fixed a bug that caused ConfigMgr applications to be copied for retention even if the current version fails to download.
* Ensure proper wildcard support for ? in detection.
* Fixed an incorrect translation for Manage Conflicting Processes. The default English text had the word ‘Applications’ translated.

## 2.1.22 - 2024-04-16

### Features <a href="#features" id="features"></a>

* It is now possible to adjust the chunk size used for uploading chunks to Azure. It can be [adjusted between 2MB and 12MB](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#AzureUploaderChunkSize).

### Improvements <a href="#improvements" id="improvements"></a>

* PowerShell detection scripts no longer call whoami. This resolves issues where the PATH environment variable may have conflicting whoami processes.
  * The ‘[recreate detection](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#RecreateDetection)‘ right-click option can be used to generate new scripts with this change. Otherwise, products will have the script updated when a new version is released.
* Product selections are stored and matched based on a product Id
* A message box will appear when a ‘[latest](https://patchmypc.com/products-multiple-versions-patch-my-pc#topic2)‘ product is selected. This message box contains a brief note about how products with multiple versions are handled and provides a help button for [more info](https://patchmypc.com/products-multiple-versions-patch-my-pc#topic2).
* Improve how we search for ConfigMgr application content.
* When creating the cloud connection in the Publisher, the System Default browser will now be used.
  * If needed, the embedded web browser can still be used with a [registry flag](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#MsalUseEmbeddedWebView).
* The ‘[Collect Logs](https://patchmypc.com/logging-options#collectlogs)‘ button now collects all PowerShell detection scripts modified within the last 7 days. The scripts are renamed to have a .txt extension before being added to the zip file.
* Additional default translations added to Manage Conflicting Processes
  * Added German, Danish, Norwegian and Swedish
  * Fixed Dutch translation
* Icons in the product treeview now indicate if the product requires local content, or is configured to skip the install if running by default.

![An image showing the Patch My PC Publisher product treeview with icons and tooltips indicating if a product needs a manual downoad, or Manage Conflicting Processes configured.](../../_images/CallToActionIcons.png)

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a bug that caused a null reference exception if a recommended pre script, and a recommended post script were configured on a product.
* The configured proxy will be used to get an access token during cloud connection creation.
* Disconnecting from the cloud tab did not save to settings.

## 2.1.21 - 2024-03-07

### Fixes

* Cloud features were not using the configured proxy. The proxy configured in the Publisher will now be used.

### Other

* Update Patch My PC TOS

## 2.1.20 - 2024-02-21

### Features <a href="#features" id="features"></a>

* Custom apps
  * Idea: [PATCHMYPC-I-1303](https://patchmypc.aha.io/ideas/PATCHMYPC-I-1303)
  * [Documentation](https://patchmypc.com/ui-doc-publisher-cloud)

### Improvements <a href="#improvements" id="improvements"></a>

* Improve how the list of custom products is queried from the cloud.
* Improve the cloud connection flow to account for the EU region.
* Various typo corrections in the UI and in the log.
* Improve logging for retained ConfigMgr applications.
* Expand out aggregate exceptions when they are logged.
* Improved user experience both for a disconnected cloud configuration and an empty custom app list.
* Use less memory when uploading .intunewin files to Intune.
* Improve the user experience when the ConfigApi is not available
  * The UI can now start without the ConfigApi being available. A popup message will still appear indicating it cannot be reached.
  * When this is not available, the cloud features of the Publisher will be disabled.

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a bug that made connecting to an EU Patch My PC cloud customer inconsistent.
* Fixed a bug causing the copy between tab options not to work as expected when custom applications are configured.
* Fixed a bug where ESP associations would copy between the Intune Apps and Intune Updates tab.
* Improved how .intunewin files are handled to ensure we can process large files.
* Fixed a bug that caused some right-click options to not clear their state as expected for custom apps.
* Editing Manage Conflicting Process options did not light up the Apply button.
* Fixed a bug that caused the Publisher to fail to retry when uploading chunks to Azure.
* Fixed a bug where a custom application download may compare hash against an older version of the custom application’s hash.
* Fixed a bug that caused the treeview to have a yellow background, as if no products are selected, even when products were selected.

## 2.1.19 - 2024-01-16

### Features <a href="#features" id="features"></a>

* Ability to create Custom App updates and base installs (Public preview)
  * Idea: [PATCHMYPC-I-1303](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1303)
  * The Publisher must have ‘[Install preview builds](https://patchmypc.com/preview-channel)‘ checked in the About tab.
  * [Setup docs](https://patchmypc.com/ui-doc-publisher-cloud)
  * Custom Applications are supported in the ConfigMgr apps, Intune apps, and Intune updates tabs.
  * A license with one of the below subscription levels is required.
    * Enterprise Plus
    * Enterprise Premium
    * MSP
* Implement Publish Now for Custom Apps
* Support detecting software that translates DisplayName
  * Idea: [PATCHMYPC-I-1335](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1335)
* Add support for configuring Win32 application max runtime in minutes
  * ![](../../_images/max-runtime.png)

### Improvements <a href="#improvements" id="improvements"></a>

* \*\*\* Report lines have been updated.
  * As the catalog grows and the number of syncing products increases, our \*\*\* report line has gotten too long! CMTrace does not parse the line, and it will not show it. To prevent this, we have split up the report line into one line per type. Below is an example.
  * ![Patch My PC log file with four separate report lines all prepended by \*\*\*](../../_images/report-line-change.png)
* Implement certificate pinning. All requests to Patch My PC domains will have the certificate validated.
* Implement a safety check prior to deleting a ConfigMgr application. In some instances, the SMS provider returns an empty list of apps instead of a connection exception. To account for this, we ensure at least one Site is returned by the SMS provider prior to application deletion.
* ConfigMgr script size is reduced. No functional changes. This should help with metadata download issues over CMG.
* Add support for the ? wildcard character in detection.
* Improve some popup notifications to direct the user to the correct tab.
* Improve cleanup during service shutdown.
* Update the default login authority for Intune. It is now [https://login.microsoftonline.com](https://login.microsoftonline.com/)
  * This will not affect existing Intune configurations. It is only a change to the defaults for a new connection.
* Implement an attempted reconnect when a WMI query fails against the SMS provider.
* Improved scriptrunner logic for finding uninstall strings. DisplayVersion will now have any “-” or “\_” replaced by a “.” when searching for uninstall strings. This matches the behavior of our script based detection.

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a dead ‘More Info’ link for WSUS certificate management.
* Fixed a bug causing dependencies to be removed from an Intune Win32 application when republishing.
* Fixed a bug where publish now and delayed ConfigMgr apps did not work as expected.
* Fixed a bug that caused a new install of Patch My PC Publisher to be in ‘Intune Only Mode’ regardless of the checkbox state.
* Servers are no longer included in Intune device counts.
* Resolved a race condition which caused the additional webhook filtering options to be unavailable in some instances.
* Improved download engine logging to include the URL when the download fails. This was a regression that is now resolved.
* The logging path for Intune [Manage Installation Logging](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#install-logging) incorrectly defaulted to the ConfigMgr path. It is now corrected to the Intune default path for logging.
* For some sync schedules, the ‘Next Sync’ time displayed in the General tab was in UTC instead of local time. The correct time should now be displayed.
* Fix logging during the creation of Intune products when local content lookup fails. The Publisher would incorrectly log that the existing application would be deleted.
* Fixed a bug causing Enforced Uninstall Arguments to be ignored for ConfigMgr apps. This resulted in some ConfigMgr apps being created with an uninstall that may not work as expected. The next sync after the Publisher is updated will fix these products’ uninstall configuration.
* The connection name is now required in the Cloud tab.
* Fixed a bug that caused a Null Reference Exception when exiting the [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) configuration in the Intune apps or Intune updates tab.
  * This was a regression that only impacted preview builds
* Fixed a bug that caused the [custom naming convention](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#IntuneNamingConvention) for ConfigMgr applications to be overwritten during a sync in some cases.
* Fixed a bug where the authorization token can expire when connecting to Custom Apps, requiring a service restart.
* Fixed a bug where Right-Click selections for “All Products” on the “Intune Apps” tab would be lost when custom apps was enabled.
  * This was a regression that only impacted preview builds

## 2.1.18 - 2023-10-16

### Features <a href="#features" id="features"></a>

* Sync only selected apps/updates during a sync
  * Idea: [PATCHMYPC-I-468](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-468)
* Allow the management of Delivery Optimization configuration for Intune assignments.
  * Idea: [PATCHMYPC-I-2071](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2071)
  * Note: Existing DO configuration on an assignment will also carry forward now when a new version of the software is Published.
* The [Intune Application Manager Utility](https://patchmypc.com/intune-application-manager-utility) now has some multi-select bulk options.

![A right-click menu in the Intune App manager tool, showing the options available. Manage DO priority. Manage ESP associations. Delete assignments. Delete applications. Extract content(s).](../../_images/intune-app-man-bulk-options-zoomed.png)

### Improvements <a href="#improvements" id="improvements"></a>

* Implement a new download engine across all components.
* Detection method improvements.
  * Support parsing version numbers that use – or \_ instead of .
* Improved logging regarding installer downloads and sourcing.
* Use CSV-based reporting endpoints for detected software per-computer.
  * This should prevent 429 responses when getting the list of devices with an application.
* WMI connection test to SMS provider prior to deleting ConfigMgr content.
* Improve cleanup of files during the synchronization of Intune.
* Updated the “Enabled” header of CSV exports in scan wizards to be less specific.
* OK button has been changed to ‘Save and Close’
  * Open to feedback on this change. We have received a fair number of reports that it is unclear the ‘OK’ button will close the UI.

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a bug where the wrong ID property was shown in the ‘[Show Package Info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo)‘ tool for the update ID.
* Fixed a bug where Manage Conflicting Processes may be enabled if [‘Add the executable name in the deployment type’s install behavior’](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#install-behavior) is enabled. This is unexpected behavior that will no longer occur.
* Fixed a bug where multiple threads could access some components of settings at the same time, causing a race condition.
* Fixed a bug where the ‘Change Visibility’ option for WSUS updates would not work if the WSUS DB is called something other than SUSDB.
* Fixed a bug that caused the right-click menu at the root to sometimes not display correctly.
* On the ConfigMgr Apps tab, if the option «Add the executable name in the deployment type’s install behavior» is enabled, the Manage Conflicting Process is automatically enabled to kill processes.
* Fix crash when sorting some columns in the [Manage Assignments tool](https://patchmypc.com/intune-application-manager-utility).
* Fixed a bug that would cause a republished Intune product to have the content for the latest version and the metadata for version n-1.
  * This would occur if the republish flag is set and there is a new version of the application in the catalog.
* The list of Intune assignment filters is now filtered to Windows.
* Fixed a bug where in some scenarios, the republish flag would not be removed after a sync.
* Fix a possible null reference exception when loading assignments for bulk delivery optimization edits.
* Fixed a bug where the custom logging path may be reset to defaults instead of inheriting the expected value.

## 2.1.17 - 2023-09-08

### Fixes <a href="#fixes" id="fixes"></a>

* General security fixes and improvements

## 2.1.16 - 2023-07-06

### Improvements <a href="#improvements" id="improvements"></a>

* Update the Intune [Application Manager Utility](https://patchmypc.com/intune-application-manager-utility) to use the [aggregate reports](https://learn.microsoft.com/en-us/mem/intune/fundamentals/reports-export-graph-available-reports) for both the collection of applications, as well as application extended info. This prevents a 429 when retrieving the data.

### Fixes <a href="#fixes" id="fixes"></a>

* Updated Publisher to reflect changes in Graph API schema. This should resolve issues with the [Patch My PC Intune reports](https://patchmypc.com/power-bi-reports-for-microsoft-intune-third-party-updates).

## 2.1.15 - 2023-06-14

### Features <a href="#features" id="features"></a>

* Add support for .cmd files in pre/post-scripts.
  * Idea: [PATCHMYPC-I-2745](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2745)

### Improvements <a href="#improvements" id="improvements"></a>

* The Update ID is now an available column in the [Show package info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo) tool.
* Updated some graph calls to use a smaller page size. This reduces the chance of receiving a 429 or 503 response from graph.
  * The page size is configurable from 20-999 in the Advanced tab of the Publisher.
* The product treeviews are now sorted by Vendor and then Product Name automatically.

### Fixes <a href="#fixes" id="fixes"></a>

* Fixed a bug where a ConfigMgr application’s supersedence relationship was lost when the application was upgraded in place.
* Fixed a bug where the sorting of products in the email report was in reverse alphabetical order.

## 2.1.14 - 2023-04-11

### Improvements

* Adjusted log levels of some lines to assist with troubleshooting.
* Update context menu items to reflect new labels in ConfigMgr for featured apps.
* Update several labels in the UI to be more clear on their functionality.
* The ability to set ‘Prevent the end-user from opening an application while the application is updating’ is now only allowed at the per-product level. This setting is only needed in specific scenarios, and enabling it for all products can be problematic.

### Fixes

* Fixed a bug where Intune device counts are not reporting properly.

## 2.1.13 - 2023-03-27

### Features

* Email and Webhook notifications now include information about delayed ConfigMgr applications during each sync.
  * Idea: [PATCHMYPC-I-1862](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1862)
* Add support for creating an Available assignment for All Devices. This was previously not supported by Intune. Support has been added, and the Patch My PC UI now allows it as well.

### Improvements

* Added the option to import CAB files when importing tenants.
* Email and Webhook notifications are now sent when a delayed ConfigMgr application fails to download. Previously a notification would only happen if the Publishing failed after the delay.
* Improved the cleanup of registry keys related to ‘Prevent the end-user from opening an application while the application is updating’ in [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications).

### Fixes

* Fixed a bug where PowerShell scripts for Intune were created with an encoding of UTF8 with BOM. They are now encoded as UTF8 without BOM, which is the recommended encoding based on Microsoft documentation.
* Fixed a bug where a malformed ConfigMgr folder item (SMS\_ObjectContainerItem) would be created the first time the Publisher moved a ConfigMgr application. The result was a folder that could never be deleted.
* Fixed a bug where having a product marked with exclude from auto-publishing rules and a custom naming convention or pause set would cause invalid XML to be generated.
* Fixed a bug where the Collect Logs feature would fail if a company name contained characters that are invalid for file names.
* Fixed a bug where PatchMyPC Scriptrunner logging did not use an invariant datetime format. This could cause CMTrace to fail to parse the logs.
* Fixed a bug where an exception may occur if deleting a large number of Intune Applications using the Intune Application Manager Utility
* Fixed a bug where some data exports would result in malformed date time strings. This occurred if a culture used the same character for the number group separator and for time parts.
* Fixed a bug where ConfigMgr detection script logging did not use an invariant date-time format. This could cause CMTrace to fail to parse the logs.
* Fixed a bug where Manage Conflicting Process logging did not use an invariant date-time format. This could cause CMTrace to fail to parse the logs.
* Fixed a bug where the option to abort an uninstall if the prescript failed caused an argument parsing exception.
* Fixed a bug where the automatic backup of setting changes would fail in certain cultures due to a date-time parsing issue.
* Fixed a bug where custom naming conventions were copied between tabs. We no longer copy naming conventions when copying products between tabs.

## 2.1.12 - 2023-01-20

### Features

* Enable [Right-Click Options](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications) for MSP-based updates
  * Idea: [PATCHMYPC-I-614](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-614)
* Intune option added to ‘[Copy requirements](https://patchmypc.com/intune-application-creation-options#CopyRequirements)’ for Intune products. This can be configured globally, per vendor, or per product.
  * Idea: [PATCHMYPC-I-1501](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1501)
* [Recreate Detection](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#RecreateDetection) right-click option for Intune
  * Idea: [PATCHMYPC-I-2605](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2605)

### Improvements

* If a PMPC-defined pre or post-script is missing from the content source for ConfigMgr applications, then the Publisher will redownload it during a sync or republish.
* The expected and actual hash of files found in the local content repository is now added to the log in debug mode. This has always been the case for files downloaded from the internet.

### Fixes

* Fixed a bug where non-Windows devices may show up in the [Intune scan wizard](https://patchmypc.com/scan-intune-for-supported-products) drill-in.
* Fixed a bug where republishing an Intune product would cause the application to be deleted from Intune if retention was also enabled and set to zero.
* Fixed a bug where the Publisher would not check the WSUS certificate validity unless at least one WSUS update was selected.
* Fixed a bug where the requirements for Workstation or Server OS would not be set for postponed ConfigMgr applications.

## 2.1.11 - 2022-12-16

### Improvements

* Improved the content of alerts when additional files or folders are missing when Publishing a product
* The ‘Configure SMS Provider connection’ button is no longer highlighted if unconfigured in WSUS Standalone Mode.
* Improved the logging for SMTP initialization and error handling.
* All titles in the email report now link to release notes if available.

### Fixes

* Fixed a bug where the Publisher would not add a PMPC-defined script to an existing product.
* Fixed a bug where Scriptrunner did not append the provided Silent Uninstall Arguments to MSI uninstalls.
* Fixed a bug where some UI listviews had a broken filter.
* Fixed a bug where the Manage Conflicting Process window may be offset from the bottom right corner.
* Fixed a bug where the [Pause](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#pause-product-updates) was never removed from Intune applications.
* Fixed a bug where the Publisher would check for the WSUS code signing certificate even if updates were disabled in some scenarios.
* Fixed a bug where the DateTime formats in the Usage Statistics section of the Publisher were inconsistent.
* Fixed a bug where some temporary folders were not cleaned up by the Publisher. These will be retroactively cleaned up once this build is installed and running.

## 2.1.10 - 2022-11-17

### Improvements

* Added a filter for Superseded to the [Modify Updates Wizard](https://patchmypc.com/modify-published-third-party-updates-wizard).
* Adjusted some log levels and log text to be clearer.
* Added additional logging when the proxy settings are loaded in the event of a failure.
* Add the ability to limit the number of threads used during the upload of Intune packages.
  * [Documentation](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#AzureUploaderMaxThreadCount)
* Scriptrunner will now log out a comma-separated list of all public desktop shortcuts if the installing product is configured to delete desktop shortcuts.
  * This is to help troubleshoot when icons for applications are not deleted.
* Improved how running processes are enumerated for [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) making the popup more responsive.
* Implemented a ‘retry’ in the event of failure for many critical interactions with Azure via Microsoft Graph.
* The Publisher will delete files from the download cache if there is a hash mismatch for the file. This makes the root cause of Publishing failure easier to identify.

### Fixes

* Fixed a bug where whitespace at the beginning or end of the Organization Name for [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) would cause the property to fail to parse correctly.
* Fixed a bug where old setting backups would not rename properly, causing an error during settings backup in some cases.
* Fixed a bug where some network operations would not use the configured proxy.
* Fixed a bug where the code signing of ConfigMgr detection scripts may fail to validate the digital signature on the endpoint.
* Fixed a bug where the [UseGSInstalledSoftware](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#topic3) registry option would cause the ConfigMgr database scan to never perform a query.
* Fixed a bug where a failure to download an icon would cause a product to fail to publish.

## 2.1.9 - 2022-10-14

### Fixes

* Fixed a bug where selecting Intune Standalone Mode during the initial installation of the Publisher would not hide the Updates and ConfigMgr Apps tabs.
* Fixed a bug that caused a failure to rename legacy settings backup CAB files.
* Fixed a bug where Scriptrunner would fail to parse the registry when searching for Uninstall keys if there is an empty string in the SystemComponent property.
* Fixed a bug where [Intune Dynamic Assignments](https://patchmypc.com/manage-dynamic-assignments) may unexpectedly match against all selected updates.
* Fixed a bug where the ‘[Republish…](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#republish-updates)‘ option is not unchecked on Intune products if the UI is left open while the synchronization runs.

## 2.1.8 - 2022-10-10

### Improvements

* Improve speed of creating .intunewin files for Intune package creation

### Fixes

* Fixed a bug where ConfigMgr applications would fail to install with error code 0x80070057 or “The parameter is incorrect ” during the installation.
  * If an existing application has this problem in your environment you will need to [republish](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#republish-updates) the affected application.
  * The trigger for this bug is having the ConfigMgr option set to “[Update existing application’s metadata…](https://patchmypc.com/base-install-update-options-explained#topic1)“
  * This bug was introduced in preview version 2.1.6.35 and carried through to production version 2.1.7.0.

## 2.1.7 - 2022-10-06

This release contains a variety of features, improvements, and fixes, as noted below.

This will be made available via the self-update channel over the next 2 weeks. You can upgrade in place now by downloading the latest [**MSI installer**](https://patchmypc.com/publishing-service-setup-documentation).

{% hint style="info" %}
**Note:** Starting with this production build, Patch My PC Publisher now requires a minimum of Microsoft .NET Framework 4.6.2.
{% endhint %}

### Features -

* ConfigMgr and Intune scan wizard allow drilling into list of devices where the software was detected.
  * Idea: [PATCHMYPC-I-2042](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2042)
* Ability to enforce timestamping, making it a terminating error for the publishing of a product
  * Idea: [PATCHMYPC-I-2112](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2112)
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
* Allow variables to be used to customize the ConfigMgr application name and localized application name. This provides parity with the Intune feature for customized names. The variables available are below.
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
* Allow the same Azure group to be assigned multiple times for Intune assignments. This allows a group to be used as both an include, and an exclude.
  * Idea: [PATCHMYPC-I-2322](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2322)
* Pass variables into pre and post-scripts.
  * Note: the %ProductName% and %VendorName% variables are Base64 encoded when they are passed to the pre and post-scripts. It will need to be decoded. Patch My PC will provide a sample PowerShell snippet to decode the resulting parameter.
  * Idea: [PATCHMYPC-I-1348](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1348)
* Extract content from ConfigMgr applications.
* Extract content from WSUS updates.
* Azure app registration secret or certificate expiration is now shown in the Intune Options form.
* Alerts are now sent via email and webhook when secret or certificate expiration is near.

### Improvements

* When exceptions are thrown in the Manage Assignments form, they are now handled better by presenting a popup with the exception and a link to related documentation.
* Main form accessibility has been improved.
  * Accessibility names are assigned to many controls to provide context
  * Alt-codes are added to most buttons that did not have them before
  * Right-click options are now accessible via the Apps keyboard button or shift-F10
* When a default Patch My PC provided translation exists for a language selected in [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) it will now automatically populate the text upon adding the language.
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
* Improved child-form handling in some cases, so they now open in the center of the parent form.
* Multi-selection views, such as selecting application scopes or categories, now use a consistent form that allows filtering.

### Fixes

* Fixed a bug that caused the Paused products section in the email alert to be empty.
* Fixed a bug where we would not put back the version on retained applications if the configuration was set to remove the version from application names and update existing application metadata.
* Fixed a bug in the [Intune application manager](https://patchmypc.com/intune-application-manager-utility#topic3) tool that caused an unhandled exception if you attempted to edit an assignment with a deadline in the past.
* Fixed a bug where the settings backups were stored in a non-sortable format. This bug was introduced in preview 2.1.6.1 and would only impact customers who opted into preview.
* Fixed a bug where the filters were not applied in the scan wizards when filtering the data. This bug was introduced in preview 2.1.6.1 and would only impact customers who opted into preview.
* Fixed a bug where the ConfigMgr database scan may throw an exception due to a malformed query. This bug was introduced in preview 2.1.6.1 and would only impact customers who opted into preview.
* Fixed a bug where the logging option to copy failed logs to a share was not retained. This bug was introduced in preview 2.1.6.1 and would only impact customers who opted into preview.
* Fixed a bug where failing to copy additional files did not cause an Intune product to fail to publish.
* Fixed a bug where localization files for Manage Conflicting Processes may not be copied correctly in some cases.
* Fixed a bug where the WSUS Options window was not scrollable.
* Fixed several UI navigation bugs on the main form.
* Adjusted encoding of detection and requirement scripts to use UTF8. Some scripts were failing to sign with the previous encoding.
* Fixed a bug where the Manage Conflicting Process Organization Name was not retained when republishing a ConfigMgr application.
* Fixed a bug where the wrong URL was used for Microsoft Graph batch requests in some cases.
* Fixed a bug where the buttons in Managed Conflicting Process may not fit the text in some translations.
* Fixed a bug where the ConfigMgr app options window is not resizable.
* Fixed a bug where the Manage Conflicting Process Organization Name would not be set when a ConfigMgr application was revised.
* Fixed a bug where settings could not be saved if the internet was unreachable.
* Fix some typos 🙂

## 2.1.6 - 2022-06-15

### Improvements

* Setting [Delete Desktop Shortcut…](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#delete-shortcut) or [Disable Self-Updater](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#disable-updates) at the vendor level will now display the list of affected products similar to when these selections are made at the All Products level.
* Updated language in the Update Republish message box to reflect new UI changes for Advanced WSUS options.

### Fixes

* Fixed a bug where a sync may run multiple times back to back.
* Fixed a bug where Intune authentication did not use the configured proxy.
* Fixed a bug where [republishing](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#republish-updates) an Intune application or update would not update the code signing configuration of the detection script. Republishing an Intune application or update will now update the detection and requirement scripts and code signing configuration as needed.

## 2.1.5 - 2022-06-02

### Features

* Include server name in Publisher upgrade notification email and Teams/Slack notification.
  * Idea: [PATCHMYPC-I-2136](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-2136)

### Improvements

* Adding German and Dutch translations to [Manage Conflicting Processes](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#manage-conflicting-processes)
* Intune Filter viewing and configuration is now available in all instances of managing Intune Win32 assignments in the Publisher.
* All setting backups are now in a .CAB format. The import setting option now allows for .XML or .CAB import to ensure we support importing older setting files.
* The [Delete desktop shortcut…](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#delete-shortcut) right-click option now removes shortcuts from the user desktop for user-based applications.
* The SMS provider button is now highlighted in the WSUS options if the SMS provider is not configured.
* Updated default [Manage Conflicting Processes](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#manage-conflicting-processes) banner.
* ConfigMgr operating system requirements are now recreated when an application is updated. This ensures new operating systems such as Windows 11 or Server 2022 are added as applications are updated in place.

### Fixes

* Fixed a bug where scriptrunner may fail to find the uninstall string in the registry for some products.
* Fixed a bug where scriptrunner may fail to validate an installation after the installer completes causing a 3-minute delay after the installation completes.
* Fixed a bug where [Pause](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#pause-product-updates) does not account for postponed binaries. If there is an existing postponed binary it will publish even if a pause is set.
* Fixed a bug where some publishing summarization info was miscounted in the PatchMyPC.log file.
* Fixed a bug where the Publisher would leave behind an empty folder when Publishing a ConfigMgr application and the download fails.
* Fixed a bug where a version number would be appended to the current ConfigMgr application instead of the retaining application if the download fails. This bug affected customers who had the ‘Do not include version…’ option configured as well as the ‘Retain…’ option.
* Fixed a bug where an empty Intune tenant is written to settings causing errors when the Publisher attempts to query the invalid tenant.
* Fixed the layout of the [Add MST transformation file](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#mst-transform) form.
* Fixed a bug where we may fail to query for Distribution Point groups if the name or description is DBNull instead of an empty string.
* Fixed a bug where the ConfigMgr SUP sync would not start after a Patch My PC Sync if only updates using local content were published.
* Fixed a bug where the Intune auto-publishing may fail in some cases when right-click options are configured.

## 2.1.4 - 2022-05-04

### Features

* Add Intune multi-tenant support
  * Idea: [PATCHMYPC-I-595](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-595)
  * Requires MSP license
* Dynamic Assignments for Intune
  * Idea: [PATCHMYPC-I-1433](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1433)
  * [Documentation](https://patchmypc.com/manage-dynamic-assignments)
  * Requires Enterprise Plus
* Allow Intune assignment and ESP options to be set per product to override global options.
  * Idea: [PATCHMYPC-I-1831](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1831)
* Per product retention setting for Intune Apps and Updates
  * Idea: [PATCHMYPC-I-1568](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1568)
* Validate the hash of pre/post scripts on sync as well as during a republish.
  * Idea: [PATCHMYPC-I-1946](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1946)
* Collect Logs button now prepends the file name with the company name from the license.
  * Idea: [PATCHMYPC-I-1904](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1904)
* The email report now converts size to a readable format such as MB or GB instead of bytes.
  * Idea: [PATCHMYPC-I-1331](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1331)
* Support for Intune Filters
  * Idea: [PATCHMYPC-I-1434](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1434)
  * Requires Enterprise Plus
* Certificate Authentication for Azure App Registration
  * Idea: [PATCHMYPC-I-1540](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1540)
* Option to pause creation of updates or applications for specific products
  * Idea: [PATCHMYPC-I-1554](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1554)
  * Requires Enterprise Plus
* Allow per-tenant branding for Manage Conflicting Process

### Improvements

* CSV files are now saved with UTF-8 formatting.
* PatchMyPC.log file now includes the timestamp for the catalog that is processed.
* When a download happens we now write the redirected URL to the PatchMyPC.log as well as in the PatchMyPC-DownloadHistory.csv.
* The Publisher will now retry every 10 seconds up 12 times when saving Package.xml for ConfigMgr applications. This helps account for file locks caused by antivirus.
* The email report has been updated (dark mode)
* Add an operator dropdown in the filter options for Intune and ConfigMgr scan wizards
* Improve Manage Conflicting Process configuration window to better support scaling

### Fixes

* Fixed a bug where Intune ADR would publish both an Application and an Update.
* Fixed a bug where we might fail to match a running process with Manage Conflicting Processes if the case of the process name did not match.
* Fixed a bug where illegal characters were allowed in file paths, such as a custom log path.
* Fixed a bug where an application may report being automatically enabled during every sync in some scenarios.
* Fixed a bug where the Manage Conflicting Process UI would not show up for a user-based application.
* Fixed a bug where the Manage Conflicting Process UI would not show for an Intune application when the user is not an Administrator.
* Fixed the Collect Logs button so it takes into account custom log paths as defined in the Publisher.
* Fixed a bug causing enter to close the group search form for Manage Assignments when in the group input textbox.
* Fixed a bug where PatchMyPC-Scriptrunner may throw an exception during log cleanup if the folder does not exist
* Fixed a bug where the publishing summary in the PatchMyPC.log would not include products published from the local content repository
* Fixed a bug where changes to Intune assignments are applied even if the assignment form is cancelled
* Fixed a bug where the Manage Conflicting Process window would not show up when the product install is triggered via Company Portal as a non-admin user
* Fixed a bug where ConfigMgr app retention setting right-click option is not checked when configured
* Fixed a bug where the Updates (WSUS) tab could be used while on an Intune license

## 2.1.3 - 2022-02-04

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

## 2.1.2 - 2021-12-23

### Features

* Collect Logs button added to the Publisher. Will create a .zip file of files useful for troubleshooting.
  * Idea: [PATCHMYPC-I-1750](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1750)

### Improvements

* If the ConfigMgr applications are configured to remove the version from the name, and there is application retention configured we will now append the version to OLD versions of the app. This is to ensure that there is only one application with the same name.
* Improved the initial configuration process for adding Patch My PC Software Updates to an environment. This involves attempting to restart the WCM component after an initial Patch My PC update is published. This expedites getting the Patch My PC category into ConfigMgr so it can be selected.
* The Publisher will send an alert if the catalog failed to download.
* The Publisher can now process FTP links for downloads.
* Updated to the latest Patch My PC logo.

### Fixes

* Fixed a bug where the Republish feature may cause multiple republish actions to occur if the customer performs the operation on multiple tabs.
* Fixed a bug where ‘disabling’ a tab with the checkbox at the top would cause the settings to be lost if the Publisher was closed.
* Fixed a bug where the alert webhooks may be duplicated during a setting import.
* Fixed a bug where some unsupported right-click options might be enabled by the auto-enable product’s rules.
* Fixed a bug where conflicting process notification timeout setting was not being read properly from settings.xml causing the setting to not apply.
* Fixed a bug where the /SyncNow switch for the Publisher would not work if an instance of the Publisher was already running.
* Fixed a bug where multiple assignments for the same group may attempt to be created in Intune.
* Fixed a bug where the Organization Name specified for the Manage Conflicting Process window would not be populated for ConfigMgr applications.
* Fixed a bug where the icon would not be set for a republished Intune application.
* Fixed a bug where the republish ConfigMgr application feature would not validate the hash of existing additional files which caused edited files to not be copied during a republish.
* Fixed a bug where republish ConfigMgr application would not set the expected OS requirements.
* Fixed a bug where ‘Override manual assignment changes’ is checked for an Intune product, and there is an ‘exclude’ assignment which would cause the Publisher to fail to process all assignments.

## 2.1.1 - 2021-11-02

### Features

* Allow customized [Managed Conflicting Process](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) popup notifications, including support for localization.
  * Idea: [PATCHMYPC-I-1296](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1296)
* Clicking a ‘localhost’ download URL in [show package info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo) will validate the local content.
  * Idea: [PATCHMYPC-I-1363](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1363)
* Option to “Republish” ConfigMgr and Intune Applications
  * Idea: [PATCHMYPC-I-1353](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1353)

### Improvements

* It is now possible to ‘Manage ESP assignments’ from within the [Intune Application Manager](https://patchmypc.com/intune-application-manager-utility).
* ConfigMgr database scan button is now available on the ConfigMgr apps tab as well as the Updates tab.
* ScriptRunner will always use Intune-based folders when executing from an Intune app installation.
* ScriptRunner will now monitor for child processes during the uninstall of software. This ensures that uninstalls which spawn child processes do not exit immediately and cause a detection error.
* Prevent using a ConfigMgr source path that could cause paths to exceed the 256 windows path limit.
* Fixed a bug where publishing would proceed even if a custom script failed to be processed.

### Fixes

* Fixed a bug where the Publisher would fail to parse a command line that had a parameter that occurred more than once. This would cause a content update every sync.
* Fixed a bug where Recreate Detection Script option for ConfigMgr would cause the wrong ‘Installation Behavior’ to be set for user-based apps.
* Fixed a bug where the Publisher and ScriptRunner would fail to parse a parameter with nested quotes and spaces.
* Fixed a bug where PreventStart UI would fail to be bypassed when a SYSTEM launched a conflicting process potentially leaving behind Image File Execution Option registry keys.
* Fixed a bug where retained applications may be updated unexpectedly when both postpone app and retain app are configured.
* Fixed a bug where the Publisher would run a sync every time ‘Apply Changes’ is clicked and the schedule is set to hourly.

## 2.1.0 - 2021-09-16

### Features

* Improve conflicting process timeout options
  * ConfigMgr and Intune timeout increased to their respective maximums, minus a 15-minute buffer.
    * ConfigMgr App Max: 705 minutes
    * Intune Max: 45 minutes
  * New option to use ‘maximum run time’ from the respective update or app.
    * ConfigMgr Update Max: Will use configured update ‘[max run time](https://docs.microsoft.com/en-us/mem/configmgr/sum/get-started/manage-settings-for-software-updates#BKMK_SetMaxRunTime)’ as configured in ConfigMgr for the update.
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

### Improvements

* Text boxes within the UI now implement an autocomplete for file paths and URLs.
* The [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) notification will now display ‘update’ based language for an Intune Update. For example, the button will say ‘Close and Update’ instead of ‘Close and Install.’

### Fixes

* Fixed a bug where the Publisher would throw an exception if a ConfigMgr scope is deleted, but still associated with a product in the Publisher.
* Fixed a bug where Intune email reports would not include the warning regarding missing local content for applications
* Fixed a bug where the ConfigMgr [source folder validation](https://patchmypc.com/smsprovider-connection-and-source-folder-options#Source-Folder-Validation) would perform a partial match, such as \\\server\source\_apps being considered a conflict for \\\server\source. We now append a trailing slash to the comparison.
* Fixed a bug where the ‘Prevent Start…’ option for [Manage Conflicting Process](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) would throw an access denied error instead of the desired message box.
* Fixed a bug where assignments would be copied from Intune app to Intune updates when the copy between tabs is used.
* Fixed a bug where custom return codes set in the catalog were not processed for updates by the Publisher.
* Fixed a bug where ConfigMgr applications would be revised every sync when the Manage Conflicting Process option is set to an option other than ‘Notify’

## 2.0.9 - 2021-08-09

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
* The Publisher will not delete the local content for a product if the publishing of the product failed.
* The Publisher will automatically revise an update if the applicability rules or description is updated in the catalog.
* The Publisher now supports log rollover of up to 10 log files. Previously we would only retain one rollover log. This is configurable in the General tab of the Publisher above the max log size.

### Fixes

* Fixed a bug where the Manage Conflicting Process window may not show the proper process name in the list of conflicting applications.
* Fixed a bug where the Publisher did not respect the ConfigMgr app retention settings when the delay in-place upgrade feature was also in use.
* Fixed a bug where Intune apps and updates would not use the temp content download directory specified in the advanced tab.
* Fixed a bug where the Publisher would revise ConfigMgr apps every sync in certain cultures (The known issue was with Russian, but could impact others).
* Fixed a bug where the alert webhook configured for Slack may revert to a Teams webhook causing malformed messages.
* Fixed a bug where the Manage Conflicting Process UI may continue to append text instead of having a countdown when it is set to ‘Do not allow user deferral…’
* Fixed a bug where pre/post uninstall scripts would only copy into the ConfigMgr source during a new application publisher. Scripts will now be copied into the source during the sync after the configuration change.
* Fixed a bug where the Intune Assignment UI would allow an invalid grace period/restart/snooze configuration.
* Fixed a bug where PatchMyPC-ScriptRunner would create an invalid command line for an MSI uninstall in some cases.
* Fixed a bug where the Manage Conflicting Process UI would fail to enumerate some properties of the blocked processes causing it to close the blocking process before the user can interact.

## 2.0.8 - 2021-07-12

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
* Manage Conflicting Process UI should now scale better vertically.

### Fixes

* Fix user validation of the input fields for pre/post script when the file does not exist.
* Fixed Intune detection script which was looking for a non-existent ‘dn’ property.
* Fixed Intune detection script so that it will parse invalid version parts that exceed a 32-bit signed integer.
* Fixed ConfigMgr detection script so that the RegKeyDetection work as expected for enhanced detection based on additional registry key values.
  * Script Version: 3.1
* Fixed a bug where double-clicking an item in the Intune App Manager would cause an ‘Index out of Range’ unhandled exception. This now opens the Manage Assignment wizard as expected.
* Fixed a bug where ConfigMgr applications with only user-based deployment types would have the checkbox set to allow installation during a task sequence, which is not allowed.
* Fixed a bug where the UI notification log file may not be created if the folder does not exist.
* Fixed a bug where user-based ConfigMgr applications may not have the Application Experience configuration properly configured.

## 2.0.7 - 2021-06-30

### Features

* Allow the [scheduling of the Modify Updates Wizard for Update Cleanup (unreferencedpackagefolders)](https://patchmypc.com/clean-up-third-party-updates-from-the-wsus-updateservicespackages-folder#AutoCleanUpdateServicesPackages)
  * Idea: [PATCHMYPC-I-797](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-797)
* Fill out ‘Disk Space Required’ for Intune apps.
  * Idea: [PATCHMYPC-I-1466](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1466)
* Intune app manager will filter by PMPC published apps by default, providing a drop-down to select non-PMPC or all apps.
  * Idea: [PATCHMYPC-I-1460](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1460)
* Within the ‘[Show Package Info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo)‘ window, you can now right-click on any cell to copy the cell data or the row data to your clipboard.
  * Idea: [PATCHMYPC-I-1468](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1468)

### Fixes

* Further improvements to CM log format for culture compatibility.

## 2.0.6 - 2021-06-16

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

### Fixes

* Fixed a bug where a ‘Security Error’ may occur when signing PowerShell scripts and a PowerShell Execution Policy is set via GPO.

## 2.0.5 - 2021-06-08

### Features

* Add option to update Intune assignments on sync.
  * New checkbox at the bottom of the Manage Assignments wizard to ‘Override manual assignment changes…’
  * Idea: [PATCHMYPC-I-1297](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1297)
* Add the title of the application or update to the Manage Assignments wizard.
  * Idea: [PATCHMYPC-I-1420](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1420)
* Notifications are presentation mode aware
  * Idea: [PATCHMYPC-I-1248](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1248)
* View and customize Conflicting Processes list
  * Idea: [PATCHMYPC-I-1382](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1382)
* The UI notification for Conflict Processes now lists all processes which are conflicting in a dropdown. This is to make it more clear what software will be closed.
* Send alerts to Slack
  * Idea: [PATCHMYPC-I-684](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-684)
  * Note: Slack notifications are a work in progress.
* Reverted a Scriptrunner change which flagged the exe to always run as Administrator. This is in preparation for supporting user-based applications in Intune and ConfigMgr.

### Improvements

* When a product is double-clicked in the [show package info](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo) tool the applicability rule will be shown.
* Improve the message which displays when an incorrect configuration is saved.
* Code changes in preparation for user-based applications.
* Publisher SMTP alerts for the creation of ConfigMgr apps, Intune apps, and Intune updates will all now show the CVE information. Previously only the WSUS updates would show this information.
* Added notes to the pre/post script window to help clarify the feature functionality.

### Fixes

* Fixed a bug where the Manage Conflicting Process window would not appear when a ConfigMgr application was deployed as required and the checkbox for ‘Allow user interaction…’ was not checked.
* Fixed a bug where Intune role scope tags would not be updated on sync for Intune Updates.
* Fixed a bug where the configured proxy may not be used for the Intune connection during publisher sync.
* Fixed a bug where software may be marked for revision during every sync of the Publisher. This would occur when PreventConflictingProcessRestart was in use and the KillProcess was set instead of Notify.
* Fixed a bug where the 'Exclude from Auto-Publishing' option for Intune apps and Intune updates may not work as expected causing excluding software to still be published if found.
* When a user or admin category was selected on a ConfigMgr application the Publisher would create a revision of the application every synchronization. Now a revision will only be created if a user or admin category needs to be added.
* Improved logging when checking access to timestamp.digicert.com if a proxy is defined

## 2.0.4 - 2021-04-26

### Improvements

* Adding a right-click context menu to the Intune App Manager allowing you to navigate to the MEM portal to view some application information.

### Fixes

* Fixed a bug where ConfigMgr applications would not populate in the Publisher if a scope was set at the All Vendors or the Vendor level.

## 2.0.3 - 2021-04-21

### Features

* Added the Usage Statistics group in the General tab that will show usage statistics
  * Idea: [PATCHMYPC-I-1343](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1343)
* Changed the license input to display only the 20 character license id and not the full license URL
* Define ConfigMgr scopes inside the Publisher service
  * Idea: [PATCHMYPC-I-962](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-962)
  * Note: This requires updated permissions. The ‘Import Role’ option in the Publisher will import the role with proper permissions or you can refer to this [article](https://patchmypc.com/permissions-required-in-sccm-for-base-installation-packages-from-patch-my-pc).

### Improvements

* The Intune and ConfigMgr scan wizard ‘Export’ buttons now prompt for whether the filter should be applied to the export.
* Improve how Timestamping is handled in some scenarios.
* Improved the speed of Intune application deletion by using batch calls to Microsoft Graph
* Options related to WSUS have been moved from the Advanced tab to the Options button in the Updates tab

### Fixes

* The classification field in the Intune Apps Manager is not populated for Updates
* Update revision doesn’t take account of republished updates
* Connections to Intune may not respect the proxy configuration set in the Publisher.
* ‘Show Package Details…’ right-click option would not load as expected.
* CVE Wizard would not load as expected.
* SSRS dashboards would report a negative % for compliance in some scenarios. The reports can be reinstalled if you are affected by following the same process as the initial install which will overwrite the reports.

## 2.0.2 - 2021-04-06

### Features

* ConfigMgr right-click option to set OS type requirement – client vs. server
  * Idea:[PATCHMYPC-I-1255](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1255)
* Intune Scoping Support
  * There is a [new right-click option](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#Manage-RoleScopeTags) for Intune applications and updates which lets you ‘Manage scope tags.’
  * Scope tags will be copied from the previous PMPC application or update to the new version during Publisher sync.
  * Requires new permission to be added to the Azure App Registration
    * DeviceManagementRBACRead.All
  * Idea:[PATCHMYPC-I-1029](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1029)
* Change description text and icon for Intune Win32 applications
  * Idea:[PATCHMYPC-I-1158](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1158)
* Retain N-X apps in ConfigMgr when set to ‘Create a new application…’ is enabled.
  * Idea:[PATCHMYPC-I-1266](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1266)
* Retain N-X apps in ConfigMgr when set to ‘Update existing application…’ is enabled.
  * Idea:[PATCHMYPC-I-1265](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1265)

### Improvements

* Scriptrunner will now automatically prompt for elevation when executed.
* Improve how settings are saved to prevent losing your Publisher configuration in some scenarios such as no disk space.
* The UI Notification feature for conflicting processes will now exit with an exit code 1602 if the installation is snoozed or a timeout occurs. Previously it was 1618 which could cause very frequent reevaluation.
* Wait to delete local content repository files until the end of the Publisher sync if the option to ‘Delete the update file in the local repository after publishing’ is selected.
  * In some cases, customers had the same binary needed for two different publish actions, and the second publish would fail because the binary had been deleted.
* In the DownloadHistory.csv file, we now include the purpose of the download and the port.
* The scan wizard found application count is now updated to reflect applications found with the specified filter.
* Scriptrunner will now clean up leftover ‘Image File Execution Options’ registry keys. This helps prevent unexpected blocking of application launch in the event scriptrunner crashes and leaves behind some of these keys. We have also update the [Manage Conflicting Processes docs](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications#UpdateInProgress) to provide additional information for this scenario.
* Updated the ConfigMgr detection script to cast the DisplayVersion to a string before trimming in the event a vendor has created DisplayVersion as a DWORD and not a REG\_SZ
  * Script Version: 2.9
* The ‘Purpose’ field will now be cleared in the Intune App Manager when all assignments are removed.

### Fixes

* Fixed a bug where we may fail to parse a package.xml file that contains special characters such as an ampersand.
* Fixed a bug where the DownloadUrl and MoreInfoUrl columns were not sortable in the ‘Show Package Info’ UI.
* Fixed a bug where the UI may crash if there is a large number of Azure AD Groups being retrieved and the UI is closed before the query completes.
* Fixed a bug where some right-click options such as Manage Categories, Manage ESP profiles and Manage Naming Convention may not propagate from the root, or vendor level to a newly enabled product.
* Fixed a bug where assignments may not be added to an existing Intune Win32 application during Publisher sync.
* Fixed a bug where the Publisher UI would crash if the ‘Modify Updates Wizard’ was launched on a computer that does not have the WSUS role.
* Fixed a bug where only the first 1000 Intune applications are returned which can cause Application lookup failures via Microsoft Graph.

## 2.0.1 - 2021-03-02

### Features

* Interactive user notifications that allow the user to be prompted to close conflicting software
  * Has a range of options for customizing the deferral options. See the [documentation](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) for more information.
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
* Use Scriptrunner to uninstall MSIs
  * Idea: [PATCHMYPC-I-1083](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1083)
* Use MainFile to uninstall software
  * Idea: [PATCHMYPC-I-991](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-991)
* Increase the max delay for the ConfigMgr delay application creation feature to 32 days.
  * Idea: [PATCHMYPC-I-914](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-914)

### Improvements

* Only one instance of the Publisher is allowed to run at a time. If a second user runs the Publisher they will receive an error message and the Publisher will close.
* Intune Application Manager button is now available in the Intune Apps and Intune Updates tab directly, as well as in the Intune Options.
* ConfigMgr detection scripts now validate the architecture and installation type of the software being detected.
  * This feature was in place for Intune scripts and has been integrated into the ConfigMgr scripts.
  * Script Version: 2.8

### Fixes

* Fixed a bug where adding file-based right-click option to a ConfigMgr application would not trigger a revision in some cases.
  * Examples: MST, Pre/Post Script, Additional files
* Fixed a bug where the Intune detection and requirement script might fail to work as expected if there are invalid registry properties on an object in the registry.
* Fixed a bug where the new Conflicting Process settings may not be saved for ConfigMgr applications.
* Fixed a bug where the company logo may not show in the Conflicting Process UI for Intune clients.
* Fixed a bug where the Conflicting Processes deferral count would allow more than the configured number of deferrals.

## 2.0.0 - 2021-01-29

This version of the publisher will be rolled out over the coming week. If you would like to upgrade now you can download the latest MSI [here](https://patchmypc.com/msi).

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
* Add an additional Right-Click option for x86 OS requirement for x86 application installers
  * Idea:[ PATCHMYPC-I-779](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-779)
* Sign PMPC provided pre/post scripts with local WSUS Code Signing certificate
  * Idea: [PATCHMYPC-I-959](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-959)
* ScriptRunner now deletes log files older than X days according to the setting in Advanced Tab.
  * Idea: [PATCHMYPC-I-1105](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1105)

### Improvements

* PatchMyPC-ScriptRunner has improved logic for UninstallPackage.
* Now factors in SystemComponent and QuietUninstallString when searching the registry.
* Intune Scan Wizard updated to match the ConfigMgr scan wizard.
* Can include zero-count applications in results and export.
* Filtering options updated.
* The ‘Exclude from auto-publish…’ option now exists for Intune Apps and Intune Updates.
* Scan Wizards will now automatically allow vertical scrolling if needed.
* Improved vertical scrollbar behavior for Scan Wizards
* Implement a retry when performing some ‘POST’ operations to Microsoft Graph to improve Intune Win32 app creation reliability.
* The warning message box that pops up if the Enrollment Status Page right-click option is invoked without proper Azure App Registration Permission now has a ‘Help’ button that links to the permission KB article.
* The pre and post script ‘browse’ buttons now will open to the location of the currently selected script if found.
* Update right-click option text to accurately reflect functionality.
* Exclude from being enabled during automated SCCM/Intune inventory scans
* Renamed to: Exclude from auto-publishing rules
* Add/Manage pre/post update installation scripts
* Renamed to: Add/Manage pre/post scripts
* Patch My PC defined pre/post update installation scripts
* Renamed to: Patch My PC defined pre/post scripts

### Fixes

*   Fixed a bug where the certificate option would be enabled while in

    ‘Intune Only’ mode.
* Fixed a bug where the Intune Graph token used by features such as Intune App Category selection would expire if the Publisher UI was open for a long time.
* Fixed a bug where unnecessary calls were made to renew the Graph API token when performing Graph Batch queries.
* Fixed a bug where the ConfigMgr ‘Recreate Detection’ option would not set the MSI product code for the newly generated script.
* Fixed a bug where the ConfigMgr ‘Recreate Detection’ option would not set the VersionInclude for the newly generated script.
* Fixed a bug where an Enrollment Status Page may have a mobileAppId listed twice when making the Graph PATCH API call. This would cause a 400 status code, and cause the API call to fail.
* Fixed a bug where the Intune Scan or ConfigMgr Scan would happen if the respective ‘Auto-Enable’ option was enabled, but the feature itself, such as Intune Updates, was disabled.
* Fixed a bug where the Teams notifications for auto-enable would not contain details regarding the software.
* Fixed a bug where the auto-enable feature of Intune Scanning may cause duplicate Win32 apps to be published within Intune.
* Fixed a bug where conflicting right-click options could be selected in the scan wizards.
* Fixed a bug with the new Log Retention feature of Script Runner where it may unnecessarily trigger an ‘Update Content’ on ConfigMgr applications.

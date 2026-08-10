# Publisher 1.x Releases

_Applies to: Patch My PC Publisher V1.x_

Details the production release history for Patch My PC (PMPC) Publisher, for version 1.0.0 - 1.9.9.

### 1.9.9 - 2020-12-18

#### Features

* [Customizable Naming Convention](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#IntuneNamingConvention) for Intune Applications
  * Idea: [PATCHMYPC-I-961](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-961)

#### Improvements

* Improved the updating of supported products metadata during Publisher synchronization.

#### Fixes

* Adjust certificate signing validation for Patch My PC signed files.
* Fixed an issue where [Recreate Detection](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#RecreateDetection) for MSI-based applications would not populate some variables in the script.

### 1.9.8 - 2020-12-14

#### Features

* Manage categories for Configuration Manager applications
  * User Categories: Viewable to users in Software Center
  * Admin Categories: Viewable to administrators in the Configuration Manager Console
  * Idea: [PATCHMYPC-I-780](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-780)
* ScriptRunner now has a new custom variable, %CurrentDir%
  * This variable may need to be put in double-quotes or the entire parameter may need to be in double quotes depending on the application. Examples of this are below.
    * Config=”%CurrentDir%\Config.ini”
    * “Config=%CurrentDir%\Config.ini”
  * Idea: [PATCHMYPC-I-985](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-985)

#### Improvements

* During a Publisher sync, the Settings.xml will be automatically updated according to SupportProducts. This improves the experiences when Patch My PC makes metadata changes that impact some of the application configurations such as detection.
* The Intune Application Manager now has a button for ‘Manage Assignments’
* Improve how ScriptRunner handles version parts that exceed the 32 bit signed integer max.
* Improve [CVE Import Wizard](https://patchmypc.com/how-the-cve-import-wizard-works-for-matching-cve-ids) CVE-ID matching
* Improve logging associated with delayed application publishing
* The[ SSRS report dashboards](https://patchmypc.com/free-software-update-compliance-dashboard-reports-for-microsoft-sccm) now include a parameter for Deployed.

### 1.9.7 - 2020-11-24

#### Features

* Manage Intune categories for created and updated Intune applications and updates.
  * Note: Currently, existing applications/updates in Intune will not have their categories removed but new categories will be added for existing Win32 applications.
  * Idea: [PATCHMYPC-I965](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-965)
* Clicking a ‘digest’ in the Modify Published Updates Wizard, or the Package Details wizard will now open the respective VirusTotal page.

#### Improvements

* Sorting by ‘Selected’ in Modify Published Updates Wizard now sorts by the checked state.
* The Configuration Manager detection script now handles invalid version parts better. Some vendors use DateTime stamps in their version. This can end up being a value larger than a 32-bit integer causing the version cast to fail.

#### Fixes

* Fixed an issue where copied Intune Assignments for newly published Intune software would not have their custom available time, and deadline time adjusted relative to the new publish date.
* Fixed an issue where Intune Assignments would be created without a deadline or available time if the ‘copy assignment’ option was not configured.
* Fixed an issue where the maximum value for restart notification would not allow a value greater than 201.
* Fixed a bug where the console version check for UninstallContent setting was incorrect.
* Improved catalog parsing when there are a large number of CPU cores on the machine running the publisher.

### 1.9.6 - 2020-11-12

#### Features

* New feature that allows [viewing, and exporting package details](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#PackageInfo).
  * Idea: [PATCHMYPC-I-1037](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-1037)
  * The below information can be viewed for the currently synchronized catalog.
    * Title (Including version)
    * File Name
    * Command-line
    * Download URL
    * Digest

#### Improvements

* Improved the speed at which the catalog is processed. This will improve the loading speed of the CVE Import Wizard, the new Package Details Feature, and the Modify Updates Wizard.
* Improved the speed at which the catalog is extracted for the CVE Import Wizard.
* Win32 Intune applications will no longer be created as featured by default.
  * Existing Intune applications will not have their ‘featured’ state changed. The Publisher will retain the currently configured ‘featured’ setting for any given application.

### 1.9.5 - 2020-11-06

#### Fixes

* Fixed a bug where new Intune assignments may not be created.

### 1.9.4 - 2020-11-05

#### Features

* The first release of our CVE import/matching features based on UserVoice [**Feature Request for CVE Import automation**](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-916)
  * You can launch the CVE import feature in the Updates tab by clicking the new document lock icon
  * If you have any feedback on the first release, leave a comment at [https://ideas.patchmypc.com/ideas/PATCHMYPC-I-916](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-916)
* Updates published via the CVE Import Wizard will have a Teams and Email alert if enabled.
* Scan Configuration Manager Database wizard updated.
  * Supports Filtering
  * Can optionally show, and export, applications whose count is zero.
    * Idea: [PATCHMYPC-I-828](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-828)
  * General UI improvements such as tooltips, alt-shortcuts, empty field validation.

#### Improvements

* Certificate selection for Intune code signing will now additionally search the WSUS store if it is found.
* The Product Name has been added to the PatchMyPC-DownloadHistory.csv generated in the installation directory of the publisher.
* Improved the method used to gather PackageID from newly published Applications.

#### Fixes

* Fixed a bug where an application may fail to publish on versions of Configuration Manager older than 1706.
* Fixed a bug where the publisher would fail to find applications published to a folder containing square brackets
  * For Example: \\\server\sources\\\[PMPC]Applications
* Fixed a bug where the TLS port for SMTP alerts may show as 587 in the UI, even when a custom port is set. The port in the UI will now accurately reflect the saved settings.
* Fixed an issue where Intune assignments may not set the correct delayed deadline
* Fixed an issue where older versions of the ConfigMgr console may receive error: Method not found: ‘Void Microsoft.ConfigurationManagement.ApplicationManagement.MsiInstaller.set\_UninstallSetting(Microsoft.ConfigurationManagement.ApplicationManagement.UninstallContentSetting)’.

### 1.9.3 - 2020-10-19

#### Features

* Application update in-place vs. create new application configurable at the individual product level.
  * Idea: [PATCHMYPC-I-209](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-209)
* Support for user-based installations for Configuration Manager applications, as well as Intune Applications and Intune Updates.
  * Idea: [PATCHMYPC-I-801](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-801)
  * Note: We still need to add user-based software to the catalog, but the publisher now has support for this so that we can begin adding some user-based software.
* Option to not append the republished date tag to republished updates.
  * Idea: [PATCHMYPC-I-876](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-876)
  * This is now a configurable checkbox in the advanced tab.
* Intune Scan Wizard now has the option to[ automatically enable Intune Updates based on scan data](https://patchmypc.com/scan-intune-for-supported-products#CurrentFeatures).
* Update the PatchMyPC-ScriptRunner.exe to use the CCM client log directory defined in the registry by default
  *   Check

      “HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\CCM\Logging\\@Global”

      \> LogDirectory, and fallback to “%windir%\ccm\logs”
  * Idea: [PATCHMYPC-I-911](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-911)

#### Improvements

* Log out the in-progress count of updates and applications as they are processed.
  * Previously the in-progress count was only logged if the log level was set to debug. It is now logged with informational level logging.
* Improve the PatchMyPC-ScriptRunner.exe to have better logic when searching the registry for uninstall strings
* The PatchMyPC-ScriptRunner.exe will retry MSI based operations if a 1618 exit code is returned by the installer. The result is a reduction in failed installs due to Windows Installer being unavailable.
  * Maximum three retries, with 1 minute in between.
* Updated the PowerShell script for Intune applications and updates to improve compatibility with constrained language mode.
* Optimized icon resizing for ConfigMgr applications.
* MSI based ConfigMgr applications will now have 'No uninstall content' set for the uninstaller, as we directly call msiexec, no content is needed.

#### Fixes

* Configuration Manager application detection script fixed to supported PowerShell 2.0.
* Fixed an issue where republishing a WSUS update would also cause the equivalent Intune Update to republish as well.

### 1.9.2 - 2020-09-25

#### Improvements

* Publisher code changes to better support our [Proactive Customer Care](https://patchmypc.com/proactive-customer-care) program

#### Fixes

* Fixed an issue where the [Intune Application Manager Utility](https://patchmypc.com/intune-application-creation-options#topic5) would throw a terminating error if Intune applications were found with an empty ‘Notes’ field.

### 1.9.1 - 2020-09-21

#### Features

* Added an option to disable WSUS publishing using a checkbox at the top of the 'Updates' tab. This allows the Update publishing feature to be disabled while still retaining all products and settings. This can be helpful if you need to sync only Applications, Intune Applications, or Intune Updates, but don't want to lose your selected Updates and configurations.
* Added a right-click option to open the help page that details the right-click options.
* During synchronization, the Publisher will check if the WSUS code signing certificate is expired or near expiration and add a message in the email report.
* During synchronization, the Publisher will check if the WSUS code signing certificate is in the required Windows Cert stores and add it if needed.
* SMTP port automatically set to 587 when 'Use TLS' is selected, and to 25 when 'Use TLS' is unselected. The port can still be manually edited to account for any port, but the common port for the protocol is set by default.

#### Improvements

* Add additional known errors in the log, providing a link to a KB article that may assist with solving the known error.
* Display additional info in the Certificate information wizard on whether the certificate is found in the expected Windows Cert stores.
* SMTP port default to 25 instead of 587 when the feature is in a non-configured state.
*   The Publisher will retry several times when the rename of a folder during an SCCM application upgrade fails. This should help prevent

    'Access Denied' errors that are caused by file locks.

#### Fixes

* Fixed an issue where, sometimes, the SupportedProducts.xml file cannot be read during a synchronization.
* Fixed an issue where a machine with a large number of CPU cores may experience high CPU load when running the Intune Scan Wizard.

### 1.9.0 - 2020-09-11

#### Fixes

* Fixed a bug where if the [application delay option](https://patchmypc.com/application-creation-options#topic6) is enabled and an update contains spaces in the file name such as Firefox, it may download with an incorrect file name.
  * This would cause the following error in appenforce.log:
    *   \*\*fails to install error code Looking for exit code

        -2147467259 in exit codes table\*\*
    * **Unmatched exit code (2147500037) is considered an execution failure.**
      *

### 1.8.9 - 2020-09-10

#### Features

* The Publisher now has a '**Recreate Detection Script'** right-click option. When this is selected, the specified products will have their Detection Scripts recreated during the next Publisher synchronization.
  * Idea: [PATCHMYPC-I-855](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-855)
* The Modify Updates Wizard now has a checkbox to 'Show Only Updates for Not Enabled Products'
  * This is helpful in identifying updates you may want to decline for products you no longer publish updates for

#### Improvements

* Intune Application and Update detection script now has improved version string parsing
* Intune Application and Update detection script will only parse DisplayName for a version if the DisplayVersion is empty
* SCCM Application detection script will only parse DisplayName for a version if the DisplayVersion is empty
* VLC is now split into an EXE and an MSI
  * The existing selection of VLC will be converted to the EXE version of the application. The MSI can now also be selected and published.
* Pre/Post Script form now validates that Pre-Update Script and Post-Update Script exists before allowing you to press OK.

#### Fixes

* Fixed an issue where the Publisher was unable to get the list of published Intune applications.
* Fixed an issue where a republished WSUS update may be republished multiple times if the Publisher was left open during synchronization and settings were changed after the initial republish completes.
* Fixed a bug where certain detection scripts generated for Intune Applications and Intune Updates would not detect as expected.

### 1.8.8 - 2020-08-28

#### Improvements

* Improved the copying of right-click options from the Updates tab, to the ConfigMgr Apps tab, or the Intune Apps tab.

#### Fixes

* Fixed an issue where the Publisher would falsely report that it was not installed on a Software Update Point in some scenarios.
* Fixed an issue where the Intune Updates product list was not reloaded during publisher sync in some scenarios.
* Fixed an issue where Intune Applications would not detect appropriately for certain applications. OneDrive was a known affected product, but others may have been included.
* Fixed an issue where the Intune Connection Options would log out an error state 'Invalid Uri.'
*   Fixed an issue where ConfigMgr Base Applications were created with a detection script that did not specify a version to search for. All base applications created with \*\*Publisher Version 1.8.4 or newer

    (released 2020-07-22)\*\* would always show as detected if any version was installed on the endpoint. The version was not being validated.

    * The affected detection method would show version 2.2 in the logs, and in the script itself.
    * Applications created after 2020-07-22 by the Publisher should be deleted and recreated to ensure the proper detection method script is used.

### 1.8.7 - 2020-08-21

#### Fixes

* Fixed a bug where the publisher would report ‘Cannot get available disk space’ when validating there is enough free disk space for deferred application publishing.
* Fixed a bug where the publisher would fail to parse the Proxy URL, reporting the following error.
  * An error occurred while converting the provided Proxy URL to a URI for use by the Web Client…
  * See [this KB article](https://patchmypc.com/error-converting-proxy-url-to-uri) for remediation steps if you are affected.

### 1.8.6 - 2020-08-20

#### Features

* You can now [automatically create the security role](https://patchmypc.com/permissions-required-in-sccm-for-base-installation-packages-from-patch-my-pc) for allowing the publishing to create Configuration Manager applications.

#### Improvements

* Within the ‘Manage Assignments’ page for Intune Applications and Updates the cells now have a clickable link to open up the form for managing available dates, deadlines, and restart behavior. Previously this link was only on the application name.

#### Fixes

* Fixed an issue where SMTP settings were not properly translated when the new Anonymous authentication option was added.
* Fixed an issue where right-click settings from the “All Products” level may not be applied when copied to another tab.

### 1.8.5 - 2020-08-17

#### Features

* Support for Intune Updates
  * [https://patchmypc.com/third-party-patch-management-for-microsoft-intune-now-available](https://patchmypc.com/third-party-patch-management-for-microsoft-intune-now-available)
* Add Anonymous authentication method to send emails.
  * User voice [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-817)
* Intune updates use the description in the SDP for the title.
  * User voice [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-915)
* Split the «Delete Intune Application when a new release is published» option to allow to choose the behavior for Apps and Updates independently.
  * User voice [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-913)

#### Improvements

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

#### Fixes

* Fixed an issue where custom options are not correctly copied between two tabs when copying enabled products from one tab to another.
* Fixed an issue where reserved characters were not working as expected when searching for Azure AD Groups
* Fixed an issue where the Publisher may display a warning that the certificate is incorrect or missing when it's within 30 days of the expiration date.

### 1.8.4 - 2020-07-22

#### ​ Fixes

* Changed how Unreferenced Package Folders are found. If third party updates are set to display in WSUS, then they might show up as 'Unreferenced' by the WSUS content cleanup tool. The publisher now correctly display the list of unreferenced contents.
* Available date and deadline date for Intune assignments are not properly displayed in the assignment setting wizard
*   The Publisher may crash when trying to check for a new release on Intune only installation where only RSAT:Windows Service Update Services is being used. If you are affected by this issue, please perform an in-place upgrade of the publisher using

    [**version 1.8.4 available for download now**](https://app.gitbook.com/publishing-service-setup-documentation).

### 1.8.3 - 2020-07-08

#### Features

* Add an Intune Scan Wizard allowing you to auto-enroll applications based on Intune App scanning.
  * [https://patchmypc.com/scan-intune-for-supported-products](https://patchmypc.com/scan-intune-for-supported-products)
* Add all options available in the 'User Experience' for Applications to a new context menu option for base installs.
  * [https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#app-user-experience](https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications#app-user-experience)
  * User voice [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-803)

#### Improvements

* Add more logging to the application update and creation processes to assist with troubleshooting.
* Code optimization and cleanup for applications.
* Detection script now accounts for user-based installs when needed.
* Detection script checks if running as SYSTEM using the SID instead of the username.
* Add a new known error to assist with identifying and resolving TooManyCategories for WSUS.
* Enabled CTRL+F functionality in the Intune tab.
* Product download will fallback to the Internet in case of a digest mismatch in the local content repository.
  * User voice [idea](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-802)
* Display third party vendor/product count in the Update Modification Wizard.
* Deprecate WSUS v3
* We now use a FIPS compliant algorithm when creating Intune applications

#### Fixes

* Fixed a bug where the Publisher service would never timeout during content downloads in some scenarios, causing the service to hang.
* See the [HTTP Download Timeout section](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service#HTTP-Timeout) for more information regarding the timeout. The default value is a 15-minute download timeout.
* Fixed a bug where some system cultures would result in incorrect command-line parsing.
* Fixed a bug where an application's content would not be updated when a right-click option was selected in some scenarios.
* Fixed a bug where the 'exclude from autoenrollment' option was unable to be changed on a product when the setting was configured at the vendor level.
* Fixed a bug where the publishing service could not publish a postponed application if it contained an HTML escaped character.
* Fixed a bug where the Intune Scan Wizard was overwriting the Intune Authentication URL
* Fixed an issue where the checkbox in the MSI installer to enable Intune only mode may not be applied after the installation
*   Fixed an issue where the republish option no longer showed for

    "All Products" and Vendor nodes
* Fixed an issue where incorrect workstation counts were shown on certain SSRS reports

### 1.8.2 - 2020-06-09

#### Fixes

* Fixed an issue where the admin comment field of a dependent application would be updated to say the application was created by Patch My PC
* Fixed an issue where the republish updates right-click menu may exist in the ConfigMgr Apps and Intune Apps tab

### 1.8.1 - 2020-06-03

#### Fixes

* Settings tool can crash when copying enabled products from the WSUS tab to another tab if the «All Products» node is not displayed
* Teams notifications are malformed if they contain a file path.

### 1.8.0 - 2020-06-01

#### Features

* Add button to restart the service
* Added support for Server 2019 in the [SSRS dashboards](https://app.gitbook.com/free-software-update-compliance-dashboard-reports-for-microsoft-sccm)
* Cache binary for postponed updates allows postponed updates to be published after the download link has changed.
* [Custom right-click options](https://app.gitbook.com/custom-options-available-for-third-party-updates-and-applications) applied at the All Products level are now retained when the UI is closed, and future products are enabled. UserVoice Idea: [Retain the Logging Options in View when Saved at the All Products Level](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-742)
*   SCCM Database Scan now has an option to ["Auto-enable products as 'Metadata Only' if found, but threshold is not met"](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-565)

    **Fixes**
* Fixed bug where some SSRS report links did not function as expected
*   Fixed an issue where a customer with an expired Intune only license could get stuck in a message box loop.

    **Improvements**
* Enhances the display in the Update modification wizard when there is a lot of updates.
* Sort SCCM folders when choosing a folder to move new newly created applications to. UserVoice Idea: [Fix sorting in Console Folder Browser](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-818)

### 1.7.9 - 2020-05-19

#### Feature

* Allows creating a self-signed certificate with the private key marked as non-exportable.
* Added new subscription state reporting using Teams or SMTP emails

### 1.7.8 - 2020-05-14

#### Feature

*   Added 'Like,' 'Dislike', and 'Feedback' button in the title bar of the settings tool.

    **Fixes**
* List unreferenced package folders did not list any folders in some WSUS configurations
* Added a workaround to handle SCCM apps published with an unsupported language
*   Resolved incorrect summarization within the SCCM Scan Database tool

    **Improvements**
* Web domains of downloaded icons are listed in the DownloadHistory.csv file.
* Added several help links in the UI.
*   Improved logging for known errors linking to KB articles

    **Changes**
* The option to fallback to ConfigMgr package publishing when an application can't be published as an SCCM application has been removed in the UI due to not being needed.
* SQL query default timeout is now 90 seconds from 30 seconds.
* Removed from the UI the option to generate a CSV file with publishing info. The option is always enabled, and the file path can be configured with the registry setting : HKEY\_LOCAL\_MACHINE\SOFTWARE\Patch My PC Publishing Service:PublishingHistoryCSVFolder

### 1.7.7 - 2020-04-28

#### Feature

*   Intune assignments created during an application creation or update are now reported in Teams notifications and email alerts

    (Idea:

    [PATCHMYPC-I-700](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-700))
*   Adds a line in the log to specify Intune AppIDs (old and new release) during an application updating (Idea:

    [PATCHMYPC-I-723](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-723))
*   Improves how Azure AD groups are retrieved (Set page limit to 999). We will also now display O365 groups. Adds the ability to search a group based on the group name starts with (Idea:

    [PATCHMYPC-I-718](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-718))
*   Adds a new column, UpdateEnabled, to the resulting CSV from the SCCM Scan Database Wizard -

    (Idea: [PATCHMYPC-I-645](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-645))
* UI improvements to the Base Install options
*   Generates a CSV file (PatchMyPC-DownloadHistory.csv) that includes the vendor name, protocol, web domains, and download status for downloaded binaries. (Idea:

    [PATCHMYPC-I-740](https://patchmypc.aha.io/ideas/PATCHMYPC-I-740))

    **Fixes**
* Fixed an issue where the WSUS Maintenance for unreferenced updates would not return folders when the name is longer than 80 characters
* Fixed an issue where file coping during publishing would fail when a file is referenced more than once (e.g., in additional files and pre-command script)
* Fixed an issue where adding multiple Intune assignments with customer deployment deadlines may cause the publisher UI to crash
*   Fixed an issue where double quotes in the command line argument for software updates would not be retained.

    **Improvements**
* Adds logging for a new known error when access is denied to the application source.
* Improved documentation for different areas of the Publisher UI.

### 1.7.6 - 2020-04-17

#### Fixes

* An error message is logged out if a device collection attribute is not configured in the SCCM application scan feature
*   Intune assignments referring to another a customer Azure AD group may be lost from the settings. Previous Intune assignments could be restored by importing a settings backup from the

    \\\backup folder in the advanced tab.
* Mistakenly notify a success when a hash validation failed during an SCCM application in-place upgrade

### 1.7.5 - 2020-04-15

#### Feature

* Added the ability to edit assignments for already published Intune applications using the Intune application manager
* Added a column in the Update Modification Wizard to show supersedence based on [**UserVoice 710**](https://patchmypc.aha.io/ideas/ideas/PATCHMYPC-I-710)
* Added a right-click option to open Local Content Repository
*   You can now limit the SCCM application database scan to a specific collection based on [**UserVoice 475**](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-475)

    **Improvements**
* When a TRANSFORMS command is added in the additional arguments, we will automatically add the full relative path at execution based on [**UserVoice 668**](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-668)
* Install times are now expressed as time offset starting from the publishing date when an application is published for the first time
* When an Intune application is updated, if assignments are not copied from a previous version, new assignment(s) are created based on the right-click assignment options
* Displays a warning message if the Local Content repository path is empty, and the option to look into this directory first is enabled
* We made significant performance improvements for our SCCM database scanning for application detection

### 1.7.4 - 2020-03-27

#### Fixes

* Fixed an issue introduced in build 1.7.3 where assignments for Microsoft Intune applications created directly within Microsoft Intune may be removed if they are not assigned within the Patch My PC Publisher.

### 1.7.3 - 2020-03-26

#### Features

*   We will now create assignments in Intune even if the Intune application was already created before adding the assignment

    **Fixes**
* Snooze duration in Intune assignments can be set to an invalid value when the restart grace period and restart countdown are also enabled
*   SCCM Applications may fail to be created on older SCCM builds with error "An error occurred while creating an application in SCCM: Could not load type

    'Microsoft.ConfigurationManagement.ApplicationManagement.ProcessDisplayName' from assembly

    'Microsoft.ConfigurationManagement.ApplicationManagement, Version=5.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'."
*   Microsoft Intune application may fail to be created with error

    "An error occurred while processing an Intune application: Unrecognized Guid format."
* Log the ApplicationID of the Intune app that is updated instead of the Intune App ID (reported by Jan Ketil Skanke)

### 1.7.2 - 2020-03-23

#### Improvements

*   Retain Deployment type dependencies during application in-place update

    **Changes**
* Changed the behavior of the Scan SCCM Database wizard, add an Ok button, and rename the Close button to Cancel.
*   Remove «Full Content» mention on Intune and SCCM TreeViews

    **Fixes**
* We would always log 0 requirements carried from the previous version even if more than 0 requirements have been carried over
* PowerShell detection method script wouldn't be signed if the filename contained a single quote
* Intune assignments are not always carried during an upgrade
  * **Advanced**
* Added a new [advanced option](https://app.gitbook.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service) enable via a registry value
  * Add the ability to parse the catalog using a sequential method instead of parallel (UseSequentialMethod = 1)

### 1.7.1 - 2020-03-09

#### Fixes

* Fix an issue where if there's a WIn32 application larger than 1.95gb, you would receive the following error:
  *   An error occurred while connecting to Intune: JSON integer 2242219440 is too large or small for an Int32. Path

      'value\[75].size', line 1, position 118932.

### 1.7.0 - 2020-03-08

#### Features

* Microsoft Intune production release.

### 1.6.9 - 2020-03-07

#### Features

* This update contains backend changes to prepare for production support for Microsoft Intune in an upcoming release.

### 1.6.8 - 2020-03-06

#### Fixes

* Fixed an issue where the code-signing certificate may not save correctly in the Microsoft Intune options.

### 1.6.7 - 2020-03-05

#### Improvements

* Improved the Microsoft Intune options. The options are now available in the Intune Apps tab and not the Advanced tab.
*   Improved the installation options for enabling Microsoft Intune only publishing.

    **Features**
* Display application dependencies in the SCCM application manager.

### 1.6.6 - 2020-03-02

#### Improvements

* Enhancements to prepare for Microsoft Intune support

### 1.6.5 - 2020-02-21

#### Improvements

* Adds a new application management tool for SCCM in the application options menu. You can now bulk delete applications created from Patch My PC or bulk delete deployments for applications
* Changed title format for republished updates to be more granular
* Included updated DLLs for Compression.cab from Wix
* When an update is republished, all previous republished updates can be superseded by the new update that is republished
* Add email, teams, and logging notifications when an update cannot be revised
* Added a more details button in the modify published update wizard that will show important details about updates published to WSUS
*   Improved success and failed icons for Microsoft Teams alerts

    **Fixes**
* Fixed an issue where the right-click option for manage logging may display the correct information

### 1.6.4 - 2020-02-14

#### Fixes

* Fixed an issue where updating MSI based applications may result in an error: An error occurred while updating a package in SCCM: Access to the path \ is denied.

### 1.6.3 - 2020-02-13

#### Features

*   Added the Intune bulk editor in the Advanced tab

    **Fixes**
* Fixed an issue where custom files and folders defined, may not be included in a software update cab file

### 1.6.2 - 2020-02-07

#### Features

* Added a new right-click option in the Applications tab to display an application as featured in company portal.

### 1.6.1 - 2020-02-06

#### Fixes

* Fixed an issue where you may receive an error: _An error occurred while signing the PowerShell detection script, but there is no error message to display._

### 1.6.0 - 2020-02-06

#### Features

* Applications will no longer be duplicated in the event the deployment type's source folder was deleted.
* You can now trigger a full and delta software update point synchronization from the advanced tab
  * **Microsoft Intune (Release Candidate)**\\
* You can now automate Win32 application management in Microsoft Intune
* You can now create assignments for Win32 applications in Microsoft Intune
* The authority URL for Microsoft Intune will be prepopulated
* You can now select a custom code-signing certificate from the computer's personal certificate store. A full WSUS installation is no longer required for code-signing the detection method script used for Intune.
*   The publishing service can now be installed on Windows 10 (x64) for a Microsoft Intune only setup.

    **Improvements**
* Use env variables instead of hard-coded path in PowerShell detection script.
* No longer perform WSUS service checks when the WSUS publishing is disabled for Intune only scenarios.
* You can now test the SMS Provider connection under SYSTEM-level context
*   Other fixes and improvements.

    **Fixes**
* Bug fixes and other improvements
*   Fixed an issue where you may receive an error: An error occurred while updating a package in SCCM: OpenDatabase,DatabasePath,OpenMode

    **Changes**
* Rename Intune preview to Intune Release Candidate.

### 1.5.9 - 2019-11-29

#### Features

* You can now trigger a full and delta software update point synchronization from the advanced tab
* You can now set a custom folder for temporary downloads of the software update and application content
* You can now set a custom folder for the log save location
* You can now browse to UNC paths when adding a custom folder in scripts dialog
*   You can now change the folder location for the generated CSV file

    **Improvements**
* You can now test the SMS Provider connection under SYSTEM-level context

### 1.5.8 - 2019-11-23

#### Fixed

* Fixed an issue in version 1.5.7 where youo may receive the following error when an application is updated in-place
  * An error occurred while updating a package in SCCM: Invalid property: object Application(ScopeId\_\*) property DisplayInfo.DisplayInfo.DefaultLanguage: Language En does not match any data in the set

### 1.5.7 - 2019-11-22

#### Features

* You can now right-click an individual product in the application tab and choose to move it to a custom folder in the console
* You can now create new folders in the applications node of the console directly from the folder browse dialog
*   You can now refresh folders in the applications node directly from the folder browse dialog

    **Improvements**
* Files downloaded for publishing updates are now cached and reused for applications within the same sync cycle
* Support to publish applications in other languages than en-US

### 1.5.6 - 2019-11-19

#### Features

*   You can now send Microsoft Teams publishing alerts using a webhook

    **Improvements**
* The software update point synchronization will be triggered after the update synchronization task rather than waiting for the updates and applications sync.
*   Improved the accuracy of the SCCM application scan feature to better differentiate between x86 and x64 products based on UserVoice [Improve accuracy of 32/64-bit count results of SCCM Database scan](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-461)

    **Fixes**
* Minor bugs fixes

### 1.5.5 - 2019-10-25

#### Feature

* Add support to auto-popular the uninstall command line for 50+ applications in SCCM
*   Allow searching backward for products and vendors when clicking

    (Shift+F3)
* Preserve User Categories when updating Apps in SCCM
* Preserve Admin Categories when updating an SCCM application
* You can now configure a custom application name, localized application name, localized application description, and icon
* You can now increase the [HTTP download timeout](https://app.gitbook.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service)
* You can now enable your software update point to sync when updates are published when your software update point is on a remote site system.
* You can now exclude products at the vendor level from being enabled in automatic scanning
* You can now press F4/Shift+F4 keys to go to the next/previous when searching products or vendors
* When disabling updates, we will now create a RegKey is it doesn't exist to disable self-updates

#### Changes

*   Set default download timeout to 100 seconds from 30 seconds.

    **Fixes**
* Fixed an issue where a custom command line may not be processed if it contained double quotes and a space
* Fixed an issue where the UI may crash when enabling a large number of products

#### Improvements

* Improved logging for varias actions including download percentages
* Improved logging
* Remove leading and trailing spaces in catalog URL, sms provider server name, application source folder path, and timestamp server URL

### 1.5.4 - 2019-10-09

#### Features

* Create a CSV file at the end of each synchronization with a summary of what was published, revised, created
* You can now set the max log size between 1-10 MB
* Added an option to show and delete unreferenced WSUS folders in the UpdateServicesPackages folder
* Added an option to show/hide already enabled products in the SCCM scan
* Added the ability to start a sync by running the PatchMyPC-Settings.exe with argument /SyncNow (the UI is not displayed)
*   Log events in the Windows event log (Starting/ending sync, success/fail publishing updates)

    **Improvements**
*   Add several log entries when sync fails

    ([EventID=3001-3005](https://patchmypc.com/windows-event-logging-details-for-patch-my-pc-publishing-service))
* Add new[ advanced options to improve SQL queries](https://patchmypc.com/advanced-configurations-available-using-the-registry-for-patch-my-pcs-publishing-service) for large organizations.
*   Improve the version comparison in the PowerShell detection method script

    **Fixes**
* Distribution point groups containing apostrophe were ignored during distribution
* Improved the PowerShell detection method scripts to handle invalid DWORD entries better fixing a "Specified cast is not valid." error message
* Various bug fixes

### 1.5.3 - 2019-09-20

#### Features

* Added the ability to delay updating applications in-place between 1-14 days after release.
* Display the count of updates and selected updates in the update modification wizard
* You can choose a custom folder in the applications node of the console to move applications to upon creation or updating automatically.
* You can now include custom folders for updates and applications.
* You can now specify the subject name when creating a self-signed certificate.
*   You can now Import/Export settings from the advanced tab.

    **Improvements**
*   PatchMyPC-ScriptRunner.exe files are updated when SCCM applications are upgraded.

    **Fixes**
* Fixed an issue where application detection method scripts may fail on devices with PowerShell version 2. The following output error would be logged to appdiscovery.log
  * Unexpected token '.0' in expression or statement.
  *
    * CategoryInfo : ParserError: (.0:String) \[], ParseException
  *
    * FullyQualifiedErrorId : UnexpectedToken
  * CScriptHandler::DiscoverApp failed (0x87d00327).
  * Deployment type detection failed with error 0x87d00327.

### 1.5.2 - 2019-09-07

#### Features

*   You can now configure any custom pre-update script to run before checking any processes to close or skip

    **Improvements**
* Improved logging
* If SMTP emails are enabled, we will now include any newly enabled products from the automated SCCM inventory scans.
* If there are pending settings changes unsaved, you will be prompted if you want to save the settings when performing a synchronization.
* You can now view applicability rules from the modify published updates wizard.

### 1.5.1 - 2019-09-02

#### Features

* You can now automatically enable products to be enabled based on them being detected in the SCCM database.
* Added options to Kill or Skip installations when auto-enrolling new products.
* Application names are now clickable for applications published, and links to the vendors release notes.
*   Added right-click option for products to be excluded from being automatically enabled during automated SCCM inventory scans.

    **Fixes**
* Fixed an issue where applications may fail to install on Windows 10 when using Latvia language.
* Fixed an issue where you may get an email about the license being expired when in trial-mode.

### 1.5.0 - 2019-08-13

#### Improvements

* New right-click option for applications to Add the Executable Names(s) in the Deployment Type's Install Behavior
* New right-click option for applications to Set the max and estimated run times

### 1.4.9 - 2019-08-08

#### Improvements

* Logging improvements
*   Any application created by Patch My PC will now contain and administrative comment of "Created by Patch My PC Version

    \\"

    **Fixes**
* Fixed a bug in version 1.4.7 and 1.4.8 where the application detection script may fail to evaluate when the application is deployed to a user collection as available, and a non-admin user initiates the installation. Note: this was a regression bug from version 1.4.1.

### 1.4.8 - 2019-08-07

#### Improvements

*   PowerShell detection scripts can now be saved in an additional folder using a registry value. Based on UserVoice item:

    [Detection Method Scripts Location](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-317)
* Settings file can now be saved in an additional folder from the advanced tab. Based on UserVoice item: [Publishing Service configure backup path](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-313)
* Add an option to always check the local content repository to update content prior to downloading from the internet. Based on UserVoice item: [Check Local Content Repository for All Products](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-266)
*   Dependencies are retained when updating SCCM App

    **Fixes**
* Fixed an issue where the detection method script may show invalid signature on the client-side.

### 1.4.7 - 2019-08-01

#### Improvements

*   Powershell detection method scripts are now saved in the

    \\\Detection Method Scripts folder.
*   Set requirements to prevent the installation of Flash Player ActiveX on Windows 10 and Windows Server 2016 and 2019 and higher.

    **Fixes**
* Products that don't support the application model would be created as a package even if the option to not fall to a package is enabled.

### 1.4.6 - 2019-07-30

#### Fixes

* Fixed an issue where application update drop-down menu wouldn't be retained.

### 1.4.5 - 2019-07-29

#### Improvements

* The right-click context menu item checkbox will now be checked for the pre/post scripts feature when only addition files are added in the pre/post script dialog window.
* If an application is deleted from the SCCM and the content source folder still exists, the application will be re-created during the next sync schedule if it's enabled.
* If the application deployment type is set to Allow users to view and interact with the program installation, you will no longer see a dialog window for PatchMyPC-ScriptRunner.exe.
* We now handle the non-standard exit codes for Adobe Digital Edition and Evernote so the installation will report successful.
*   MSI based applications will now have the repair command line configured in the deployment type.

    **Fixes**
* Fixed an issue where the detection method PowerShell script may not be code-signed if there was more than one certificate in the WSUS certificate store.
* Fixed an issue where applications may fallback to the package model when a publishing sync if performed at the same time the SMSProvider DLL's are being registered during a site upgrade.
* Fixed an issue where the uninstall command line may be empty after an MSI based product performed an in-place upgrade to a newer version.

### 1.4.4 - 2019-07-26

#### Improvements

*   Email reports for publishing updates and applications will now be listed alphabetical order.

    **Fixes**
* Fixed an issue where if multiple certificates exist in the WSUS certficaite the detection method script may not get code-signed.

### 1.4.3 - 2019-07-24

#### Fixes

* Fixed an issue wherein a small number of cases applications may fail to install with the following error "An error occurred while preparing the installation of the application: Illegal characters in path." in PatchMyPC-ScriptRunner.log
*   Improved detection for CutePDF Writer and Allway Sync

    **Changes**
* Updates and applications will now timeout after thirty minutes
* The ESC key will no longer close the publishing service UI
* If timestamping is disabled for update publishing, the detection method PowerShell script will now not be timestamped

### 1.4.2 - 2019-07-22

#### Features

* Added an option to include abitrary files in the pre/post script dialog box.
*   Added an option to copy the installation log to a secondary folder on installation failure.

    **Fixes**
*   Updated the detection method script for applications to resolve the following error (Access to the path

    'C:\Windows\CCM\Logs\PatchMyPC-SoftwareDetectionScript.log' is denied.) that would occur in AppDiscovery.log in certain builds of Configuration Manager.

### 1.4.1 - 2019-07-15

#### Features

*   The base installation feature now creates applications in SCCM rather than legacy packages. Based on customer idea:[Base Installation Feature Should Create Applications not Packages in SCCM](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-16)

    **Improvements**
* You can now configure an offset (in days) for the sync schedule. Based on customer idea: [Schedule Patch Tuesday +1 (Offset From Date)](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-138)
* When using a custom pre/post update script, it will be run before any Patch My PC defined script. Based on customer idea: [Run custom pre-update scripts before any PatchMyPC defined scripts](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-177)

### 1.4.0 - 2019-07-10

#### Changes

* This update contains improvements to help support the future release of the application creation feature.

### 1.3.9 - 2019-07-02

#### Changes

* The installed version of the publishing service and whether you have opted into the preview channel will be reported.

### 1.3.8 - 2019-06-07

#### Fixes

*   Fixed an issue where if you switch from the general tab to the update rules tab very quickly the products enabled may reset and the Settings.xml would need to be restored from the

    \\\Backup folder.

    **Improvements**
* Added an option to prefix the computer name to the installation log file name to allow you to use a shared path and receive unique log file names for each device.

### 1.3.7 - 2019-06-04

#### Fixes

* Improved publishing for products that use special characters in their install command line.
  * Fixed an issue where up to 5 products may continually be detected as being revised during publishing syncs.
  * During the first publishing sync after this update, you may see up to 40 products say that where revised and this can be safely ignored.

### 1.3.6 - 2019-06-03

#### Fixes

* Fixed an issue where the "**Automatically create installation packages in SCCM for initial installation.**" in the **Package Rules** tab would become un-checked when in trial mode.

### 1.3.5 - 2019-05-23

#### Features

* Added a new right-click context menu item to add MST transformation files for MSI based product installers.
* Right-clicking on a product will now display the installer technology the product uses (MSI, EXE, or MSP)
*   Added support for customer SSRS folder names for the report installer

    **Fixes**
* Bug fixes

### 1.3.4 - 2019-05-02

#### Improvements

* You will no longer receive an invalid license ID on start in the event no license ID was defined previously.

### 1.3.3 - 2019-05-02

#### Features

* Added support for required Pre/Post-Scripts
*   Added support for recommended Pre/Post-Scripts

    **Improvements**
* We will now cache the list of supported products, so in the event, the settings tool can't download the latest products, it will use the last cached copy.
* When the settings tool is opened, if any products are previously enabled that now have a Patch My PC defined recommended and required Pre/Post script(s) those scripts will be saved in the settings.xml automatically.
*   When there is a product enabled that requires a [manual content download](https://patchmypc.com/local-content-repository-for-licensed-applications-that-require-manual-download) the product name(s) will be included in the prompt.

    **Fixes**
* Fixed an issue where the UI may show not responding for a short period of time on initial open.
* Fixed an issue where you may receive a prompt saying some settings are missing when clicking apply when using trial mode when all relevant settings are correct.

### 1.3.2 - 2019-04-19

#### Features

*   Added a section in email report for updates published with Local Content Binary

    **Improvements**
* Better handling of situations where SupportedProducts.xml fails to download
* 3010 is considered as a success code by for pre-scripts when the option to bypass update installation when pre-script fail, is enabled

### 1.3.1 - 2019-04-12

#### Features

* The option to scan SCCM for applications will now be more accurate for products split by major versions.
* You will now receive an email notification if your subscription is expired causing synchronizations to fail to run.
* Improved error messages in logs and emails.
* Updated the PatchMyPC.chm documentation included in the MSI installer.

### 1.3.0 - 2019-04-09

#### Features

* Added the new option to enable the creation of base installation packages in SCCM.
* Other feature improvements and bug fixes
* Disabled the delete option for published updates in the modify published updates wizard.
  * To enable the Delete button, create a new DWORD registry value: Computer\HKEY\_LOCAL\_MACHINE\SOFTWARE\Patch My PC Publishing Service:EnableDeleteUpdates = 1. We only recommend using this option when working with our support team.
* Added an option to disable timestamping. We generally do not recommend using this unless there is a specific use case. To disable timestamping you can create a DWORD registry value:: HKEY\_LOCAL\_MACHINE\SOFTWARE\Patch My PC Publishing Service:DisableTimestamping = 1
* Added an option in the About tab to opt-in to the preview channel.
*   Added subscription level and licensed device count based on feedback in the SCCM slack group.

    **Improvements**
* We removed the two columns displaying the distribution point group and description in the base installation options dialog.
* Change the error return for 404 download errors.
* Changes to improve the performance of the license validation check.
* Revisions to packages are now included in email reports.
* When using the Scan SCCM for Managed Applications feature, the database server, database name, and connection account details will be retained after a successful query.
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
  * WinZip
* When a package is created for a 64-bit product, the requirements will be configured on the program to only install on 64-bit operating systems
* If a package fails to be created, the distribution attempt to SCCM distribution points will no longer be performed.
* Added an option to change the subject name for email notifications
*   Added an option to include text in the body of the email notifications.

    **Fixes**
* Fixed an unhandled exception when you enable base packages when no catalog URL is set.
* Fixed an issue where updated installation packages are not added in the email report
* Fixed an issue where superseded applications may not publish into SCCM
* Fixed an issue where SCCM package creation is malformed when updates are configured to be republished.
* Fixed an issue where products are still listed in the SCCM application scan when the Include Products Already Enable in Scan is not checked.
* Miscellaneous fixes

### 1.2.5 - 2019-03-14

#### Features

* Added an option in the About tab to opt-in to the preview channel.

### 1.2.4 - 2019-02-27

#### Changes

* Increased the number of backup settings files saved from 5 to 50
* Fixes an issue where MSI logging options may be removed from a previously published update
*   Improved logging

    **Fixes**
* The Local Content Repository textbox is now read-only

**Note:** Build 1.2.4 was re-released on 2019-03-07 to resolve an issue where the license validation may fail after the initial installation.

### 1.2.3 - 2019-02-20

#### Improvements

* Added the ability to provide custom arguments to pre/post scripts
* Added support to run EXE or MSI binaries in the pre/post scripting feature
* Added a new option in the right-click context menu in the product rules to republish update(s)
* Improved the auto kill/close feature for applications where the process name may change between different versions
* Improved the HTML email report format and color
* Improved error handling if the WSUSPool or WSUS Service is in a stopped state
*   When the user triggers a self-upgrade via the about tab, a progress bar is displayed, and the publishing settings UI will reopen after the update.

    **Fixes**
* Fixed a bug where the SCCM application scan wrongly displays the Java migration update as being installed
* Other minor bug fixes

### 1.2.2 - 2019-02-05

#### Improvements

* Added option to "**Un-Decline**" updates in the "**Modify Updates Wizard**"
* Added new right-click action in the "**Product Rules**" tab to allow you to enable **installation logging for updates** and choose a standard path for the installation logs.
* The option to "**Scan SCCM for Managed Applications**" will now list **all products available in the catalog** even when the publishing service is in **trial mode**.
* Improved logging, when there are **known publishing error codes**, we will now link to any **KB articles containing the resolution**.
* Added option in the "**About**" tab to "**Disable Self-Updates**" based on customer feedback.

### 1.2.1 - 2019-01-21

#### Improvements

* Added filter textbox to allow free-form typing to filter updates in the "Modify Updates Wizard"
* Added option in the Pre/Post Script dialog to not attempt an update if the pre-update script returns an exit code other than 0.
* Right-click custom actions on the "All Products" in the "Product Rules" tab will be retained when the Publishing Settings tool is re-opened.

### 1.2.0 - 2019-01-15

#### Improvements

* Added filtering options in the "Modify Updates Wizard"
* Added CC field in the SMTP Settings
* Added common SMTP providers in the SMTP Settings
* Added last day of the month and last week of the month options in the "Sync Schedule"

### 1.1.9 - 2018-12-27

#### Fixes

### 1.1.8 - 2018-12-24

#### Improvements

* Added "**About**" tab that shows version information, release notes, support options, and how to request new products.
*   Added "**Local Content Repository**" option in the

    "**Advanced**" tab. This feature is used if there are licensed products that don't allow for public download in the future. For more details, please see [licensed products that require a manual download](https://patchmypc.com/local-content-repository-for-licensed-applications-that-require-manual-download)

### 1.1.7 - 2018-12-13

#### Fixes

* Fixed a scheduling issue where you may see higher than average CPU utilization if the schedule was set to the Second Tuesday of the month.

### 1.1.6 - 2018-11-20

#### Fixes

*   Fixed an issue where updates may fail to publish on WSUS 3.0 SP2

    (Windows Server 2008 and Windows Server 2008 R2)

### 1.1.5 - 2018-11-19

#### Improvements

* HTML email improvements
  * Update title is now clickable and will link to the vendor's release notes for the update
  * Added Classification tab to the report
  * Added Severity tab to the report
  * Added CVE tab to the report
  * When there is only one CVE, the CVE-ID will be clickable and link to [https://cve.mitre.org](https://cve.mitre.org)
* We will now retain on previous version PatchMyPC.log and rename it to PatchMyPC.lo\_ when the max log size is reached.
*   If a product doesn't support pre/post update scripts, the option will no longer be visible in the right-click action

    **Changes**
* Changed the PatchMyPC.log from 10MB to 2MB

### 1.1.4 - 2018-10-25

#### Improvements

* Within the "Product Rules" tab, we have added a new option called "Disable self-updater". For applications that support this feature, we will automatically disable the self-update feature for the product after applying any new update. This option is available on the All Products, Vendors, and Product level in the Product Rules treeview.
* When custom actions are enabled for a product, the PatchMyPC-ScriptRunner.log will save to %WinDir%\CCM\Logs by default rather than %WinDir%\Temp on the client side for logging custom actions.

### 1.1.3 - 2018-09-30

#### Improvements

* Added the ability in the product rules tab to connect to the Configuration Manager database to scan for supported products from our catalog and enable detected products for publishing.

### 1.1.2 - 2018-09-17

#### Improvements

* Enabled the kill and skip process option for almost all products
* Added a new right-click context menu option for deleting the public desktop shortcut when applicable

### 1.1.1 - 2018-09-06

#### Improvements

* Added support to use patchmypc.com in the catalog subscription URL. Previously, you could only use patchmypc.com for your subscription URL.

### 1.1.0 - 2018-09-03

#### Improvements

* Added an option to define your own custom pre/post update scripts in each products right-click context menu.
* Added an option to open the wsyncmgr.log in the General Settings tab.

### 1.0.9 - 2018-08-20

#### Improvements

* Added the ability to change published updates visibility in the WSUS console from the Modify Published Updates wizard in the advanced tab
* Added a column to show declined updates in the modify updates wizard
*   Auto-refresh display in the modification updates wizard when

    «Declined» or «Delete» button is pressed
* Added a checkbox in the scheduling tab to synchronization the Software Update Point after the publishing services completes and any updates are published or modified
* Added the size of the downloaded file in the log file
* Improved performance when reading the settings file

### 1.0.8 - 2018-08-12

#### Improvements

* Added the ability to customize the certificate expiration length and key strength when generating a self-signed certificate.
* Emails will now use an improved HTML format instead of plain text.

### 1.0.7 - 2018-07-23

#### Improvements

* We added a new option to expire all or specific published third-party updates from the Advanced tab.

### 1.0.6 - 2018-07-08

#### Improvements

* Added a new tab called Advanced
* New option in the Advanced tab named "**Standalone WSUS Mode**".
  * When enabled, third-party updates published from the publishing service will be visible and available to deploy directly in the WSUS console. This option shouldn't be enabled if Microsoft SCCM is being used to deploy updates.
* Moved the option "Defer Expiration of Updates" from the Scheduling tab to the Advanced tab.

### 1.0.5 - 2018-06-15

#### Improvements

* Added the ability to delay the re-publishing of expired updates.

### 1.0.4 - 2018-06-13

#### Improvements

* The "Product Rules" tab now supports a semi-checked mode. The semi-checked will appear when only some products under a vendor are enabled.
* You can now schedule the scheduler to when every X (1-4) week of the month on a specific day.

### 1.0.3 - 2018-05-30

#### Improvements

* We added a right-click context menu for vendors and products in the Product Rules tab.
  * We added two new options that allow you to kill an applications process before performing an update or skipping the update install if conflicting processes are running. \*

### 1.0.2 - 2018-05-20

#### Improvements

* Added a new checkbox in the "Product Rules" tab "Use a single vendor name (Patch My PC)". This option will publish all updates under a vendor named "Patch My PC" and product named "SCUP Updates". This options will allow a single vendor to be enabled in the Software Update Point "Products" tab, and any new products enabled in the publishing service will show up in the next SCCM sync and won't require additional products to be enabled in the Software Update Point. This option will be enabled during a clean install of the publishing service. If you had a previous version and upgrade, you would need to enable this option and save your settings.

### 1.0.1 - 2018-05-16

#### Fixes

* Fixed a proxy password issue. If the password was 16 characters or a multiple of 16x, it wouldn't save correctly in the Settings.xml file.

### 1.0.0 - 2018-05-14

* Initial Release
# Release notes for Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Details the production release history for Patch My PC (PMPC) Cloud, the most recent release being shown first.

{% hint style="info" %}
**Note**

We aim to release new features, updates, and fixes at 12:00 CEST every Wednesday.

_Production Release_ means we have released that item to our Production environment i.e. customers can access it, although a specific feature maybe in one of the following three production states:<br>

* Private Preview, which is invitation-only.
* Public Preview for which you will need to have [Preview Features enabled](../manage/settings/company-settings/preview-features.md) in your company to access it.
* General Availability (GA) which is available to everyone.

Please see the relevant docs for a feature for more information which will indicate the state of the feature, plus you can see a list of [Cloud Preview Features](../preview-features.md) for more information.

You can also access this page from within the Cloud Portal by clicking the support button (!["support" button](../../.gitbook/assets/image-\(587\).png)) in the header area and selecting **Release Notes**.

Release Notes for previous years can be accessed using the following links:

[2025](2025.md) | [2024](2024.md)
{% endhint %}

## Week of August 5th, 2026

<details>

<summary>New Features/Improvements</summary>

#### Intune Apps

* **Improved “Install Parameters” tool –** We now highlight any additional arguments that have been entered that were already detected from the app’s metadata in our App Catalog.

</details>

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue where adding an additional language to an existing Branding App caused an error that required fields were missing, when in fact they weren’t.

#### Custom Apps

* Resolved an issue where, if a Custom App is published using Publisher, the **Additional Uninstall Parameters** field in Cloud is not updated.

</details>

## Week of July 22nd, 2026

<mark style="color:red;">**NOTE:**</mark> No release Week of July 15th

<details>

<summary>Fixes</summary>

#### Custom Apps

* Resolved an issue where, after updating an existing script-based Custom App that uses a folder of files by using **Add Version**, the upload became stuck.

</details>

## Week of July 8th, 2026

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue with Filter names for assignments being truncated.

</details>

## Week of July 1st, 2026

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue with the Admin Portal where trial customers were incorrectly treated as having an invalid license, which prevented them from running a Full Resync.

#### Custom Apps

* Resolved an issue with a self-healing End-of-Life (EOL) enhancement that incorrectly marked Custom App deployments as EOL after adding a revision, as Custom Apps were not excluded from the EOL evaluation logic.

</details>

## Week of June 24th, 2026

<details>

<summary>Fixes</summary>

#### Custom Apps

* Resolved an issue where if a file upload was interrupted and the user started a new upload, background retries from the previous (deleted) file continued running and incorrectly updated the upload state, causing the Custom App to get stuck in an **In progress** state.

#### Intune Apps

* Resolved an issue with Snoozing notifications, where the “Snoozing notifications” days value in a deployment was not propagated to Intune, so the original value continued to be used.
* Resolved an issue where if a deployment failed to create a package, the previous AppId was also lost, preventing the system from tracking and deleting older app versions in Intune.
* Resolved an issue with requirements scripts where the requirement script generated in the Cloud Portal differed from the one sent to Intune.

#### Migration

* Resolved an issue when migrating script-based and PSADT apps, where the system automatically interpreted scripts without clearly informing users, which could lead to mismatches with the original logic.

</details>

## Week of June 17th, 2026

<details>

<summary>New Features/Improvements</summary>

#### Intune Apps

* **Permission Validation –** Improves the user experience by clearly showing which permissions the PMPC Company has/has not been granted in the Cloud Portal. Only the features that can be used with the granted permissions are enabled. All other features will be unavailable to help prevent errors.

#### Custom Apps

* Resolved an issue where if several files were uploaded for a Custom App and one failed, the whole upload failed. Now, if an upload fails, users can retry just the failed files.
* Resolved an issue with Intune failing to detect migrated 64-bit Custom Apps.

#### Intune Apps

* Resolved an issue where updating a custom uninstall script did not trigger regeneration of the deployment package, so the old script continued to be used even after recreating the deployment.

#### PSADT

* Resolved an issue with non-PSADT scripts failing to run if they define commands with the same name as PSADT commands.

</details>

## Week of June 10th, 2026

<details>

<summary>Fixes</summary>

#### Intune Apps

* Resolved an issue with deployment sync behavior that could remain stuck during multi-revision scenarios.
* Resolved an issue with category mapping behavior that prevented expected version updates.
* Resolved an error that blocked customers from creating deployments.
* Resolved a forbidden access issue when retrieving customer domains through Intune-connected workflows.
* Resolved a tenant device service error that caused endpoint failures.

#### Migration

* Resolved an issue with storage size messaging so that migration limits are displayed correctly in the UI.

</details>

## Week of June 3rd, 2026

<details>

<summary>New Features/Improvements</summary>

#### Intune Apps

* **Warning added to the Deployment Drawer –** If a deployment encounters an error, we now show the error on the deployment drawer (i.e. when you click the deployment).

</details>

<details>

<summary>Fixes</summary>

#### Intune Apps

* Resolved an issue where changing the Branding type from Classic to Modern did not display the correct version of the chosen log.

#### Managed Service Provider

* Resolved an issue where the name of the Parent Company was always included in the list of assignments for an App Set, even if the app was not assigned to the Parent Company.

</details>

## Week of May 27th, 2026

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue where opening **Available Groups** in the Cloud Portal returned **An error occurred while processing your request** notification.

#### Custom Apps

* Resolved an issue where no validation message was displayed if either no value or an incorrect value was entered in the **Value** field when adding a Detection Rule.

#### Managed Service Provider

* Resolved a validation issue where an App Set could be created without an Assignment.

</details>

## Week of May 20th, 2026

<details>

<summary>Fixes</summary>

#### Binary Free Apps

* Resolved an issue where apps with partially uploaded binaries could not be deployed for variants that had completed binary uploads. We now allow deployments to proceed correctly when only some variants have been fully uploaded.

#### Custom Apps

* Resolved an issue where the deployment state of a Custom App was not updating correctly in the Cloud Portal.

#### Migration

* Resolved an issue where Custom Apps were assigned a **Failed** status during migration despite completing the process successfully.
* Resolved an issue where scripted Public Apps were incorrectly reclassified as Custom Apps after reanalysis, causing them to lose their assigned category.

</details>

## Week of May 13th, 2026

<details>

<summary>Fixes</summary>

#### Custom Apps

* Resolved an issue where the checkmark was not present in the **OS Architecture Requirements** section after updating the architecture for an app.
* Resolved an issue where silent install parameters were not saved after adding an app.

#### Intune Apps

* Resolved an issue handling Continuous Access Evaluation (CAE) claims challenges when connecting to Intune. This resolved connectivity issues for customers using CAE-enabled environments and improved access security validation.
* Resolved an issue where searching for an app name with and without spaces returned inconsistent results.

#### Migration

* Resolved an issue where the **Enable** button under **Enable Migration** remained visible when the **Enable Application Migration** checkbox was unchecked.

</details>

## Week of May 6th, 2026

<details>

<summary>New Features/Improvements</summary>

#### Portal

* **Improved Company Recovery process –** We have improved the process for recovering access to a PMPC Cloud Company to cater for more scenarios.

#### Custom Apps

* **Support for Unicode/non-ASCII characters –** You can now use Unicode/non-ASCII characters when creating and working with Custom Apps.

</details>

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue where, if a Support Request was raised, an event was not written to the **Events** node.

#### Custom Apps

* Resolved an issue where, after creating a Custom App and providing silent install parameters, when you edited the app, these were mistakenly removed.

#### Intune Apps

* Resolved an issue where the **Installation Command line** field on the **Summary** tab of a scripted app appeared empty.
* Resolved an issue where deploying a discovered caused an error on the deployment page.

#### Migration

* Resolved an issue where PSADT apps were not migrated correctly from ConfigMgr.

</details>

## Week of April 29th, 2026

<details>

<summary>Fixes</summary>

#### Intune Apps

* Resolved an issue with ScriptRunner+ deployments with a command line exceeding 1,024 characters failed with the error "**CommandLine exceeds maximum allowed length of 1024 characters.**”

#### Managed Service Provider

* Resolved an issue where if an MSP admin impersonates a user account in the Cloud Portal, the remaining access time shown during impersonation does not match the actual granted access duration.

#### Migration

* Resolved an issue where migrating a 32-bit ARM app resulted in the app being migrated as ARM, but the 32-bit option was removed and greyed out.
* Resolved an issue with our AI being unable to process a script containing PSADT commands.
* Resolved an issue where not all ConfigMgr Apps were appearing in Migration.

</details>

## Week of April 22nd, 2026

<details>

<summary>New Features/Improvements</summary>

#### Advanced/Patch Insights for Intune

* **Improved Client/Uninstall –** We’ve made several improvements to how you install/uninstall the PMPC Client.

</details>

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue where a user assigned just the **Report Admin** role was able to connect/enable the Microsoft Defender for Endpoint integration from Intune.
* Resolved an issue where, after a PMPC Cloud trial has expired, it is not possible to uninstall our Client as the **Save** button is disabled.
* Resolved an issue where if a new user (who is part of the customer’s organization) tries signing into Cloud using a custom domain name configured in the Cloud Portal, it fails to authenticate.

#### Custom Apps

* Resolved an issue where, during the Custom Apps creation process, apps that were still uploading (i.e. hadn’t finished being created) were shown in Publisher.

#### Migration

* Resolved an issue where if apps had "**.\\**" at the beginning of the installation file name in the .ps1 script and the AI toggle is enabled, PSADT apps are displayed as **Not Supported**.
* Resolved an issue where the **Display Name** for some apps is not displayed in the **App Update Status**.
* Resolved an issue where a Public app with options had the option to be migrated as an app with multiple matches instead of just a Public app.

</details>

## Week of April 15th, 2026

<details>

<summary>Fixes</summary>

#### Custom Apps

* Resolved an issue where after adding an additional script for PSADT to an existing Custom App, when installing the app on a VM, it failed with "**Failed to unzip**".

#### Intune Apps

* Resolved an issue with apps that use different languages for the Add/Remove Program entry, with ScriptRunner not searching for the app based on the RegEx of all possible names.

#### Migration

* Resolved an issue where some properties are not shown on the **Summary** tab during migration.

</details>

## Week of April 8th, 2026

<details>

<summary>Fixes</summary>

#### Binary Free Apps

* Resolved an issue where, even though all variants for some apps had been uploaded, the user still saw a prompt to upload a file.

#### Intune Apps

* Resolved an issue where the PMPC read-only script was displayed as unsigned when creating a deployment with an Update-only assignment.

#### Migration

* Resolved an issue where, during the analysis of an app, it was showing as being available for migration even though the analysis had not completed. Now an app will be unavailable for migration until the analysis has been completed.
* Resolved an issue where some properties completed during migration were not shown on the **Summary** page.

</details>

## Week of April 1st, 2026

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue where adding an image to a support request resulted in an HTTP 500 error.

#### Binary Free Apps

* Resolved an issue where if an app has both binary and binary-free variants, the binary-free logic did not work.

#### Intune Apps

* Resolved an issue where customers were receiving different variants of the app or configurations than the ones they had originally set.
* Resolved an issue that when trying to edit an existing deployment, the following error was shown **Validation error on "getProductInfoByProductIdForDeployments", Expected object, received undefined.**
* Resolved an issue where an app fails to install if the Registry path contains custom requirements such as **HKLM:** or **Registry::**
* Resolved an issue where changing variants in a deployment did not update the list of **Tools** on the **Configuration** tab.
* Resolved an issue where after deleting an assignment for a deployment containing ESP Profiles, the ESP Profiles themselves were not reevaluated, potentially highlighting errors in their configuration.

#### Migration

* Resolved an issue when creating a deployment for an app that was previously migrated, resulting in **An error occurred while processing your request** error.

</details>

## Week of March 25th, 2026

<details>

<summary>New Features/Improvements</summary>

#### Intune Apps

* **Custom Requirement Rules –** The new Custom Requirement Rules feature has been released to Public Preview. This feature allows you to configure custom requirement rules directly in the Cloud Portal when deploying applications.

#### Managed Service Provider

* **Multi-variant support in App Sets –** You can now add the same app with different variants to the same App Set.

</details>

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue where notification emails sent from the Portal either weren’t sent or came through blank.

#### Intune Apps

* Resolved an issue where, if a deployment was initially created without assignments, when editing the deployment, we allowed users to add Update Rings. This conflicted with the intended logic (deployments without assignments may rely on manual Intune assignments, and adding rings later could create inconsistencies). You can no longer add Update Rings when editing a deployment created without assignments.
* Resolved an issue where applying a deployment template to a deployment and then switching the **Installer Type** did not trigger the dialog warning that doing so would cause the values of the deployment to be reset based on the new installer type, potentially resetting those set in the template.
* Resolved an issue where applying a default deployment template cleared all existing form errors, even if the inputs were still invalid.
* Resolved an issue where unsupported deferral-related variables were allowed in various fields for localizations defined in Branding apps. The UI now shows the correct values under each relevant field.

#### Migration

* Resolved an issue where if an app was migrated from one variant to a different ProductId, the deployment could not be edited.

</details>

## Week of March 18<sup>th</sup>, 2026

<details>

<summary>New Features/Improvements</summary>

#### Portal

* **Ability to see your License Key –** Now, on the **Subscription** page, we’ve added an eye icon that lets you view your full license key.
* **“Apps & Feature” updated –** Given that Windows 11 uses the **Installed Apps** applet to view installed software, we have now renamed all instances of **Apps & Feature** in the product to **Installed Apps** instead.
* **Improved Visibility of Trial Limits –** Now on the **Subscription** page, we show you the product limits when you are using a trial account to help you familiarize yourself with the product and our different subscription levels.

</details>

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue where if we had deployments for both a regular variant of an app and a Binary Free variant, after creating a deployment for the regular variant, validation would fail.

#### Custom Apps

* Resolved an issue where clicking **Add App** or **Add Version** for an existing Custom App resulted in an HTTP 500 error.

#### Managed Service Provider

* Resolved an issue where editing an App Set containing two variants of the same product caused broken deployments.

#### Migration

* Resolved an issue where if there were two updates available for an app, it generated an error. Now only the latest update is shown.

</details>

## Week of March 11<sup>th</sup>, 2026

<details>

<summary>New Features/Improvements</summary>

#### Migration

* **New Multiple Matches category –** Now, all apps with multiple matches in our App Catalog are displayed on the dashboard as **Multiple Matches**, so you know you need to select which app these apps should be migrated to.
* **New Scripted App Matching –** The Migration feature can now match scripted apps from ConfigMgr to a Public App Catalog app to allow you to migrate these apps as Public so you can keep them up-to-date.

</details>

<details>

<summary>Fixes</summary>

#### Portal

* Resolved an issue with the Template feature not validating the relationship between Update Ring delays and the Sync Schedule frequency. When the delay between rings was less than the Sync Schedule frequency, no warning was shown, which could lead to ineffective or misleading deployment timing.

#### Custom Apps

* Resolved an issue where clicking either **Add App** or **Add Version** (for an existing Custom App) resulted in an HTTP 500 error.

#### Intune Apps

* Resolved an issue where adding a new Detection Rule resulted in a **Type** of **0** and no content.

#### Managed Service Provider

* Resolved an issue where editing an App Set took an extended amount of time and resulted in an **AbortError:signal is aborted without reason** error.

</details>

## Week of March 4<sup>th</sup>, 2026

<details>

<summary><strong>Fixes</strong></summary>

#### Custom Apps

* Resolved an issue where deployments were not recreated on sync if extra files were present and the installation file was changed.
* Resolved an issue where deployments were recreated incorrectly in scenarios when they should not have been.
* Resolved an issue where a newly created Custom App is not visible in Publisher after it has been deployed.

#### Migration

* Resolved an issue where the failed validation (red ’**x**’) is shown on the **General** tab when migrating an app, instead of the **Files** tab, if the app being migrated has no **Installation Script** defined.
* Resolved an issue where the deployment status for a migration was not updated after a successful migration.

</details>

## <sup>Week of February 25th, 2026</sup>

<details>

<summary><strong>Fixes</strong></summary>

#### Binary Free Apps

* Resolved an issue where if a user added a new version of a Binary Free App, any existing deployments could not be updated.

#### Custom Apps

* Resolved an issue where if a Custom App is deployed for the ARM architecture and then edited to uncheck ARM, the ARM option remains unchecked once the deployment is saved.

#### Intune Apps

* Changed the default timeout settings for Conflicting Processes Notifications to a maximum of 1,380 minutes with a 60-minute buffer before the notification times out to improve deployments.
* Resolved an issue where macOS deployments were recreated on the Sync Schedule even if the app that was deployed had not been updated.
* Resolved an issue where editing the deployment for an app and changing the assignment type and variant resulted in the app being recreated with a new revision. Now the app is recreated with the current revision whenever it is edited.
* Resolved an issue where if the **Disable the Patch My PC Recommended scripts** option was selected for a script that used a disallowed filename, the deployment could not be completed.
* Resolved an issue where if a user edits the **Notify Timeout Configuration** value for a deployment, the change does not appear in the **Installation time required** property in Intune.

#### Managed Service Provider

* Resolved an issue where if an app belonging to an AppSet is marked End of Life, any deployments to new customers of that AppSet get stuck **In Progress** and then eventually fail.

#### Migration

* Resolved an issue where the status of a migration was not updated to **Success** upon the successful migration of an app.

</details>

## <sup>Week of February 18th, 2026</sup>

<sup>No release.</sup>

## <sup>Week of February 11th, 2026</sup>

<details>

<summary><strong>Fixes</strong></summary>

#### **Binary Free Apps**

* Various fixes and improvements to how app updates are handled.

#### **Custom Apps**

* Various fixes and improvements to how app updates are handled.

#### **Intune Apps**

* Various fixes and improvements to how app updates are handled.

#### **Migration**

* Improved performance when migrating apps.
* Improved error handling by Publisher when migrating apps.
* Resolved an issue where the most matched app was shown in the middle of the list instead of the top.

</details>

## <sup>Week of February 4th, 2026</sup>

<details>

<summary>Fixes</summary>

#### **Binary Free Apps**

* Resolved an issue where adding a new revision to an app did not trigger the email to the user informing them they need to upload the relevant file for the new revision.

#### **Custom Apps**

* Resolved an issue where adding a new revision to a Custom App did not force the associated deployment to be recreated.

#### **Intune Apps**

* Resolved an issue where, if a deployment has been manually recreated in between Sync Schedules, the deployment was recreated again at the next Sync Schedule.

</details>

## <sup>Week of January 28th, 2026</sup>

<details>

<summary>New Features/Improvements</summary>

#### **Portal**

* **ConfigMgr to Intune App Migration** - [This feature](../migration/) has now been releasd to General Availability.
* **Improved Webhook handling –** Now, if you have multiple Webhooks and one is invalid, the rest will still function. Previously, if one Webhook was invalid, it prevented notifications from being sent by other Webhooks, even if they were valid.
* **Improved Limits Warnings –** Now, when you reach 90% of the limits for your Cloud Company, we will display a banner warning you about this, so you can perform some housekeeping or consider upgrading to a different version with increased storage limits.

#### **Advanced/Patch Insights for Intune**

* [Officially released](../insights-intune/) to General availability.

#### **Intune Apps**

* **Improved Intune Disconnection –** To help you better understand the consequences of [disconnecting your Intune connection](../manage/settings/connections/disconnect-connection.md#disconnect-intune), we now require you to take additional steps before we let you do this.

</details>

<details>

<summary>Fixes</summary>

#### **Managed Service Provider**

* Resolved an issue with the processing of App Set status messages in the wrong order, preventing App Sets from being edited.

#### **Migration**

* Resolved numerous issues as we continue to develop this feature.

</details>

## <sup>Week of January 21st, 2026</sup>

<details>

<summary>New Features/Improvements</summary>

#### **Portal**

* **More Information on Preview Features –** A new [More Info](../preview-features.md) link has been added to the **Preview Features** section of the **Company** page. This links to our docs, where you can find out more information about each of the features currently in preview.
* **New "Report Admin” User Role –** This new user role only has Read-Only access to the **Reporting** and **Settings** nodes.

</details>

<details>

<summary>Fixes</summary>

#### **Portal**

* Resolved an issue where, for some Enterprise Premium customers, trial limits were being incorrectly enforced.
* Resolved an issue where editing a deployment with no assignments and changing the architecture resulted in older versions being removed from Intune. We now no longer support changing the architecture for a deployment with no assignments.

#### **Custom Apps**

* Resolved an issue where editing a Custom App caused the **Max Storage Limit** to be increased even if no additional files were added.

#### **Intune Apps**

* Resolved an issue where an app with several dependencies was not applying the dependencies correctly.
* Resolved an issue where if an app has multiple Windows assignments and a macOS deployment, editing the Windows deployment brings up details for the macOS deployment.

#### **Migration**

* Resolved numerous issues as we continue to develop this feature.

</details>

## <sup>Week of January 14th, 2026</sup>

<details>

<summary>New Features/Improvements</summary>

#### **Intune Apps**

* **Updates to Public Apps –** Now when we update a public app in the App Catalog, we do not update the deployed version in your PMPC Company until the next Sync Schedule runs in your company.

</details>

<details>

<summary>Fixes</summary>

#### **Migration**

* Resolved numerous issues as we continue to develop this feature.

</details>

## Week of January 7<sup>th</sup>, 2026

<details>

<summary>Fixes</summary>

#### **Advanced/Patch Insights for Intune**

* Resolved numerous other issues as we continue to develop this feature.

#### **Intune Apps**

* Resolved an issue where editing a macOS deployment resulted in the **pkg** installer type being selected incorrectly instead of the **pkg (LoB)** option for LOB apps.

#### **Migration**

* Resolved numerous issues as we continue to develop this feature.

</details>

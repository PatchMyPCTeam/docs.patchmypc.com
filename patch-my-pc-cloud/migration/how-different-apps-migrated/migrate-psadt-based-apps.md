# Migrate PSADT-based Apps

_Applies to: Patch My PC Cloud_

When applications are inventoried from Microsoft Configuration Manager (ConfigMgr), Patch My PC (PMPC) Cloud analyzes the application metadata to determine how the application is installed and how it should be migrated. As part of this process, the installation command line is evaluated, and the primary installer file is identified from the application’s content source folder.

## Identifying a PSADT-based App

ConfigMgr does not explicitly label an application as PSADT-based. In most cases, the easiest way to confirm that an application is PSADT-based is to select the application from the Migration dashboard and review the **Installation Program** field.

If the **Installation Program** contains a **Deploy-Application.exe**, **Deploy-Application.ps1**, **Invoke-AppDeployToolkit.exe** or **Invoke-AppDeployToolkit.ps1**, the application can be considered PSADT-based.

![PSADT-based app identified from the installation program](/_images/image-(3825).png "PSADT-based app identified from the installation program")

During the migration deployment flow, the **Configuration** tab indicates when an application has been identified as PSADT-based. Detection is based on the presence of PSADT functions in the script; when detected, the PSADT module is automatically enabled. The script content is analyzed and logically split into pre-install and post-install scripts.

![PSADT-based app shown in the deployment flow](/_images/image-(3826).png "PSADT-based app shown in the deployment flow")

When migrating PSADT-based applications, AI can assist with parsing the PowerShell script and identifying key components, including the primary installer and the **MARK: Pre-Install**, **MARK: Install**, and **MARK: Post-Install** sections. This allows the script to be accurately split around the main installer and mapped to the appropriate pre-install and post-install execution stages.

Without AI assistance, reliably separating PSADT scripts into pre-install and post-install logic can be challenging, particularly when scripts are heavily customized or do not follow common PSADT structures. AI-assisted analysis improves accuracy in identifying the primary installer and its surrounding MARK logic, enabling more applications to be migrated successfully.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>**AI usage is optional** and can be **disabled at any time** from the Cloud Portal settings. See  [Manage Cloud AI Usage](../../manage/settings/company-settings/ai-usage.md) for more information.</p>
</blockquote>

## Migration Behavior of PSADT-based Apps

When the application is migrated, **PatchMyPC-ScriptRunner.exe** becomes the primary installer and orchestrates execution of the pre-install script, main installer, and post-install script. This model preserves the original installation behavior whilst enabling PMPC–specific enhancements that would not be possible with a simple “lift and shift” migration.

In the example below, the Rainbow application has been identified as PSADT-based, and the PSADT script has been automatically split during the migration flow. Logic originally contained within the **MARK: Pre-Install** section of the PSADT script has been mapped to the Pre-install script.

![PSADT script automatically split during the migration flow](/_images/image-(3828).png "PSADT script automatically split during the migration flow")

In the original PSADT script for Rainbow, both the **MARK: Pre-Install** and **MARK: Install** sections contain executable actions.

![Original PSADT script](/_images/image-(3830).png "Original PSADT script")

The pre-install section runs a prerequisite installer (**vstor\_redist.exe**), whilst the install section performs the primary application installation (**Rainbow\_Installer\_Machine\_Offline.msi**). During migration, these sections are analyzed and separated so that prerequisite logic is mapped to the **Pre-install** script, and the primary installer is executed as the main install action, preserving the original execution order.

You can edit any generated Pre-install and Post-install scripts to review whether PMPC Cloud has correctly identified the **MARK: Pre-Install**, **MARK: Install**, and **MARK: Post-Install** execution order.

![PSADT script editing in the migration flow](/_images/image-(3827).png "PSADT script editing in the migration flow")

<blockquote class="wp-block-quote">
<p>**Important**\</p>
<p>Because the original PSADT script is split into separate Pre-install and Post-install scripts during migration, any existing code signature is invalidated. If script signing is required in your environment, export the generated script blocks, re-sign them, and then re-import them before completing the migration.</p>
<p>Also, you need to ensure .NET version 4.7.2 is installed on any devices to which this app will be deployed.</p>
</blockquote>

## Preserved Properties of PSADT-based Apps

The following information indicates the properties that are carried forward from the ConfigMgr application to the migration deployment flow when the application is matched to:

* [PMPC Catalog App](migrate-psadt-based-apps.md#pmpc-catalog-app-properties-preserved)
* [PMPC Custom App](migrate-psadt-based-apps.md#pmpc-custom-app-properties-preserved)

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [How Migration Type is Determined](../how-migration-type-determined.md) to understand how ConfigMgr applications are matched during migration.</p>
</blockquote>

### PMPC Catalog App Properties Preserved

* Source Files (the main installer file will be replaced with the current version of the matched application in the Patch My PC catalog)
* DisplayName
* Return Codes
* Vendor
* Description
* Information URL
* Privacy URL
* PSADT Script&#x20;
  * "MARK: Pre-Install" mapped to Pre-install Script
  * "MARK: Post-Install" mapped to Post-Install Script

<blockquote class="wp-block-quote">
<p>**Note**\</p>
<p>If more than one action is detected in a MARK install section, additional actions are reassigned to the **MARK: Pre-Install** or **MARK: Post-Install** scripts, as only one action can run in the main install stage.</p>
</blockquote>

### PMPC Custom App Properties Preserved

* Source Files
* DisplayName
* Vendor
* Description
* Version
* Return Codes
* Information URL
* Privacy URL
* PSADT Script
  * "MARK: Pre-Install" mapped to Pre-install Script
  * "MARK: Post-Install" mapped to Post-Install Script

<blockquote class="wp-block-quote">
<p>**Note**\</p>
<p>If more than one action is detected in a MARK install section, additional actions are reassigned to the **MARK: Pre-Install** or **MARK: Post-Install** scripts, as only one action can run in the main install stage.</p>
</blockquote>

* Detection Rules
# Migrate MSI-based Applications from ConfigMgr to Intune using Patch My PC Cloud App Migration

_Applies to: Patch My PC Cloud_

When applications are inventoried from Microsoft Configuration Manager (ConfigMgr), Patch My PC (PMPC) Cloud analyzes each application's metadata to determine how it is installed and should be migrated. As part of this process, the installation command line is evaluated, and the primary installer file is identified from the application’s content source folder.

## Identifying an MSI-based App

ConfigMgr does not explicitly label an application as MSI-based. In most cases, the easiest way to confirm an application is MSI-based is to select the application from the Migration dashboard and review the Installation Program field.&#x20;

If the **Installation Program** contains both **msiexec** and a reference to a **.msi** file, the application can be considered MSI-based.

![MSI-based app identified from the installation program](/_images/image-(3819).png "MSI-based app identified from the installation program")

During the migration deployment flow, the **Installer Type** field also indicates when an application is being treated as MSI-based.

![MSI-based app shown in the deployment flow](/_images/image-(3820).png "MSI-based app shown in the deployment flow")

If an application is identified as MSI-based, as much existing metadata as possible is captured to support migration, drawing from both the ConfigMgr application and the MSI properties table.&#x20;

This includes analyzing the following to help ensure the application behaves the same way after it is migrated to Intune:

* installation command line
* primary installer file
* conflicting processes
* any supporting content.

## Migration Behavior of MSI-based Apps

The information analyzed is used to determine how the application is migrated and how the installation is executed. All supporting files in the original content source folder are included in the migration.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The only exception is the primary installer itself. When an application is migrated as a PMPC Catalog App, the original installer and version are replaced with the latest version available in the PMPC catalog. When migrating as a PMPC Custom App, the original installer and version are retained and used.</p>
</blockquote>

MSI properties (**PROPERTY=value**) are preserved and applied to the created deployment.

Detection rules are carried across during migration; however, the default PMPC detection rule (which detects applications based on the MSI product code) is enabled by default in the migration flow. If required, this can be changed to **Use Custom** on the **Detection Rules** tab to use the detection rules defined in ConfigMgr instead.

When the application is migrated, **PatchMyPC-ScriptRunner.exe** becomes the new primary installer and invokes the original MSI. This approach preserves the original installation behavior whilst enabling the deployment to leverage additional Patch My PC customizations that would be unavailable with a "lift and shift" migration.

## Preserved Properties of MSI-based Apps

The following information indicates the properties that are carried forward from the ConfigMgr application to the migration deployment flow when the application is either matched to a PMPC Catalog App or a PMPC Custom App.&#x20;

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [How Migration Type is Determined](../how-migration-type-determined.md) to understand how ConfigMgr applications are matched during migration.</p>
</blockquote>

### PMPC Catalog App Properties Preserved

* Source Files (the main MSI-based installer will be replaced with the current version of the matched application in the Patch My PC catalog)
* DisplayName
* MSI Properties (not visible in the Deployment created, but are present in the app metadata)
* Return Codes
* Vendor
* Description
* Information URL
* Privacy URL.

### PMPC Custom App Properties Preserved

* Source Files&#x20;
* DisplayName
* Vendor
* Description
* Version
* MSI Properties
* Installer Type
* Return Codes
* Information URL
* Privacy URL.
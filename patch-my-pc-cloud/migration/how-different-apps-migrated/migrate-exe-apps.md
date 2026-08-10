# Migrate EXE-based Applications from ConfigMgr to Intune using Patch My PC Cloud App Migration

_Applies to: Patch My PC Cloud_

When applications are inventoried from Microsoft Configuration Manager (ConfigMgr), Patch My PC (PMPC) Cloud analyzes the application metadata to determine how the application is installed and how it should be migrated. As part of this process, the installation command line is evaluated, and the primary installer file is identified from the application’s content source folder.

## Identifying an EXE-based App

ConfigMgr does not explicitly label an application as EXE-based. In most cases, the easiest way to confirm an application is EXE-based is to select the application from the Migration dashboard and review the **Installation Program** field.

![EXE-based app identified from the installation program](/_images/image-(317).png)

If the **Installation Program** references an **.exe** file, the application can be considered EXE-based.

> \*\*Note\*\*
>
> When evaluating EXE-based applications, references to helper executables such as \*\*msiexec.exe\*\*, \*\*powershell.exe\*\*, and the PowerShell App Deployment Toolkit (PSADT) are not classified as EXE-based installers; instead, they are treated as \[MSI-based]\(migrate-msi-apps.md), \[Script-based]\(migrate-script-apps.md), or \[PSADT-based]\(migrate-psadt-based-apps.md).

During the migration deployment flow, the **Installer Type** field also indicates when an application is being treated as EXE-based.

![EXE-based app shown in the deployment flow](/_images/image-(318).png)

If the application is identified as EXE-based, as much of the existing metadata as possible is captured to support migration. This includes analyzing the install command line, the main installer file, and any supporting content to ensure the application behaves the same way after migration to Intune.

## Migration Behavior of EXE-based Apps

The information analyzed is used to determine how the application is migrated and how the installation is executed. Any custom command-line arguments defined in ConfigMgr are preserved, and all supporting files in the original content source folder are included in the migration.

> \*\*Note\*\*
>
> The only exception is the primary installer itself. When an application is migrated as a PMPC Catalog App, the original installer and version are replaced with the latest version available in the PMPC catalog. When migrating as a PMPC Custom App, the original installer and version are retained and used.

When the application is migrated, **PatchMyPC-ScriptRunner.exe** becomes the new primary installer and invokes the original EXE with the existing command-line arguments. This approach preserves the original installation behavior whilst allowing the deployment to leverage additional PMPC customizations that would not be available with a "lift and shift" migration.

In the following, an older version of Notepad++ has been matched to a PMPC Catalog App. The original ConfigMgr application included an additional command-line argument, **/noupdater**, which has been preserved and carried through into the migration flow to ensure the application is deployed with the same installation behavior.

![](/_images/image-(319).png)

## Preserved Properties of EXE-based Apps

This section details the properties that are carried forward from the ConfigMgr application to the migration deployment flow when the application is either matched to:

* [PMPC Catalog App](migrate-exe-apps.md#pmpc-catalog-app-properties-preserved)
* [PMPC Custom App](migrate-exe-apps.md#pmpc-custom-app-properties-preserved)

> \*\*Note\*\*
>
> See \[How Migration Type is Determined]\(../how-migration-type-determined.md) to understand how ConfigMgr applications are matched during migration.

### PMPC Catalog App Properties Preserved

* Source Files (the main EXE-based installer will be replaced with the current version of the matched application in the Patch My PC catalog)
* DisplayName
* Additional Arguments
* Return Codes
* Vendor
* Description
* Information URL
* Privacy URL

### PMPC Custom App Properties Preserved

* Source Files
* DisplayName
* Vendor
* Description
* Version
* Silent Install Parameters
* Installer Type
* Additional Arguments
* Return Codes
* Information URL
* Privacy URL
* Detection Rules
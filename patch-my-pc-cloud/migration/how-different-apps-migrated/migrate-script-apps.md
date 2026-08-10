# Migrate Script-based Applications from ConfigMgr to Intune using Patch My PC Cloud App Migration

_Applies to: Patch My PC Cloud_

> \*\*Note\*\*
>
> Support for Script-based apps is still in development and is expected to be available soon.

When applications are inventoried from Microsoft Configuration Manager (ConfigMgr), Patch My PC (PMPC) Cloud analyzes the application metadata to determine how the application is installed and should be migrated. As part of this process, the installation command line is evaluated, and the primary installer file is identified from the application’s content source folder.

## Identifying a Script-based App

ConfigMgr does not explicitly label an application as Script-based. In most cases, the easiest way to confirm that an application is Script-based is to select the application from the Migration dashboard and review the **Installation Program** field.

If the **Installation Program** contains a **.ps1, .cmd, .bat** or **.vbs** file reference, the application can be considered Script-based.

![Script-based app identified from the installation program](/_images/image-(3824).png)

During the migration deployment flow, the **File** tab also indicates when an application is being treated as Script-based, and the script content is displayed.

![Script-based app shown in the deployment flow](/_images/image-(3822).png)

If the application is identified as Script-based, as much of the existing metadata as possible is captured to support migration. This includes any supporting content to ensure the application behaves the same way after migration to Intune.

## Migration Behavior of Script-based Apps

Script-based apps can only be migrated as PMPC Custom Apps.

When the application is migrated, **PatchMyPC-ScriptRunner.exe** becomes the new primary installer and invokes the original script defined in the installation command line. This approach preserves the original installation behavior whilst allowing the deployment to leverage additional PMPC customizations that would be unavailable with a "lift and shift" migration.

In the example below, a PowerShell-based Windows Update script is being migrated. The installation script content is displayed inline within the migration flow, allowing it to be reviewed or edited before proceeding. The script is currently not code-signed, as indicated by the warning below the editor. The script can be exported for signing and then re-imported, or migrated "as-is," depending on your organization’s script-signing requirements.

![Script-based app flow](/_images/image-(3823).png)

> \*\*Important\*\*
>
> If the script is code-signed, any modification on the \*\*File\*\* tab will invalidate the existing signature. For this reason, editing should only be performed on unsigned scripts. Signed scripts should be exported, re-signed after any changes, and then re-imported before completing the migration.

## Preserved Properties of Script-based Apps

The following information indicates the properties that are carried forward from the ConfigMgr application to the migration deployment flow when the application is migrated as a PMPC Custom App:

* Source Files
* DisplayName
* Vendor
* Description
* Version
* Return Codes
* Information URL
* Privacy URL
* Detection Rules.
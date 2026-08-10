# "Unsupported" Reasons for ConfigMgr to Intune App Migration using Patch My PC Cloud

_Applies to: Patch My PC Cloud_

In most cases, Microsoft Configuration Manager (ConfigMgr) applications cannot be migrated to Patch My PC (PMPC) Cloud because the Publisher, running in the **SYSTEM** context, cannot access or correctly interpret the application’s content source.

The most common reasons are:

* The Publisher does not have SMB or NTFS access to the directory specified in the **Content location** field on the **Content** tab of the ConfigMgr deployment type.
* The **Content location** directory specified on the **Content** tab of the ConfigMgr deployment type is empty.
* The installer referenced in the **Installation program** field of the ConfigMgr deployment type cannot be found.
* The application content source contains more than 1,000 files.

These issues account for most unsupported applications.

Less common reasons may still apply and are surfaced directly in the [Migration Dashboard](../about-migration-dashboard.md).

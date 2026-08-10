# WSUS Maintenance section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **WSUS Maintenance** section in Patch My PC (PMPC) Publisher provides options to help manage and clean up third party update content stored in WSUS. These options are designed to reduce disk usage, remove unused content, and prevent long term WSUS performance and stability issues caused by accumulated third party updates.

These actions cannot be triggered manually, if enabled, they are performed at the end of a publishing sync cycle.

![WSUS Maintenance Options](../../../../.gitbook/assets/image-\(92\).png)

## Show unreferenced WSUS folders

This option scans the WSUS content directory and identifies folders that are no longer referenced by any updates in the WSUS database.

Unreferenced folders typically occur when updates are declined, expired, or deleted, but the associated content was not removed. Reviewing these folders helps identify orphaned content that can be safely cleaned up.

When the **Show unreferenced WSUS folders...** button is clicked, a window opens displaying content that can be safely cleaned up (deleted).

The results displayed are identifiable by the following fields:

<table><thead><tr><th width="110.88897705078125" valign="top">Column</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">Selected</td><td valign="top">Indicates whether the folder is selected for deletion. Selected folders will be removed when <strong>Delete selected</strong> is chosen.</td></tr><tr><td valign="top">Path</td><td valign="top">The full path to the unreferenced WSUS folder.</td></tr><tr><td valign="top">File</td><td valign="top">An example file found within the unreferenced folder. This helps identify the type of content stored in the folder. There may be more files but only a single file is listed.</td></tr><tr><td valign="top">Folder Size</td><td valign="top">The total disk space consumed by the unreferenced folder. This helps assess the potential storage savings before deleting the folder.</td></tr></tbody></table>

In the example below, a single, unreferenced folder, was found in the UpdateServicesPackages folder. This is the folder where third-party updates are initially staged before being compressed to a CAB file, signed, and then finally copied to the WSUS Content folder.

![Unreferenced WSUS Folders](../../../../.gitbook/assets/image-\(73\).png)

The **Delete selected** action permanently removes the selected unreferenced folders from the WSUS content directory.

Use this option to safely reclaim disk space after reviewing the list of unreferenced folders and confirming they are no longer needed.

## Enable automatic deletion and cleanup of the UpdateServicesPackages folder

> \*\*Tip\*\*
>
> By default, \*\*Enable automatic deletion and cleanup of the UpdateServicesPackages folder\*\* is enabled.

When enabled, the Publisher automatically removes WSUS content associated with declined or deleted third party updates.

This cleanup runs at the end of a successful Publisher synchronization. The process performs two actions. First, it deletes content for declined third party updates. Second, it removes any unreferenced folders from the UpdateServicesPackages directory that are no longer associated with update metadata.

This option helps prevent long term WSUS content growth and reduces disk usage without requiring manual cleanup.

### Only delete declined Patch My PC third party updates

> \*\*Tip\*\*
>
> By default, \*\*Only delete declined Patch My PC third party updates\*\* is enabled.

When enabled, automatic cleanup is limited to updates published by Patch My PC. Content from other third party catalogs such as Ivanti, Dell, HP, or Lenovo is not removed, even if those updates are declined.

If this option is unchecked, the cleanup process also applies to declined third party updates from other vendors. This can be useful in environments where multiple catalogs have been used historically and broad cleanup is required.

## Automatically run the Unneeded update files cleanup action

When **Automatically run the Unneeded update files clean action in the WSUS Server Cleanup Wizard** is enabled, the Publisher automatically runs the WSUS Server Cleanup Wizard action that removes unneeded update files.

This action helps clean up unused content in the WSUS content directory and complements the UpdateServicesPackages cleanup by removing additional unused files managed by WSUS.

> \*\*Important\*\*
>
> If you have downstream WSUS servers that do not share the same SUSDB, you should give careful consideration to enabling this automatic deletion and cleanup. In WSUS hierarchies, cleanup should be performed from the bottom up to avoid removing content that downstream servers still require.

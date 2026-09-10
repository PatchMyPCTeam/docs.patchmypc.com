# WSUS Maintenance section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **WSUS Maintenance** section on the **WSUS Options** tab of Patch My PC (PMPC) Publisher provides options to help manage and clean up third party update content stored in WSUS.&#x20;

<figure><img src="../../../../.gitbook/assets/image (1043).png" alt="&#x27;WSUS Maintenance&#x27; section" width="563"><figcaption></figcaption></figure>

These options are designed to reduce disk usage, remove unused content, and prevent long-term WSUS performance and stability issues caused by accumulated third party updates.

These actions cannot be triggered manually. If enabled, they run at the end of a publishing sync cycle.

## Show Unreferenced WSUS Folders

Unreferenced folders typically occur when updates are declined, expire, or are deleted, but the associated content is not removed. Reviewing these folders helps identify orphaned content you can safely clean up.

Clicking the **Show Unreferenced WSUS Folders** button triggers the scanning of the WSUS content directory and identifies folders that are no longer referenced by any updates in the WSUS database, with the results being shown on the **Unreferenced WSUS Folders** screen.

<figure><img src="../../../../.gitbook/assets/image (1044).png" alt="&#x27;Unreferenced WSUS Folders&#x27; screen" width="563"><figcaption></figcaption></figure>

The following fields are shown for any items that are found.

<table><thead><tr><th width="110.88897705078125" valign="top">Column</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">Selected</td><td valign="top">Indicates whether the folder is selected for deletion. Selected folders will be removed when <strong>Delete selected</strong> is chosen.</td></tr><tr><td valign="top">Path</td><td valign="top">The full path to the unreferenced WSUS folder.</td></tr><tr><td valign="top">File</td><td valign="top">An example file found within the unreferenced folder. This helps identify the type of content stored in the folder. There may be more files, but only a single file is listed.</td></tr><tr><td valign="top">Folder Size</td><td valign="top">The total disk space consumed by the unreferenced folder. This helps assess the potential storage savings before deleting the folder.</td></tr></tbody></table>

In the example below, a single, unreferenced folder was found in the **UpdateServicesPackages** folder. This is the folder where third-party updates are initially staged before being compressed to a CAB file, signed, and then finally copied to the WSUS Content folder.

<figure><img src="../../../../.gitbook/assets/image (73).png" alt="Unreferenced WSUS Folders" width="563"><figcaption></figcaption></figure>

Clicking **Delete Selected** permanently removes the selected unreferenced folders from the WSUS content directory.

Use this option to safely reclaim disk space after reviewing the list of unreferenced folders and confirming they are no longer needed.

## Enable the automatic deletion and cleanup of the UpdateServicesPackages folder for declined third-party-updates

When the **Enable the automatic deletion and cleanup of the UpdateServicesPackages folder for declined third-party-updates** checkbox is checked (which it is by default), Publisher automatically removes WSUS content associated with declined or deleted third party updates.

This cleanup runs after a successful Publisher synchronization. The process performs two actions:

* First, it deletes content for declined third party updates.
* Second, it removes any unreferenced folders from the **UpdateServicesPackages** directory that are no longer associated with update metadata.

This option helps prevent long-term WSUS content growth and reduces disk usage without requiring manual cleanup.

### Only delete declined Patch My PC third-party updates

When the **Only delete declined Patch My PC third-party updates** checkbox is checked (which it is by default), automatic cleanup is limited to updates published by Patch My PC. Content from other third party catalogs such as Ivanti, Dell, HP, or Lenovo is not removed, even if those updates are declined.

If this option is unchecked, the cleanup process also applies to declined third party updates from other vendors. This can be useful in environments where multiple catalogs have been used historically, and broad cleanup is required.

## Automatically run the Unneeded updates files cleanup action in the WSUS Cleanup Wizard

Checking the **Automatically run the Unneeded updates files cleanup action in the WSUS Cleanup Wizard** checkbox (which isn't checked by default) causes Publisher to automatically run the WSUS Server Cleanup Wizard action that removes unneeded update files.

This action helps clean up unused content in the WSUS content directory and complements the UpdateServicesPackages cleanup by removing additional unused files managed by WSUS.

{% hint style="danger" %}
**Important**

If you have downstream WSUS servers that do not share the same SUSDB, carefully consider enabling this automatic deletion and cleanup. In WSUS hierarchies, perform cleanup from the bottom up to avoid removing content that downstream servers need.
{% endhint %}

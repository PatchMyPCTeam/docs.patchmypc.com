# WSUS Maintenance

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **WSUS Maintenance** section provides options to help manage and clean up third party update content stored in WSUS. These options are designed to reduce disk usage, remove unused content, and prevent long term WSUS performance and stability issues caused by accumulated third party updates.

These actions cannot be triggered manually, if enabled, they are performed at the end of a publishing sync cycle.

<figure><img src="../../../../.gitbook/assets/image (92).png" alt="WSUS Maintenance Options" width="563"><figcaption></figcaption></figure>

## Show unreferenced WSUS folders

This option scans the WSUS content directory and identifies folders that are no longer referenced by any updates in the WSUS database.

Unreferenced folders typically occur when updates are declined, expired, or deleted, but the associated content was not removed. Reviewing these folders helps identify orphaned content that can be safely cleaned up.

When the **Show unreferenced WSUS folders...** button is clicked, a window opens displaying content that can be safely cleaned up (deleted).

The results displayed are identifiable by the following fields:

| Column      | Description                                                                                                                                                                   |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Selected    | Indicates whether the folder is selected for deletion. Selected folders will be removed when **Delete selected** is chosen.                                                   |
| Path        | The full path to the unreferenced WSUS folder.                                                                                                                                |
| File        | An example file found within the unreferenced folder. This helps identify the type of content stored in the folder. There may be more files but only a single file is listed. |
| Folder Size | The total disk space consumed by the unreferenced folder. This helps assess the potential storage savings before deleting the folder.                                         |

In the example below, a single, unreferenced folder, was found in the UpdateServicesPackages folder. This is the folder where third-party updates are initially staged before being compressed to a CAB file, signed, and then finally copied to the WSUS Content folder.

<figure><img src="../../../../.gitbook/assets/image (73).png" alt="Unreferenced WSUS Folders" width="563"><figcaption></figcaption></figure>

The **Delete selected** action permanently removes the selected unreferenced folders from the WSUS content directory.

Use this option to safely reclaim disk space after reviewing the list of unreferenced folders and confirming they are no longer needed.

## Enable automatic deletion and cleanup of the UpdateServicesPackages folder

{% hint style="success" %}
**Tip**

By default, **Enable automatic deletion and cleanup of the UpdateServicesPackages folder** is enabled.&#x20;
{% endhint %}

When enabled, the Publisher automatically removes WSUS content associated with declined or deleted third party updates.

This cleanup runs at the end of a successful Publisher synchronization. The process performs two actions. First, it deletes content for declined third party updates. Second, it removes any unreferenced folders from the UpdateServicesPackages directory that are no longer associated with update metadata.

This option helps prevent long term WSUS content growth and reduces disk usage without requiring manual cleanup.

### Only delete declined Patch My PC third party updates

{% hint style="success" %}
**Tip**

By default, **Only delete declined Patch My PC third party updates** is enabled.
{% endhint %}

When enabled, automatic cleanup is limited to updates published by Patch My PC. Content from other third party catalogs such as Ivanti, Dell, HP, or Lenovo is not removed, even if those updates are declined.

If this option is unchecked, the cleanup process also applies to declined third party updates from other vendors. This can be useful in environments where multiple catalogs have been used historically and broad cleanup is required.

## Automatically run the Unneeded update files cleanup action

When **Automatically run the Unneeded update files clean action in the WSUS Server Cleanup Wizard** is enabled, the Publisher automatically runs the WSUS Server Cleanup Wizard action that removes unneeded update files.

This action helps clean up unused content in the WSUS content directory and complements the UpdateServicesPackages cleanup by removing additional unused files managed by WSUS.

{% hint style="warning" %}
**Important**

If you have downstream WSUS servers that do not share the same SUSDB, you should give careful consideration to enabling this automatic deletion and cleanup. In WSUS hierarchies, cleanup should be performed from the bottom up to avoid removing content that downstream servers still require.
{% endhint %}

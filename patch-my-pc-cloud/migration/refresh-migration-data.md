# Refresh ConfigMgr to Intune App Migration Data in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

The Patch My PC (PMPC) Cloud Migration dashboard includes the following options:

* [Refresh](refresh-migration-data.md#refresh)
* [Full Resync](refresh-migration-data.md#full-resync)

> \*\*Note\*\*
>
> See the \[Troubleshooting ]\(refresh-migration-data.md#troubleshooting)section below for troubleshooting tips.

## Refresh

The **Refresh** option is available directly from the dashboard toolbar.

![Refresh migration data](../../.gitbook/assets/image-\(25\).png)

Clicking **Refresh** triggers an immediate delta sync from Publisher to PMPC Cloud, bypassing the normal scheduled sync interval configured in Publisher (60 minutes by default). This is useful when new applications or recent changes are available in Publisher, and you want them reflected in Cloud as soon as possible.

A refresh only processes incremental changes and does not rebuild existing migration metadata.

## Full Resync

The **Full Resync** option is accessed by clicking the ellipsis beside the **Refresh** option.

![Full resync of migration data](../../.gitbook/assets/image-\(322\).png)

Clicking **Full Resync** clears all migration metadata in both Cloud and the Publisher, then rebuilds it from scratch using the latest migration logic in PMPC Cloud. Non-migrated applications are removed and reimported, while migrated applications remain unchanged.

This option is intended for scenarios where migration metadata is missing, incomplete, or corrupted, such as missing file access or invalid values like a file size of zero, and where the issue cannot be resolved through normal application revision updates.

Because a full resync re-evaluates all applications, the process may take some time and cannot be cancelled midway through.

## Troubleshooting

If the **Refresh** or **Full Resync** options are unavailable, it means PMPC Cloud has lost connectivity to the Publisher.

![Lost connection to the Publisher](../../.gitbook/assets/image-\(314\).png)

To restore the connection, open the Publisher console, go to the **About** tab, and select **Restart Service**, which will re-establish communication with your PMPC Cloud company.

![Restart the Publisher service to restore the connection](../../.gitbook/assets/image-\(315\).png)

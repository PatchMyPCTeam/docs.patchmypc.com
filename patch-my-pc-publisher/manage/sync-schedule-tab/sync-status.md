# Sync Status section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Sync Status** section on the **Sync Schedule** tab of the Patch My PC (PMPC) Publisher displays the current state of a Publisher synchronization and also allows you to manually [run a Publishing sync.](sync-status.md#run-publishing-service-sync)

## Status

The **Status** field updates in real time as products are evaluated and processed.

<table><thead><tr><th width="121.77783203125" valign="top">Status</th><th valign="top">Means Publisher...</th></tr></thead><tbody><tr><td valign="top">Idle</td><td valign="top">Is idle and not actively evaluating or publishing content.</td></tr><tr><td valign="top">Syncing</td><td valign="top"><p>Is actively syncing. The status bar displays the current operation, which includes the product name and version currently being evaluated or published.</p><p>As the sync runs, the status updates for each product processed. This provides visibility into which updates or applications are being evaluated at that moment and confirms that the publishing service is actively working through the configured selections.</p><p>This status is particularly useful during large publishing synchronizations, as it confirms ongoing progress and helps identify where Publisher is in the evaluation or publishing process.</p></td></tr><tr><td valign="top">Completed</td><td valign="top">Has completed successfully. The <strong>Sync completed at &#x3C;</strong><em><strong>date_time</strong></em><strong>></strong> message is displayed under the <strong>Status</strong> field.</td></tr><tr><td valign="top">Error</td><td valign="top">Has encountered an error when trying to run a synchronization.</td></tr></tbody></table>

## Run Publishing Service Sync

What happens when you click **Run Publishing Service Sync** depends on whether one or more products have been marked for a Selective Sync using the [Publish Now](../../customizations/list-customizations/publish-now.md) right-click option:

* If a product(s) has been marked for a Selective Sync, then a [Selective Sync](sync-status.md#selective-sync) is run.
* If no product(s) has been marked for a Selective Sync, then a [Full Sync](sync-status.md#full-sync) is run.

### Selective Sync

If you have used the [Publish Now](../../customizations/list-customizations/publish-now.md) right-click option to selectively publish one or more specific products, when you click **Run Publishing Service Sync**, Publisher displays the **Products for Selective Sync** dialog box listing of all products currently marked for Selective Sync.

!['Products for Selective Sync' dialog box](/_images/image-(4780).png)

If you click **OK**, the **Selective Sync Successful** dialog box is displayed stating that the sync command has been sent to the Publisher service to run the sync.

!['Selective Sync Successful' dialog box](/_images/image-(4781).png)

If you click **Cancel**, the **Selective Sync canceled** dialog box is displayed asking you how you want to proceed:

* Clicking **Yes** clears all Selective Sync flags and immediately runs a normal full publishing service sync. All enabled products across all platforms will be evaluated and processed.
* Clicking **No** keeps the existing Selective Sync flags in place and returns you to the main Publisher window without running a sync. This allows you to modify the current Selective Sync selections or run a manual sync later using the same selected products.

!['Selective Sync cancelled' dialog](/_images/image-(4445).png)

### Full Sync

If you have not used the [Publish Now](../../customizations/list-customizations/publish-now.md) right-click option to selectively publish one or more specific products, when you click **Run Publishing Service Sync**, Publisher will run a Full Sync, which performs the same evaluation as a scheduled sync.

Publisher will download the latest version of the Patch My PC catalog and evaluate all configured product selections, customizations, and global options to determine which apps and updates should be published.

To run a Full Sync:

1. Navigate to the **Sync Schedule** tab and click **Run Publishing Service Sync**

![Navigating to the 'Sync Schedule' tab and clicking 'Run Publishing Service Sync'](/_images/image-(4779).png)

2. On the **Run Publishing Service Sync** dialog box, read the message and click **Yes** if you want to proceed or **No** to cancel.

!['Run Publishing Service Sync' dialog box](/_images/image-(4782).png)

The **Run Now Successful** dialog box is displayed stating that the sync command has been sent to the Publisher service to run the sync.

!['Run Now Successful' dialog box](/_images/image-(4784).png)

After a period of time, the **Status** field under the **Sync Status** section will change to **Syncing** to show the sync is in progress.

![](/_images/image-(4785).png)

Once the sync has completed, the **Status** field changes to **Completed** as detailed at the top of this article.
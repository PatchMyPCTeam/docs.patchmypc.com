# Refresh Patch My PC Cloud Discovery Data

_Applies to: Patch My PC Cloud_

By default, you have to wait a week for the discovery data in your Patch My PC (PMPC) Cloud portal to refresh. Rather than waiting up to a week you can refresh the data in the Discovery node every 24 hours to pick up any changes.

To manually refresh the data in the **Discovery** node:

1. Navigate to the **Discovery** node.
2.  If the **Refresh Data** button is available, click it and go to Step 4.<br>

    !["Refresh Data" button available](../../.gitbook/assets/image-\(1096\).png)
3. If the **Refresh Data** button is unavailable, note the value of the **Last Sync** time.\
   \
   If it has been less than 24 hours since discovery last ran successfully, the **Refresh Data** button will be unavailable. Once 24 hours have passed, the **Refresh Data** button will be available.

> \*\*Note\*\*
>
> The \*\*Last Sync\*\* time is the time when the last sync completed successfully, which is then converted to your local browser time and shown to you in the UI.

4.  The **Refresh Data** button changes to **Collecting Data** whilst discovery runs.<br>

    !["Refresh Data" button changed to "Collecting Data" whilst discovery runs](../../.gitbook/assets/image-\(1097\).png)
5. Currently, when the discovery process completes the portal does not auto-refresh. So periodically press **F5** to refresh the portal.
6.  Once discovery finishes running, the **Last Sync** time gets updated and the **Refresh Data** button becomes unavailable.<br>

    !["Last Sync" time updated and "Refresh data" unavailable](../../.gitbook/assets/image-\(1098\).png)

> \*\*Tip\*\*
>
> If you look in the \*\*Events\*\* node, you will see the \*\*Intune Discovered Applications Refreshed\*\* event which is created whenever someone clicks \*\*Refresh Data\*\* to refresh your discovery data.

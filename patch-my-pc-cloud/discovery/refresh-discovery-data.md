# Refresh Patch My PC Cloud Discovery Data

_Applies to: Patch My PC Cloud_

By default, you have to wait a week for the discovery data in your Patch My PC (PMPC) Cloud portal to refresh. Rather than waiting up to a week you can refresh the data in the Discovery node every 24 hours to pick up any changes.

To manually refresh the data in the **Discovery** node:

1. Navigate to the **Discovery** node.
2.  If the **Refresh Data** button is available, click it and go to Step 4.<br>

    <figure><img src="../../.gitbook/assets/image-(394).png" alt="“Refresh Data” button available" width="563"><figcaption></figcaption></figure>
3. If the **Refresh Data** button is unavailable, note the value of the **Last Sync** time.\
   \
   If it has been less than 24 hours since discovery last ran successfully, the **Refresh Data** button will be unavailable. Once 24 hours have passed, the **Refresh Data** button will be available.

{% hint style="info" %}
**Note**

The **Last Sync** time is the time when the last sync completed successfully, which is then converted to your local browser time and shown to you in the UI.
{% endhint %}

4.  The **Refresh Data** button changes to **Collecting Data** whilst discovery runs.<br>

    <figure><img src="../../.gitbook/assets/image-(395).png" alt="“Refresh Data” button changed to “Collecting Data” whilst discovery runs" width="563"><figcaption></figcaption></figure>
5. Currently, when the discovery process completes the portal does not auto-refresh. So periodically press **F5** to refresh the portal.
6.  Once discovery finishes running, the **Last Sync** time gets updated and the **Refresh Data** button becomes unavailable.<br>

    <figure><img src="../../.gitbook/assets/image-(396).png" alt="“Last Sync” time updated and “Refresh data” unavailable" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

If you look in the **Events** node, you will see the **Intune Discovered Applications Refreshed** event which is created whenever someone clicks **Refresh Data** to refresh your discovery data.
{% endhint %}

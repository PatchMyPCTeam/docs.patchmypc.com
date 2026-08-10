# Overview of Discovery in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

The _Discovery_ feature of Patch My PC (PMPC) Cloud allows you to see which apps in our App Catalog are installed in your environment, including any Binary Free Apps or Custom Apps you may have added.

Once an app has been discovered, you can decide whether to manage it using PMPC Cloud.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Discovered Apps are only inventoried on devices marked as **Corporate** in Intune. Devices marked as **Personal** will not send application inventory to Intune. For more information, see <a href="https://learn.microsoft.com/en-us/intune/intune-service/enrollment/corporate-identifiers-add">Identify devices as corporate-owned</a>.</p>
</blockquote>

## How Discovery Works in Patch My PC Cloud

When you connect your PMPC Cloud Company to your Intune tenant, we retrieve the latest copy of Intune’s _discovered apps_ report, which contains an inventory of all installed apps on your devices.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See <a href="https://learn.microsoft.com/en-us/mem/intune/apps/app-discovered-apps">Intune discovered apps</a> for more information on the Intune weekly scan.</p>
</blockquote>

This report includes the following information about each app:

* Name
* Version
* Device count (how many devices the app is installed on)
* Vendor i.e. who publishes the app.

We then perform a mapping process of the report’s contents (based on the Intune app name and app version properties) to check if each app matches a publicly available app in our App Catalog or any Custom/Binary Free Apps you have uploaded.

If there is a match, the app is marked as either:

* **Unmanaged –** Apps identified as being in our App Catalog but aren’t currently managed by us as there is no matching deployment in our portal.
* **Managed –** Apps identified as being in our App Catalog and where there is a matching deployment in our portal created by either PMPC Cloud or our on-prem Publisher.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If an Intune app is discovered that maps to two different products from our App Catalog, if one of them is managed and the other is unmanaged, the managed app is displayed in the **Managed** tab and the unmanaged app is hidden in the **Unmanaged** tab.</p>
<p>Also, when our scan runs, no event is written to the Events node.</p>
</blockquote>

Any matching apps are shown on the relevant tab of the **Discovery** node.

![Populated "Discovery" node](/_images/image-(1117).png "Populated “Discovery” node")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you look in the **Events** node, you will see the **Intune Application Discovered** event which is created the first time Discovery is run in your PMPC Company.</p>
</blockquote>

## Subsequent Scans

Intune only updates its discovered apps report once a week. Because of this, PMPC Cloud will initially query Discovery data for your tenant once a week, randomly selecting a day between 1 AM and 5 AM based on the time zone of your PMPC company. All subsequent weekly updates will occur on the same day and time as the first discovery collection.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If you create a deployment for an **Unmanaged** app, you will only see it move to the **Managed** tab either:</p>
<p>* On the following Sunday (after the update scan runs)</p>
<p>* When you follow the [Refresh Discovery Data](refresh-discovery-data.md) process.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>When our query runs, no event is written to the **Events** node.</p>
<p>If you have any feedback or comments on our docs, please email [docs@patchmypc.com](mailto:docs@patchmypc.com).</p>
</blockquote>
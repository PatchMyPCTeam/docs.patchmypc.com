# Working with Patch My PC Advanced/Patch Insights for Intune Dashboards

_Applies to: Advanced/Patch Insights for Intune_

Using the Dashboards for Advanced/Patch Insights for Intune, you can:

* [Drilldown to display more detailed information](working-dashboards.md#drilldown-to-display-more-detailed-information)
* [Export data](working-dashboards.md#export-data)
* [Change to a different view of the data](working-dashboards.md#change-to-a-different-view-of-the-data)
* [Apply filters](working-dashboards.md#apply-filters)

## Drill down to display more detailed information

Whenever you click a Statistic or Chart, the device list modal opens, showing more detailed information.

![More detailed information table](/_images/image-(3795).png "More detailed information table")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You can also click the ellipsis for a chart and select **View Chart Data** to open the device list modal.</p>
</blockquote>

On the device list modal, you can:

* Control the number of items shown per page.
* Navigate between pages.
* Click a column heading to sort by that column.
* Search for a specific item.
* [Export data](working-dashboards.md#export-data)
* Potentially drilldown to display even more detailed information in some cases.

## Export data

To export data from a Statistic:

1. Click the relevant Statistic to open it.
2. Click the ellipsis (![ellipsis](/_images/8s-01I4NEiL4x1GK8BI5FxI-WCyVoxhXGnMboOzFwb898BhNoAwjowiowAAAAASUVORK5CYII "ellipsis"))in the top right-hand corner of the device list portal and select **Export <**_**device\_list\_modal\_name**_**>**

![Clicking the ellipsis and selecting Export](/_images/image-(3796).png "Clicking the ellipsis and selecting Export")

A **.csv** containing the export is downloaded and named **<**_**device\_list\_modal\_name**_**>.csv**

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The downloaded .csv file may contain additional columns and data beyond what is shown in the Dashboard.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you filter the results before exporting, the resulting .csv file contains the filtered results.</p>
</blockquote>

## Change to a different view of the data

Some Charts (such as **Device Specs**) include an action menu (![](/_images/2YYkqAAAAAElFTkSuQmCC)) that lets you switch the Chart between different views of the data.

To change the view of a Chart, click the action menu and select the desired view from the dropdown.







![Changing views](/_images/image-(3797).png "Changing views")

The Chart’s subheading updates to the selected view name, and the Chart itself updates to show the data in the requested view.

![Changed view](/_images/image-(3798).png "Changed view")

Also, when you click a Chart segment, the device list modal only displays the data for that segment. Likewise, if you switch to a different view and click a Chart segment, the device list modal displays only the data for the selected view and clicked segment.

## Apply filters

Some views include the ability to apply filters through toggles.

To apply a filter:

1. Navigate to the relevant Compliance view.
2. Click the relevant toggle to show the filtered items.

![Clicking a toggle to show the filtered items](/_images/image-(3799).png "Clicking a toggle to show the filtered items")

The view updates to display the previously filtered items.

![View updating to show the filtered items.](/_images/image-(3800).png "View updating to show the filtered items.")

Click the toggle again to re-apply the filter.
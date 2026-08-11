# Working with Patch My PC Advanced/Patch Insights for Intune Dashboards

_Applies to: Advanced/Patch Insights for Intune_

Using the Dashboards for Advanced/Patch Insights for Intune, you can:

* [Drilldown to display more detailed information](working-dashboards.md#drilldown-to-display-more-detailed-information)
* [Export data](working-dashboards.md#export-data)
* [Change to a different view of the data](working-dashboards.md#change-to-a-different-view-of-the-data)
* [Apply filters](working-dashboards.md#apply-filters)

## Drill down to display more detailed information

Whenever you click a Statistic or Chart, the device list modal opens, showing more detailed information.

<figure><img src="../../.gitbook/assets/image (3795).png" alt="More detailed information table" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

You can also click the ellipsis for a chart and select **View Chart Data** to open the device list modal.
{% endhint %}

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
2. Click the ellipsis (![ellipsis](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAAVCAMAAACXIvXeAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAA2UExURR4eLFhZbqSmxUBBUmJjequtzUlKXi8vQDk5S3d5kiQkM1xdckpLX3BxiVVWa0ZGWYiKpi8wQIfHbykAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAA2SURBVChTrcg3DgAgDACxUEKv//8s+01I4NEiL4x1GK8BI5FxI+WCyVoxhXGnMboOzFwb898BhNoAwjowiowAAAAASUVORK5CYII=))in the top right-hand corner of the device list portal and select **Export <**_**device\_list\_modal\_name**_**>**

<figure><img src="../../.gitbook/assets/image (3796).png" alt="Clicking the ellipsis and selecting Export" width="563"><figcaption></figcaption></figure>

A **.csv** containing the export is downloaded and named **<**_**device\_list\_modal\_name**_**>.csv**

{% hint style="info" %}
**Note**

The downloaded .csv file may contain additional columns and data beyond what is shown in the Dashboard.
{% endhint %}

{% hint style="success" %}
**Tip**

If you filter the results before exporting, the resulting .csv file contains the filtered results.
{% endhint %}

## Change to a different view of the data

Some Charts (such as **Device Specs**) include an action menu (![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAWCAMAAAAcqPc3AAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAABmUExURR4eLJGSrqutzXN0jScoN0RFV4+Qraiqy2lqgmVmfXh5koyNqU1OYT0+UDAwQUFBVCkpOKKjwoqMqIiJpZGTsISGoZGTryIiMT4+UR8fLV5fdklJXaqszEhJXF1edI2Pq25viFdYbaiGMgwAAAAJcEhZcwAADsQAAA7EAZUrDhsAAABeSURBVChTvc63FoAgEERRxLgmVMzZ//9JK3anoeVVnFsMq1SQIi3F4DrhZ5qB5wW5ygq8ZiZqwFsjdeD9YF3jBO77d/bcucj8uoHvPG/tAe67/7x4537AX9j5wIP3A/rcB3/2YYkqAAAAAElFTkSuQmCC)) that lets you switch the Chart between different views of the data.

To change the view of a Chart, click the action menu and select the desired view from the dropdown.







<figure><img src="../../.gitbook/assets/image (3797).png" alt="Changing views" width="563"><figcaption></figcaption></figure>

The Chart’s subheading updates to the selected view name, and the Chart itself updates to show the data in the requested view.

<figure><img src="../../.gitbook/assets/image (3798).png" alt="Changed view" width="563"><figcaption></figcaption></figure>

Also, when you click a Chart segment, the device list modal only displays the data for that segment. Likewise, if you switch to a different view and click a Chart segment, the device list modal displays only the data for the selected view and clicked segment.

## Apply filters

Some views include the ability to apply filters through toggles.

To apply a filter:

1. Navigate to the relevant Compliance view.
2. Click the relevant toggle to show the filtered items.

<figure><img src="../../.gitbook/assets/image (3799).png" alt="Clicking a toggle to show the filtered items" width="563"><figcaption></figcaption></figure>

The view updates to display the previously filtered items.

<figure><img src="../../.gitbook/assets/image (3800).png" alt="View updating to show the filtered items." width="563"><figcaption></figcaption></figure>

Click the toggle again to re-apply the filter.

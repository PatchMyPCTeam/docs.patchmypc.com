# "Hardware" Page of the Patch My PC Advanced/Patch Insights for Intune Dashboard

_Applies to: Advanced Insights for Intune_

> \*\*Note\*\*
>
> The \*\*Hardware\*\* page is only available in Advanced Insights for Intune, which requires an Enterprise Premium license.

Enhanced hardware inventory is another significant facet of Advanced Insights for Intune. The Patch My PC (PMPC) Client gathers inventory data across a range of inventory properties to improve visibility and management of your estate.

The _Hardware_ page of Advanced Insights for Intune shows key statistics from your environment and is split into the following sections:

* [Tabs](hardware-page.md#tabs)
* [Statistics](hardware-page.md#statistics)
* [Charts](hardware-page.md#charts)

> \*\*Note\*\*
>
> See \[About Advanced/Patch Insights for Intune Dashboards]\(./) and \[Working with Advanced/Patch Insights for Intune Dashboards]\(../working-dashboards.md) for more information.
>
> Also, only devices running the Patch My PC (PMPC) Client will appear on this page. See \[Manage the Patch My PC Client]\(../../manage/settings/client.md) for more details on deploying and managing the PMPC Client.

!['Hardware' page](../../../.gitbook/assets/image-\(4282\).png)

## Tabs

The _Tabs_ control lets you switch between different views of hardware data.

By default, the **General** tab is selected.

!['General' tab](../../../.gitbook/assets/image-\(4283\).png)

The layout of the views differs depending on the tab you select.

For example, clicking the **Network** tab shows a mix of Statistics, Charts, and data tables.

!['Network' tab](../../../.gitbook/assets/image-\(4284\).png)

As is standard, clicking an item displays more data that you can drill down into or show in a different view.

## Statistics

The top row of the Hardware page is called _Statistics_ and displays the following statistics.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows the number of…</th></tr></thead><tbody><tr><td valign="top">Clients deployed</td><td valign="top">PMPC Clients deployed in your PMPC Cloud Company.</td></tr><tr><td valign="top">Total external displays</td><td valign="top">External monitors detected.</td></tr><tr><td valign="top">Total batteries</td><td valign="top">Batteries detected.</td></tr><tr><td valign="top">Total logical drives</td><td valign="top">Logical drives detected, highlighting the total capacity and usage of each drive.</td></tr></tbody></table>

!['Hardware' page](../../../.gitbook/assets/image-\(4285\).png)

Clicking any of these statistics opens the device list modal, which contains the following additional information:

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows information about the…</th></tr></thead><tbody><tr><td valign="top">Clients deployed</td><td valign="top"><p>Which devices our Client is deployed to, including:</p><p>Computer Name, User Name, Client Version, Manufacturer, and Model.</p></td></tr><tr><td valign="top">Total external displays</td><td valign="top"><p>External monitors attached to your Clients, including:</p><p>Computer Name, User Name, Model, Serial Number, Manufacturer, Screen Size, Manufacturer Year, and Connection Type.</p></td></tr><tr><td valign="top">Total batteries</td><td valign="top"><p>Batteries detected in your Clients, including:</p><p>Computer Name, User, Name, Battery Name, Serial number, Chemistry, Full charge capacity, Design capacity, Health as a percentage.</p></td></tr><tr><td valign="top">Total logical disks</td><td valign="top"><p>Logical disks configured on your Clients, including:</p><p>Computer Name, User Name, Drive, Volume Name, Capacity in gigabytes, Free Space in gigabytes, and Usage as a percentage.</p></td></tr></tbody></table>

> \*\*Tip\*\*
>
> As is standard, clicking a record in a device list modal allows you to drill down to display more information about the selected record.

## Charts

The _Charts_ section of the Hardware page contains the following charts:

<table><thead><tr><th width="153.77777099609375" valign="top">Chart</th><th valign="top">Shows a breakdown by…</th></tr></thead><tbody><tr><td valign="top">Device Specs</td><td valign="top">Manufacturer of the different devices detected in your environment.</td></tr><tr><td valign="top">External Displays</td><td valign="top">Manufacturer of the different external monitors detected in your environment.</td></tr><tr><td valign="top">Battery Specs</td><td valign="top">Health of the different batteries detected in your environment.</td></tr><tr><td valign="top">Logical Drive Space Usage</td><td valign="top">The percentage of disk space used for the logical drives detected in your environment.</td></tr></tbody></table>

![Charts](../../../.gitbook/assets/image-\(4286\).png)

Clicking the action menu () for a chart allows you to switch between the following views:

<table><thead><tr><th width="153.77777099609375" valign="top">Chart</th><th valign="top">Available views</th></tr></thead><tbody><tr><td valign="top">Device Specs</td><td valign="top"><ul><li>Device Manufacturer (default)</li><li>Device Memory</li><li>Device Model</li></ul></td></tr><tr><td valign="top">External Displays</td><td valign="top"><ul><li>Display Manufacturer (default)</li><li>Display Size</li><li>Display Resolution</li><li>Display Year</li></ul></td></tr><tr><td valign="top">Battery Specs</td><td valign="top"><ul><li>Battery Health (default)</li><li>Battery Chemistry</li></ul></td></tr></tbody></table>

> \*\*Note\*\*
>
> When you click a segment, the device list modal displays the data only for that segment. Likewise, if you switch to a different view and click a segment of the donut, the device list modal only displays the data for the selected view and that segment.

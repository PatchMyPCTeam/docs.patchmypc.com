# Advanced Insights "Home" Dashboard

_Applies to: Patch My PC Advanced and Patch Insights_

The Home Dashboard is the first screen shown to you when first logging on to Advanced Insights. This page is designed to be a "daily check" type of view for your Configuration Manager environment, with a focus on software updates.

### Video Overview

{% embed url="https://www.youtube.com/watch?v=C3e_VJ-096M" %}
Video Overview of the Home Dashboard
{% endembed %}

### Dashboard Overview

![The Advanced Insights Home Dashboard](<../../.gitbook/assets/17 (1).png>)

The statistics across the top will show you details about your Configuration Manager environment and how long it has left in support, the number of devices in your environment which are under configuration, management versus devices that don't have the SCCM/ConfigMgr client install. We'll show you the number of updates in the environment which are required by at least one device, and we'll also show you any issues that you may be having with distribution of content across the Config manager infrastructure.

### Click Through Data

As with everything in the Advanced Insights interface, you can click on any of these stats to see further information about the devices or the infrastructure that is listed behind them. For example, clicking the Managed Devices box, will show a list of the machines and their managed/unmanaged state.

![](../../.gitbook/assets/image-\(2035\).png)

### Donut Charts

The next row of statistics are doughnut charts, which show you information about your Configuration Manager client count. In our demo environment we see that there are three devices running an old version of the client, two that are on a more recent version and everything else is fully up to date.

![](../../.gitbook/assets/image-\(2036\).png)

The next doughnut chart shows us details about Windows 10 and Windows 11 devices, and their support status. This chart can be pivoted to some of the other metrics that we have about Windows 10 and Windows 11. So for example, the servicing channel and we can also see things like the editions and the release version.

We can view all of the data used to build this chart by clicking the view chart data button under the cog icon.

![](../../.gitbook/assets/image-\(2037\).png)

We also show the same support and edition information for the Office 365 client if you have that deployed in the environment.

### Scan Cycle Chart

The chart on the right hand side will show us the status of the software updates scan cycle in your in your client estate. So here you can see that currently we have one machine which is running the software update scan and two have completed successfully. There are no errors. If everything is green in this chart, then that means that your software updates scan environment is healthy.

The final row on the home dashboard will show as computer compliance, sorted by default by your least compliant computers from a software update perspective.

![](../../.gitbook/assets/image-\(2038\).png)

We have several machines that have not sent in any software update compliance data for a while and so their compliance status is unknown against more recent updates. We can scroll through this list and can expand out the number of records that are being shown to show you a longer list.

### Device View

Clicking on any machine will take you to the detailed device view for that client where we show you the software update state for that individual machine.

![](../../.gitbook/assets/image-\(2039\).png)

This view shows detail of update agent configuration and scan health as well as required and installed updates. The Actions row allows us to invoke client actions against the device, such as an update deployment evaluation, reboot, etc.

The final view on the home dashboard is of deployed updates compliance.

![](../../.gitbook/assets/image-\(2032\).png)

We have dedicated Software Updates dashboards for a more detailed view of this data, but on the home page we can see our least compliant updates, and we can click through to see significant detail about each object, its deployment state, etc.

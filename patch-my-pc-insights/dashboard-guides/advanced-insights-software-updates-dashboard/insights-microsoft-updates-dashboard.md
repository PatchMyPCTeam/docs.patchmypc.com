# Insights "Microsoft Updates" Dashboard

_Applies to: Patch My PC Advanced and Patch Insights_

{% hint style="info" %}
This dashboard requires deployment of the [Advanced Insights Inventory Extensions](../../advanced-insights-inventory-extensions/)

Dashboard will only return data on devices managed by Windows Update for Business (WuFB)
{% endhint %}

<figure><img src="../../../.gitbook/assets/24.png" alt=""><figcaption><p>Microsoft Updates Scanning</p></figcaption></figure>

At the top of this dashboard you can see how many devices have reported Microsoft Update Inventory Data, count of Critical and Security updates required by one or more devices, Drivers required by one of more devices and Classifications and/or Products for required updates that you are not currently synchronising into Configuration Manager.

On the Windows Update Scanning Sources Donut chart you have 2 sources:

1. Windows Updates - Only does updates for the Windows Operating system itself. These updates also include Windows components such as Internet Explorer, DirectX, .NET and Windows Media Player. It also includes security and service pack updates.
2. Microsoft Update - Includes all of the items that Windows Update covers as well as other Microsoft products such as Office, SQL and Exchange all in one place.

On the All Required Updates report you get a list of updates available from Microsoft which 1 or more device require an update for which are not sync'd in your software update point for deployment.

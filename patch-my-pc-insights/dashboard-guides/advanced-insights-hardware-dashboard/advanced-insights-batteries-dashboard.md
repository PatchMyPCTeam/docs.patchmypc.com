---
description: Client computer batteries
---

# Advanced Insights "Batteries" Dashboard

_Applies to: Patch My PC Advanced Insights_

{% hint style="info" %}
This dashboard requires deployment of the [Advanced Insights Inventory Extensions](../../advanced-insights-inventory-extensions/)
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (2231).png" alt=""><figcaption><p>Batteries view</p></figcaption></figure>

Advanced Insights will display battery health data for managed devices. The table lists all devices with battery data. The design capacity (in mWh) is listed alongside the current Charge Capacity. The Health percentage shows the ratio of Charge Capacity to Design Capacity. As the battery loses capability to hold charge, the percentage shown will be lower. 100% Health is Good, 0% Health is bad.

This data is gathered by the Advanced Insights inventory extensions using the Powercfg.exe utility included with Windows.

Clicking an individual machine will show some additional detail about the device battery in the device view.

<figure><img src="../../../.gitbook/assets/image (2232).png" alt=""><figcaption><p>Device view battery information</p></figcaption></figure>

---
description: Advanced Insights Update scanning (this is not relevant for Patch Insights)
---

# Advanced Insights and Microsoft Updates Inventory

_Applies to: Patch My PC Advanced Insights_

If you use **Intune** to manage your windows updates (**Windows Update for Business**) then none of that compliance data is visible from ConfigMgr. This requires you to have to read compliance data from BOTH ConfigMgr and Intune.

## Solution

* You get **complete** visibility of **all** update compliance from Advanced Insights

![The Microsoft Updates Dashboard](/_images/6-(1 "The Microsoft Updates Dashboard").jpg>)

***

## How does it work?

We supplement your ConfigMgr compliance data with **additional data** from Microsoft Update.

Our Inventory Extensions WMI Provider runs on clients and scans against Microsoft Update to find update compliance data. This data is then pulled into ConfigMgr via Hardware Inventory for reporting.

![](/_images/image-(2010).png)

***

## Requirements

1. You must complete the implementation steps in the [Configuration Guide](advanced-insights-inventory-extensions/)
2. Clients must be configured to use **Windows Update for Business**
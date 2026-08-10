# Client Data Collection in Patch My PC Advanced/Patch Insights for Intune

_Applies to: Advanced/Patch Insights for Intune_

This article documents the data collected by the Patch My PC (PMPC) Advanced/Patch Insights for Intune client.

## Inventory Data

The inventory data collected/processed has been separated into the following categories:

* [Hardware](hardware-inventory-data.md)
* [Software](software-inventory-data.md)
* [User](user-inventory-data.md)

These definitions are based on the objects that exist within the PMPC Client code base or WMI.&#x20;

The current schedules for the collection of this data are shown below.

<table><thead><tr><th valign="top">Task Action ID</th><th valign="top">Task Action Name</th><th valign="top">Action Description</th><th valign="top">Intervals</th></tr></thead><tbody><tr><td valign="top">00000000-0000-0000-0000-000000000001</td><td valign="top">Policy task</td><td valign="top">Checks if there is new policy on the service side, and if yes, it downloads it.</td><td valign="top">60 Minutes</td></tr><tr><td valign="top">00000000-0000-0000-0000-000000000101</td><td valign="top">Hardware Inventory</td><td valign="top">Collects hardware specific information.</td><td valign="top">1440 Minutes (24 Hours)</td></tr><tr><td valign="top">00000000-0000-0000-0000-000000000103</td><td valign="top">Computed Inventory</td><td valign="top">Collects various hardware, software, and OS data.</td><td valign="top">1440 Minutes (24 Hours)</td></tr><tr><td valign="top">00000000-0000-0000-0000-000000000104</td><td valign="top">Update Inventory</td><td valign="top">Collects OS and PMPC software update compliance data.</td><td valign="top">720 Minutes (12 Hours)</td></tr><tr><td valign="top">00000000-0000-0000-0000-000000000200</td><td valign="top">Client Status Inventory</td><td valign="top">Collects data on Client and schedule task status.</td><td valign="top">60 Minutes</td></tr></tbody></table>

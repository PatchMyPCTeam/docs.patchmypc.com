# "Warranty" tab of the "Hardware" page of Patch My PC Advanced Insights for Intune

_Applies to: Advanced Insights for Intune_

The **Warranty** tab of the **Hardware** page of Patch My PC (PMPC) Advanced Insights for Intune lists warranty records for devices managed by your PMPC Cloud Company. Use it to identify active, expired, and missing warranty coverage.

A device can have several warranty records, such as a base warranty and one or more extensions. The table displays each record on its own row, but the dashboard consolidates those records to assign one warranty status to the device.

The dashboard considers a warranty active when its start date is before the current date and its end date is after the current date. When a device has warranties that cover different periods, the dashboard combines them into one continuous period if the next warranty starts no more than one day after the previous warranty ends.

## Warranty Status List

<table><thead><tr><th width="206.22222900390625" valign="top">Status</th><th valign="top">Meaning</th></tr></thead><tbody><tr><td valign="top">Active</td><td valign="top">At least one consolidated warranty period starts before the current date and ends after the current date.</td></tr><tr><td valign="top">Expired</td><td valign="top">The device has warranty data, but no consolidated warranty period covers the current date.</td></tr><tr><td valign="top">No Data</td><td valign="top">The manufacturer is supported, and the required dependency is available, but no warranty records were returned.</td></tr><tr><td valign="top">Dependency Missing</td><td valign="top">The manufacturer is supported, but the required manufacturer component or warranty data source is unavailable.</td></tr><tr><td valign="top">Unsupported</td><td valign="top">The device manufacturer is not supported for warranty collection.</td></tr></tbody></table>

Depending on the data available from the manufacturer, a warranty record can include:

* Warranty status
* Computer name
* User name
* Serial number
* Manufacturer
* Model
* Ship date
* Start date
* End date

Missing values display as **N/A**.

Warranty data comes from the PMPC Client. The client reads data that manufacturer software publishes locally on the device. It does not retrieve Dell, HP, or Lenovo warranty data directly from a manufacturer web API.

{% hint style="info" %}
**Note**

See [Prepare Devices for Warranty Reporting](../../technical-references/prepare-devices-warranty-reporting.md) for supported manufacturers and setup instructions.
{% endhint %}





See [Prepare Devices for Warranty Reporting](/broken/pages/371314fb30f054f52547fab4df6b262c18d0cbbf) for supported manufacturers and setup instructions.

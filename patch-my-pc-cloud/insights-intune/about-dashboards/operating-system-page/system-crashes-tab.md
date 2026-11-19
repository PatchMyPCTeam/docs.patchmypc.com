---
description: >-
  The System Crashes tab is only available in Advanced Insights for Intune,
  which requires an Enterprise Premium license and depends on the Patch My PC
  Client being operational on the client device.
---

# "System Crashes" Tab

{% hint style="info" %}
**Private Preview**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (1624).png" alt=""><figcaption></figcaption></figure>

The System Crashes tab of the Operating System page of Patch My PC Advanced Insights for Intune lists the system crashes reported by devices managed by your Patch My PC Cloud Company. A system crash, also called a stop error, bug check or blue screen (BSOD), happens when Windows detects a critical problem, halts to protect the device and its data, and then restarts.

Use the System Crashes tab to compare stability across device models and BIOS versions, identify the least stable devices so you can prioritize remediation or replacement, and track crash trends over time, for example after you deploy firmware or driver updates.

To open it, go to Advanced Insights > Operating System in the PMPC Cloud portal and select the System Crashes tab. The tab is split into the following sections:

·       Statistics

·       Charts

·       Tables

·       Device view

## Statistics

The top row of the System Crashes tab is called Statistics and displays the following statistics. Clicking any of them opens the device list modal, which lists the devices included in that statistic.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Statistic</td><td valign="top">Shows</td></tr><tr><td valign="top">Top Crash Error</td><td valign="top">The stop code name recorded most often across all devices, and how many times it has been recorded, based on all available data.</td></tr><tr><td valign="top">Most Impacted Device Model</td><td valign="top">The device model with the most affected devices (devices that have had at least one system crash), and how many of its devices are affected, based on all available data.</td></tr><tr><td valign="top">Crash Rate</td><td valign="top">The percentage of all devices running the PMPC Client that have had at least one system crash, with the number of affected devices out of the total.</td></tr><tr><td valign="top">Recent Events</td><td valign="top">The number of system crashes in the last 30 days, counted in UTC.</td></tr></tbody></table>

## Charts

The Charts section of the System Crashes tab contains the following charts. Clicking a chart segment opens the device list modal, which only displays the data for that segment.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Chart</td><td valign="top">Shows</td></tr><tr><td valign="top">Device Experience Distribution</td><td valign="top">A breakdown of all devices by crash-based experience tier. See Experience tiers below.</td></tr><tr><td valign="top">Stop Code Distribution</td><td valign="top">A breakdown of system crashes by stop code name, showing the ten most common stop codes.</td></tr><tr><td valign="top">System Crash Trend</td><td valign="top">The number of system crashes per day (UTC) over the last 60 days.</td></tr></tbody></table>

### Experience tiers

Each device is given one crash-based experience tier, based on the number of system crashes recorded for it across all available data. The Device Experience Distribution chart, and the Model Experience Distribution chart for each model, use these tiers.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Tier</td><td valign="top">Meaning</td></tr><tr><td valign="top">Excellent</td><td valign="top">No system crashes recorded.</td></tr><tr><td valign="top">Fair</td><td valign="top">1 to 3 system crashes recorded.</td></tr><tr><td valign="top">Poor</td><td valign="top">4 to 9 system crashes recorded.</td></tr><tr><td valign="top">Severely Degraded</td><td valign="top">10 or more system crashes recorded.</td></tr></tbody></table>

## Tables

### Model Reliability

The Model Reliability table lists each device model with its reliability and a breakdown of stable and affected devices. Click a model to open System Crashes for Model, which shows a Model Experience Distribution chart for that model's devices and an All System Crashes for Model table with the same columns as the All System Crashes table below.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Column</td><td valign="top">Shows</td></tr><tr><td valign="top">Model</td><td valign="top">The device model.</td></tr><tr><td valign="top">Reliability (%)</td><td valign="top">The percentage of devices of that model that have not had a system crash. For example, a model with one stable device and two affected devices shows 33%.</td></tr><tr><td valign="top">Reliability Breakdown</td><td valign="top">The number of Stable devices (no system crashes, shown in green) and Affected devices (at least one system crash, shown in red) of that model.</td></tr></tbody></table>

### All System Crashes

The All System Crashes table lists every system crash recorded across your devices, newest first. Depending on the data available, a record can include:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Column</td><td valign="top">Shows</td></tr><tr><td valign="top">Date</td><td valign="top">The date and time of the system crash, in UTC.</td></tr><tr><td valign="top">Computer Name</td><td valign="top">The name of the device.</td></tr><tr><td valign="top">User Name</td><td valign="top">The device's current user, who might not be the user signed in when the system crash occurred.</td></tr><tr><td valign="top">Model</td><td valign="top">The device model.</td></tr><tr><td valign="top">BIOS Version</td><td valign="top">The BIOS version currently installed on the device, which might be newer than the version installed when the system crash occurred.</td></tr><tr><td valign="top">Stop Code</td><td valign="top">The bug check code, shown as a decimal number. See Stop codes below.</td></tr><tr><td valign="top">Stop Code Name</td><td valign="top">The name Microsoft gives the stop code, for example PAGE_FAULT_IN_NONPAGED_AREA.</td></tr></tbody></table>

Missing values display as N/A. Use the search icon to find a record and the action menu (⋮) to export the table. Click a record to open that device's view (see Device view below).

## Device view

<figure><img src="../../../../.gitbook/assets/image (1628).png" alt=""><figcaption></figcaption></figure>

Clicking a record in the All System Crashes table, or in a model's list of system crashes, opens that device's view on its Operating System tab, with System selected. The System Crashes card on the right lists the system crashes recorded for the device, latest first, and each one shows:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Field</td><td valign="top">Shows</td></tr><tr><td valign="top">Date and time</td><td valign="top">When the system crash occurred, in UTC.</td></tr><tr><td valign="top">Stop Code</td><td valign="top">The bug check code, as a decimal number.</td></tr><tr><td valign="top">Stop Code Name</td><td valign="top">The name Microsoft gives the stop code.</td></tr><tr><td valign="top">Dmp File Path</td><td valign="top">Where Windows saved the memory dump on the device, usually %SystemRoot%\MEMORY.DMP, or the %SystemRoot%\Minidump folder for small memory dumps. The dump file itself is not uploaded and stays on the device.</td></tr><tr><td valign="top"></td><td valign="top"></td></tr></tbody></table>

<figure><img src="../../../../.gitbook/assets/image (1631).png" alt=""><figcaption></figcaption></figure>

## Stop codes

The Stop Code column shows the bug check code as a decimal number. Microsoft's documentation lists bug check codes in hexadecimal, so convert the value before you search for it. Windows Calculator converts between the two in Programmer mode.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Stop Code (decimal)</td><td valign="top">Hexadecimal</td><td valign="top">Stop Code Name</td></tr><tr><td valign="top">80</td><td valign="top">0x00000050</td><td valign="top">PAGE_FAULT_IN_NONPAGED_AREA</td></tr><tr><td valign="top">114</td><td valign="top">0x00000072</td><td valign="top">ASSIGN_DRIVE_LETTERS_FAILED</td></tr><tr><td valign="top">258</td><td valign="top">0x00000102</td><td valign="top">DPC_WATCHDOG_TIMEOUT</td></tr><tr><td valign="top">268435598</td><td valign="top">0x1000008E</td><td valign="top">KERNEL_MODE_EXCEPTION_NOT_HANDLED_M</td></tr></tbody></table>

## Where the data comes from

System crash data comes from the PMPC Client. When Windows restarts after a system crash, it records the stop code and the location of the memory dump in the System event log (Event ID 1001, from the Microsoft-Windows-WER-SystemErrorReporting provider). The client reads only these events, and reports each system crash together with the device's model and its current BIOS version and user name. It does not upload memory dump files, which stay on the device, and it does not collect the bug check parameters.

The PMPC Client collects system crash data as part of its computed inventory, which runs every 24 hours, so you don't need to set anything up on your devices. A new system crash can take up to 24 hours to appear on this tab. By default, when a device first reports system crash data, it includes the 10 most recent system crashes still recorded in its System event log.

System crashes are reported for physical and virtual devices, including those running Windows Server. A system crash can't be reported if its event isn't in the System event log when the client collects data, for example because memory dumps are turned off on the device or the System log has been cleared.

## Microsoft documentation

* Bug Check Code Reference, for the meaning of each stop code: https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-code-reference2
* Troubleshooting Windows unexpected restarts and stop code errors, for end users: https://support.microsoft.com/en-us/windows/experience/performance-optimization/troubleshooting-windows-unexpected-restarts-and-stop-code-errors
* Advanced troubleshooting for stop code errors, for IT professionals: https://learn.microsoft.com/en-us/troubleshoot/windows-client/performance/stop-code-error-troubleshooting

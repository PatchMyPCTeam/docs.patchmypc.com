---
description: >-
  The App Errors tab is only available in Advanced Insights for Intune, which
  requires an Enterprise Premium license and depends on the Patch My PC Client
  being operational on the client device.
---

# "Application Errors" Tab

{% hint style="info" %}
**Private Preview**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (1632).png" alt=""><figcaption></figcaption></figure>

The App Errors tab of the Software page of Patch My PC Advanced Insights for Intune lists the application errors reported by devices managed by your Patch My PC Cloud Company. Windows records an application error when a program hits a problem it can't handle (an unhandled exception), such as trying to use memory it isn't allowed to access. How this affects the program depends on the program and the error: it might close unexpectedly, or it might keep running.

Use the App Errors tab to find the applications that fail most often and on how many devices, see which error codes lie behind those failures, and compare stability across versions of an application, for example to check whether its latest release has improved things for your users.

To open it, go to Advanced Insights > Software in the PMPC Cloud portal and select the App Errors tab. The tab is split into the following sections:

* Statistics
* Application Errors

Clicking an application opens its details, and from there you can drill down to each affected device. See Application details and Device view below.

## Statistics

The top row of the App Errors tab is called Statistics and displays the following statistics. Clicking a statistic opens the application error details for that executable.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Statistic</td><td valign="top">Shows</td></tr><tr><td valign="top">Most Impacted Exe</td><td valign="top">The executable with the most application errors recorded across all devices, and how many, based on all available data. Clicking the statistic opens the application error details for that executable.</td></tr><tr><td valign="top">Most Persistently Impacted Exe</td><td valign="top">The executable with the longest period between its first and most recent recorded application errors, shown as a date range and its length in days.</td></tr></tbody></table>

## Application Errors

The Application Errors table lists every executable that has recorded at least one application error on your devices, with the most errors first. Depending on the data available, a record can include:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Column</td><td valign="top">Shows</td></tr><tr><td valign="top">Exe</td><td valign="top">The file name of the application that had the error, for example explorer.exe. Data is grouped by executable name, version and error code. Executables from different applications that have the same file name are therefore grouped under the same executable name.</td></tr><tr><td valign="top">Errors</td><td valign="top">The number of application errors recorded for the executable across all devices.</td></tr><tr><td valign="top">Devices</td><td valign="top">The number of devices that have recorded at least one application error for the executable.</td></tr><tr><td valign="top">First Seen</td><td valign="top">The date and time in UTC of the earliest application error recorded for the executable, based on all available data.</td></tr><tr><td valign="top">Last Seen</td><td valign="top">The date and time in UTC of the most recent application error recorded for the executable, based on all available data.</td></tr></tbody></table>

Use the search icon to find a record and the action menu (⋮) to export the table. Click a record to open the details for that executable (see Application details below).

## Application details

<figure><img src="../../../../.gitbook/assets/image (1633).png" alt=""><figcaption></figcaption></figure>

Clicking a record in the Application Errors table opens a view titled Application Errors for: followed by the name of the executable. It shows the aggregated error details for that executable on three tabs: Overview, Analysis and Devices.

### Overview

The Overview tab shows the following.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Item</td><td valign="top">Shows</td></tr><tr><td valign="top">Affected Devices</td><td valign="top">The number of devices that have had at least one application error for the executable.</td></tr><tr><td valign="top">Errors (Last 30 Days)</td><td valign="top">The number of application errors recorded for the executable during the last 30 calendar days.</td></tr><tr><td valign="top">Most Affected Version</td><td valign="top">The version of the executable that has had application errors on the most devices, and how many devices.</td></tr><tr><td valign="top">Top Error Code</td><td valign="top">The error code reported most often for the executable, and how many times. See Error codes below.</td></tr><tr><td valign="top">Recent Activity</td><td valign="top">A chart of all the executable's application errors per day over the last 60 days, with a separate colored area for each error code.</td></tr></tbody></table>

### Analysis

<figure><img src="../../../../.gitbook/assets/image (1634).png" alt=""><figcaption></figcaption></figure>

The Analysis tab shows the Error Code Distribution chart, a breakdown of the executable's application errors by error code that shows the ten most common error codes. It also shows the Version Distribution table, which lists each version of the executable that has recorded application errors, with the largest share of errors first:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Column</td><td valign="top">Shows</td></tr><tr><td valign="top">ErrorShare (%)</td><td valign="top">The version's share of all application errors recorded for the executable, based on all available data, shown as a percentage and a bar. For example, a version with 1,084 of an executable's 1,117 errors shows 97.05%. Shares below 50% use a warning-colored bar; shares of 50% or more use an error-colored bar. No green state is used because any recorded application error is undesirable.</td></tr><tr><td valign="top">Version</td><td valign="top">The file version of the executable.</td></tr><tr><td valign="top">Errors</td><td valign="top">The number of application errors recorded for that version.</td></tr><tr><td valign="top">Devices</td><td valign="top">The number of devices that have recorded at least one application error with that version.</td></tr><tr><td valign="top">First Seen</td><td valign="top">The date and time of the earliest application error recorded for that version.</td></tr><tr><td valign="top">Last Seen</td><td valign="top">The date and time of the most recent application error recorded for that version.</td></tr></tbody></table>

### Devices

<figure><img src="../../../../.gitbook/assets/image (1635).png" alt=""><figcaption></figcaption></figure>

The Devices tab lists the Affected Devices, the devices that have had at least one application error for the executable, with the most errors first. Use the search icon to find a device and the action menu (⋮) to export the list, and click a device to open its device view (see Device view below). Each record shows:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Column</td><td valign="top">Shows</td></tr><tr><td valign="top">Computer Name</td><td valign="top">The name of the device.</td></tr><tr><td valign="top">User Name</td><td valign="top">The device's current user, who might not be the user signed in when the application error occurred.</td></tr><tr><td valign="top">Errors</td><td valign="top">The number of application errors recorded for the executable on the device.</td></tr><tr><td valign="top">First Seen</td><td valign="top">The date and time of the earliest application error recorded for the executable on the device.</td></tr><tr><td valign="top">Last Seen</td><td valign="top">The date and time of the most recent application error recorded for the executable on the device.</td></tr></tbody></table>

## Device view

<figure><img src="../../../../.gitbook/assets/image (1636).png" alt=""><figcaption></figcaption></figure>

Clicking a device in the Devices tab currently opens that device's view on its Software tab on the App Errors sub-tab. The App Errors table lists the application errors recorded for the device by executable, and shows:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Field</td><td valign="top">Shows</td></tr><tr><td valign="top">Exe</td><td valign="top">The file name of the application that had the error.</td></tr><tr><td valign="top">Recent Trend</td><td valign="top">Eight squares, one for each of the last eight weeks (Monday to Sunday), starting with the oldest and ending with the current week. Each square is shaded by the number of application errors that week: the brighter the square, the more errors, and a dark square means none.</td></tr><tr><td valign="top">Errors</td><td valign="top">The number of application errors recorded for the executable on the device.</td></tr><tr><td valign="top">First Seen</td><td valign="top">The date and time of the earliest application error recorded for the executable on the device.</td></tr><tr><td valign="top">Last Seen</td><td valign="top">The date and time of the most recent application error recorded for the executable on the device.</td></tr></tbody></table>

Hover over the information icon (i) at the end of a row to see the Version, Error Code and number of Errors for the executable on the device. Click the copy icon next to a value to copy it to your clipboard.

## Error codes

The error code is the exception code Windows recorded for the application error. It's shown in hexadecimal, the format that Event Viewer and Microsoft's documentation use, so you can search for it as shown. Some codes you might see are listed below. For any other code, see NTSTATUS Values under Microsoft documentation below.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Error code</td><td valign="top">Name</td><td valign="top">What it usually means</td></tr><tr><td valign="top">0xC0000005</td><td valign="top">STATUS_ACCESS_VIOLATION</td><td valign="top">The application tried to read or write memory it isn't allowed to use.</td></tr><tr><td valign="top">0xC0000374</td><td valign="top">STATUS_HEAP_CORRUPTION</td><td valign="top">The memory the application manages while it runs (its heap) was found to be damaged.</td></tr><tr><td valign="top">0xC0000409</td><td valign="top">STATUS_STACK_BUFFER_OVERRUN</td><td valign="top">Windows detected a stack buffer overrun. Applications also raise this code to end themselves at once when they detect a serious problem.</td></tr><tr><td valign="top">0x80000003</td><td valign="top">STATUS_BREAKPOINT</td><td valign="top">The application reached a breakpoint, an instruction normally used for debugging, with no debugger attached.</td></tr><tr><td valign="top">0xC000001D</td><td valign="top">STATUS_ILLEGAL_INSTRUCTION</td><td valign="top">The application tried to run an instruction the processor can't execute.</td></tr><tr><td valign="top">0xC0000094</td><td valign="top">STATUS_INTEGER_DIVIDE_BY_ZERO</td><td valign="top">The application tried to divide a whole number by zero.</td></tr></tbody></table>

## Where the data comes from

Application error data comes from the PMPC Client. When a program hits an error it can't handle, Windows records an Application Error event (Event ID 1000) in the Application event log, including the program's name and version, the exception code and the module where the error happened. The client reads these events and counts them by executable name, version and error code. For each combination, it reports how many application errors are recorded in the log, when the first and last ones happened, and, by default, how many happened on each of the last 60 days. Events without an executable name, version or error code are skipped. The client doesn't report the faulting module or the program's path, and doesn't collect crash dump files.

The PMPC Client collects application error data as part of the computed inventory task, which runs every 24 hours, so you don't need to set anything up on your devices. A new application error can take up to 24 hours to appear on this tab. Because the client counts all the application errors still recorded in the device's Application event log each time, its first report includes earlier application errors, not just new ones. Daily counts cover the last 60 days.

Application errors are reported for every program Windows records one for, including Windows components such as explorer.exe and svchost.exe. Only Application Error events (Event ID 1000) are included, so application hangs (Event ID 1002) don't appear on this tab. An application error can't be newly reported if its event is no longer in the Application event log when the client collects data, for example because the log has been cleared or older events have been overwritten.

## Microsoft documentation

* The application or service crashing behavior troubleshooting guidance, for investigating an application that keeps crashing, including how to collect a crash dump: [https://learn.microsoft.com/en-us/troubleshoot/windows-server/performance/troubleshoot-application-service-crashing-behavior](https://learn.microsoft.com/en-us/troubleshoot/windows-server/performance/troubleshoot-application-service-crashing-behavior).
* NTSTATUS Values, for the meaning of each error code: [https://learn.microsoft.com/en-us/openspecs/windows\_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55 ](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55).

# "Secure Boot" Page of the Patch My PC Advanced/Patch Insights for Intune Dashboard

_Applies to: Advanced Insights for Intune_

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The **Secure Boot** page is only available in Advanced Insights for Intune, which requires an Enterprise Premium license.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [About Patch My PC Advanced/Patch Insights for Intune Dashboards](./) and [Working with Advanced/Patch Insights for Intune](../working-dashboards.md) for more information.</p>
<p>Also, this page relies on data from any devices running version 1.0.60 or later of the Patch My PC (PMPC) Client.</p>
<p>See [Manage the Patch My PC Client](../../manage/settings/client.md) for more details on deploying and managing the PMPC Client.</p>
</blockquote>

Secure Boot reporting is another feature of Advanced Insights for Intune. The Patch My PC (PMPC) Client gathers Secure Boot inventory data, including details of the 2023 certificate rollout.

The _Secure Boot_ page of Advanced Insights for Intune shows key statistics from your environment and is split into the following sections:

* [Statistics](secure-boot-page-of-the-patch-my-pc-advanced-patch-insights-for-intune-dashboard.md#statistics)
* [Table](secure-boot-page-of-the-patch-my-pc-advanced-patch-insights-for-intune-dashboard.md#table)
* [Device modal tab](secure-boot-page-of-the-patch-my-pc-advanced-patch-insights-for-intune-dashboard.md#device-modal-tab)
* [Donut charts](secure-boot-page-of-the-patch-my-pc-advanced-patch-insights-for-intune-dashboard.md#donut-charts)

## Statistics

The top row of the Secure Boot page is called _Statistics_ and displays the following statistics.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows the number of…</th></tr></thead><tbody><tr><td valign="top">Secure Boot Enabled</td><td valign="top">Reported devices with Secure Boot enabled</td></tr><tr><td valign="top">Completed 2023 Certificate Rollout</td><td valign="top">Devices with secure boot enabled that have completed the 2023 certificate process</td></tr><tr><td valign="top">Devices blocked by pending reboot</td><td valign="top">Devices that require a reboot to proceed with the 2023 certificate rollout</td></tr><tr><td valign="top">Devices blocked by firmware</td><td valign="top">Devices that require firmware updates to complete the 2023 certificate rollout</td></tr></tbody></table>

!['Hardware' page](/_images/image-(4357).png "&#x27;Hardware&#x27; page")

Clicking any statistic opens the device list modal, which contains the following additional information:

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows information about the…</th></tr></thead><tbody><tr><td valign="top">Secure Boot Enabled</td><td valign="top"><p>Secure Boot state for devices, including:</p><p>Computer Name, User Name, Manufacturer, Model, and Secure Boot Enabled.</p></td></tr><tr><td valign="top">Completed 2023 Certificate Rollout</td><td valign="top"><p>Devices that have completed the 2023 certificate process, including:</p><p>Computer Name, Manufacturer, Model, Firmware, LastEventId, DbUpdated, and KEKUpdated.</p></td></tr><tr><td valign="top">Devices blocked by pending reboot</td><td valign="top"><p>Devices that require a reboot to continue, including:</p><p>Computer Name, Manufacturer, Model, Firmware, LastEventId, DbUpdated, and KEKUpdated.</p></td></tr><tr><td valign="top">Devices blocked by firmware</td><td valign="top"><p>Devices identified as needing a firmware update to complete the 2023 certificate rollout, including:</p><p>Computer Name, Manufacturer, Model, Firmware, and Firmware Minimum.</p></td></tr></tbody></table>

## Table

The _Table_ section of the Secure Boot page lists devices and their current Secure Boot rollout data.

Use this table to view detailed 2023 Certficate rollout data across all devices with Secure Boot enabled.

![Charts](/_images/image-(4361).png "Charts")

## Donut charts

The _Donut charts_ section of the Secure Boot page contains the following donut charts.

Clicking the action menu (![](/_images/2YYkqAAAAAElFTkSuQmCC)) for a chart allows you to switch between the following views:

<table><thead><tr><th width="153.77777099609375" valign="top">Chart</th><th valign="top">Shows a breakdown by…</th></tr></thead><tbody><tr><td valign="top">Rollout Progress</td><td valign="top">High-level 2023 certificate rollout progress across all devices where Secure Boot is enabled.</td></tr><tr><td valign="top">Rollout Progress (Detailed Statuses)</td><td valign="top">Detailed 2023 certificate rollout progress across all devices where Secure Boot is enabled.</td></tr></tbody></table>

![Charts](/_images/image-(4358).png "Charts")

![Charts](/_images/image-(4359).png "Charts")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>When you click a segment, the device list modal displays the data only for that segment. Likewise, if you switch to a different view and click a segment of the donut, the device list modal only displays the data for the selected view and that segment.</p>
</blockquote>

## Device modal tab

Clicking a device in any Secure Boot list opens that device’s modal.

The **Secure Boot** tab shows detailed Secure Boot status and 2023 certificate rollout details for the selected device.

![Charts](/_images/image-(4360).png "Charts")

***

## Data Explainations

<blockquote class="wp-block-quote">
<p>### Data Explaination - Minimum Firmware Detection</p>
<p>Any firmware requirements are calculated using data provided by OEMs. As such, firmware requirements can only be detected on supported models where data has been provided from HP, Dell, and Lenovo</p>
<p>Please use the following external vendor documentation to validate model support and firmware requirements:</p>
<p>* <a href="https://www.dell.com/support/kbdoc/en-uk/000347876/microsoft-2011-secure-boot-certificate-expiration">DELL</a></p>
<p>* <a href="https://support.hp.com/us-en/document/ish_13070353-13070429-16">HP</a></p>
<p>* <a href="https://support.lenovo.com/us/en/solutions/ht518129">Lenovo</a></p>
</blockquote>

<blockquote class="wp-block-quote">
<p>### Data Explaination - "Status"</p>
<p>We compute a single **Secure Boot Status** for each device by evaluating all available Secure Boot–related properties and events. The goal is to reduce a complex and highly fragmented dataset into a single status that clearly communicates the device’s current state in the Secure Boot certificate rollout.</p>
<p>For example, if we detect a device does not meet the minimum firmware requirements to install the 2023 Secure Boot certificates, its status is set to **`RequiresFirmwareUpdate`**.</p>
<p>All Possible Statuses:</p>
<p>* Unknown</p>
<p>* Completed</p>
<p>* RequiresFirmwareUpdate</p>
<p>* EventId1800RebootRequired</p>
<p>* EventId1796UnexpectedError</p>
<p>* EventId1797Ca2023NotInDb</p>
<p>* EventId1798BootManagerNotSigned</p>
<p>* EventId1795FirmwareUpdateError</p>
<p>* EventId1802BlockedByCondition</p>
<p>* EventId1803KekNotFound</p>
<p>* KekUpdateFailed</p>
<p>* Uefi2023ErrorOccurred</p>
<p>* Stage1DeployCertificates</p>
<p>* Stage2AddCa2023ToDb</p>
<p>* Stage3ApplyOptionRomCa2023</p>
<p>* Stage4ApplyMicrosoftCa2023</p>
<p>* Stage5ApplyKek2023</p>
<p>* Stage6ApplyBootmgfw</p>
<p>* CertsInstalledPendingSignature</p>
<p>* KekUpdatedDbPending</p>
<p>* RolloutInProgress</p>
<p>* RolloutNotStarted</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>### Microsoft Documentation</p>
<p><a href="https://support.microsoft.com/en-us/topic/registry-key-updates-for-secure-boot-windows-devices-with-it-managed-updates-a7be69c9-4634-42e1-9ca1-df06f43f360d">Microsoft Support - Registry keys for Secure Boot</a></p>
<p><a href="https://support.microsoft.com/en-gb/topic/secure-boot-db-and-dbx-variable-update-events-37e47cf8-608b-4a87-8175-bdead630eb69">Microsoft Support - Secure Boot Event Ids</a></p>
</blockquote>
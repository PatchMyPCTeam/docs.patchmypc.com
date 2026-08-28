# "Updates" Page of the Patch My PC Advanced/Patch Insights for Intune Dashboard

_Applies to: Advanced Insights for Intune_

{% hint style="info" %}
**Note**

The **Updates** page is only available in Advanced Insights for Intune, which requires an Enterprise Premium license.
{% endhint %}

Software Update compliance reporting is a major feature of Advanced Insights for Intune. The Patch My PC (PMPC) Client performs a compliance scan against the full PMPC Catalog and the Microsoft Updates service each day and returns the result to your PMPC Company.

Compliance data is shown for all updates, whether deployed or not.

The _Updates_ page consists of the following two tabs, which contain a collection of dashboard items:

* [Patch My PC](updates-page.md#patch-my-pc)
* [Microsoft](updates-page.md#microsoft)

<figure><img src="../../../.gitbook/assets/image (754).png" alt="&#x27;Software Updates&#x27; page" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See [About Advanced/Patch Insights for Intune Dashboards](./) and [Working with Advanced/Patch Insights for Intune Dashboards](../working-dashboards.md) for more information.

Also, only devices running the Patch My PC (PMPC) Client will appear on this page. See [Manage the Patch My PC Client](../../manage/settings/client.md) for more details on deploying and managing the PMPC Client.
{% endhint %}

## Patch My PC

The **Patch My PC** tab is split into the following sections:

* [Statistics](updates-page.md#statistics)
* [Compliance](updates-page.md#compliance)

### Statistics

The top section of the **Patch My PC** tab is called _Statistics_ and displays information about the PMPC Client and apps within your environment.

<figure><img src="../../../.gitbook/assets/image (755).png" alt="&#x27;Statistics&#x27; section" width="563"><figcaption></figcaption></figure>

When you click a statistic, the device list modal for that statistic opens, displaying more information.

<figure><img src="../../../.gitbook/assets/image (756).png" alt="Device list modal" width="563"><figcaption></figcaption></figure>

The _Statistics_ section is split into the following reports:

* [Patch My PC Catalog](updates-page.md#patch-my-pc-catalog)
* [Average Device Compliance](updates-page.md#average-device-compliance)
* [Devices that require Patch My PC updates](updates-page.md#devices-that-require-patch-my-pc-updates)
* [Devices with 100% Patch my PC Update compliance](updates-page.md#devices-with-100-patch-my-pc-update-compliance)

#### Patch My PC Catalog

The **Patch My PC Catalog** statistic shows the latest version number of our catalog and the number of devices that have scanned this catalog.

Our catalog is updated daily (sometimes multiple times), so it is not unusual to see a low count after a catalog release.

The device modal for this statistic (shown in the example above) lists the versions of our catalog in your environment, with a device count for each and the last scan date.

Clicking a catalog version displays more detailed information for each Client running this version.

{% hint style="info" %}
**Note**

If devices are running a significantly out-of-date version of the catalog, it potentially puts them at risk of not detecting newer required updates.

You should therefore investigate any potential issues with the Client if this issue occurs.
{% endhint %}

#### Average Device Compliance

The **Average Device Compliance** statistic shows the average PMPC update compliance across all devices, with a value of 90% or more being considered exceptional.

#### Devices that require Patch My PC updates

The **Devices that require Patch My PC updates** statistic shows a count of any devices that require at least one update.

#### Devices with 100% Patch My PC Update compliance

The **Device with 100% Patch My PC Update compliance** statistic shows a  count of devices that have zero missing PMPC updates.

### Compliance

The _Compliance_ section shows the following compliance reports:

* [Patch My PC Update Compliance](updates-page.md#patch-my-pc-update-compliance)
* [Patch My PC Update Compliance by Device](updates-page.md#patch-my-pc-update-compliance-by-device)

#### Patch My PC Update Compliance

The **Patch My PC Update Compliance** report lists PMPC update compliance for updates categorized as either critical or security.

The table lists overall compliance for each update.

<figure><img src="../../../.gitbook/assets/image (757).png" alt="&#x27;Patch My PC Update Compliance&#x27; report" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

By default, superseded updates are hidden. Click the **Show Superseded Updates** toggle to display them. This feature can be especially useful for tracking compliance of frequently updated applications, such as Chrome.
{% endhint %}

For each update, we show the number of:

* The overall compliance as a percentage.
* Compliant devices (devices where the update is either **Installed** or **Not Applicable** to the device).
* Devices still needing this update (**Required**).
* Devices that have not yet submitted scan data for the catalog, which includes this update (**Unknown**).

Clicking an update shows more detailed information, including detailed metadata for the update.

#### Patch My PC Update Compliance by Device

The **Patch My PC Update Compliance by Device** report shows compliance data for each device against the PMPC catalog, allowing you to evaluate compliance for all updates in our catalog and whether they are deployed.

<figure><img src="../../../.gitbook/assets/image (758).png" alt="&#x27;Patch My PC Update Compliance by Device&#x27; report" width="563"><figcaption></figcaption></figure>

The compliance list includes details of the catalog version used by the Client and how up-to-date it is.

Clicking an individual record shows the **Device** view for that Client with the **Patch My PC** tab selected, which lists both the updates required and installed on the device.

The other tabs on the **Device** view are listed below.

<table><thead><tr><th width="98.33331298828125" valign="top">Tab</th><th valign="top">Shows...</th></tr></thead><tbody><tr><td valign="top">General</td><td valign="top">General information about the device, such as the Client version number, domain, the last time both hardware and software inventory ran, model, serial number, and others.</td></tr><tr><td valign="top">Hardware</td><td valign="top">Various hardware-related information for the selected device.</td></tr><tr><td valign="top">Software</td><td valign="top">Software inventory-related information for the selected device.</td></tr><tr><td valign="top">Patch My PC</td><td valign="top">Update Compliance data from the PMPC Catalog.</td></tr><tr><td valign="top">Microsoft</td><td valign="top">A list of the required Microsoft Updates and which have been installed on this device.</td></tr><tr><td valign="top">Drivers</td><td valign="top">Driver compliance for this device (sourced from Microsoft Updates).</td></tr></tbody></table>

## Microsoft

The **Microsoft** tab is split into the following sections:

* [Statistics](updates-page.md#statistics-1)
* [Compliance](updates-page.md#compliance-1)

### Statistics

The top section of the **Microsoft** tab is called _Statistics_ and displays information about the PMPC Client and Microsoft updates within your environment.

<figure><img src="../../../.gitbook/assets/image (4274).png" alt="&#x27;Microsoft&#x27; tab" width="563"><figcaption></figcaption></figure>

When you click a statistic, the device list modal for that statistic opens, displaying more information.

The _Statistics_ section is split into the following reports:

* [Microsoft Update](updates-page.md#microsoft-update)
* [Average Device Compliance](updates-page.md#average-device-compliance-1)
* [Devices that require Microsoft Updates](updates-page.md#devices-that-require-microsoft-updates)
* [Devices with 100% Microsoft Update compliance](updates-page.md#devices-with-100-microsoft-update-compliance)

#### Microsoft Update

The **Microsoft Update** statistic shows the number of devices that have submitted Microsoft update inventory today.

The device modal for this statistic lists the Windows Update Agent (WUA) version for each device along with other useful information such as last scanned date, status message and code, computer name, and user ID.

Clicking a row provides more detailed information for a given device.

#### Average Device Compliance

The **Average Device Compliance** statistic shows the average Microsoft Update compliance across all devices, where values of 90% or more being considered exceptional.

#### Devices that require Microsoft Updates

The **Device with 100% compliance** statistic shows a count of devices requiring at least one update from the Microsoft Update catalog.

#### Devices with 100% Microsoft Update compliance

The **Device with 100% compliance** statistic shows a count of devices that have zero missing updates from the Microsoft Update catalog.

### Compliance

The compliance section of the Microsoft tab shows the following compliance reports:

* [Microsoft Update Compliance](updates-page.md#microsoft-update-compliance)
* [Microsoft Update Compliance by Device](updates-page.md#microsoft-update-compliance-by-device)
* [Microsoft Update Driver Compliance](updates-page.md#microsoft-update-driver-compliance)

#### Microsoft Update Compliance

The **Microsoft Update Compliance** report lists Microsoft update compliance for updates delivered through the Microsoft Update Catalog. (Excludes driver updates)

<figure><img src="../../../.gitbook/assets/image (4364).png" alt="&#x27;Microsoft Update Compliance&#x27; report"><figcaption></figcaption></figure>

For each update, we show the number of:

* Compliant devices (**Installed**).
* Devices still needing this update (**Required**).
* The overall compliance as a percentage.

Clicking an update shows more detailed information.

#### Microsoft Update Compliance by Device

The **Microsoft Update Compliance by Device** report shows compliance data for each device against Microsoft Update, allowing you to evaluate compliance for all Microsoft updates in your environment. (Excludes driver updates)

<figure><img src="../../../.gitbook/assets/image (4276).png" alt="&#x27;Microsoft Update Compliance by Device&#x27; report" width="563"><figcaption></figcaption></figure>

Clicking an individual record shows the **Device** view for that Client with the **Microsoft** tab selected, which lists both the updates required and installed on the device.

#### Microsoft Update Driver Compliance

The **Microsoft Update Driver Compliance** report shows compliance data for drivers delivered through the Microsoft Update Catalog.

<figure><img src="../../../.gitbook/assets/image (4365).png" alt="&#x27;Microsoft Update Compliance by Device&#x27; report"><figcaption></figcaption></figure>

Clicking an individual record shows the **Device List** view for that Driver Update. Clicking a device will take you to the **Driver** tab within that clients device modal to give you a detailed breakdown of driver compliance per device.

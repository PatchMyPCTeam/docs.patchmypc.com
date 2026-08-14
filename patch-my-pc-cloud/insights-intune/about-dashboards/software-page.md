# "Software" Page of the Patch My PC Advanced/Patch Insights for Intune Dashboard

_Applies to: Advanced Insights for Intune_

{% hint style="info" %}
**Note**

The **Software** page is only available in Advanced Insights for Intune, which requires an Enterprise Premium license.
{% endhint %}

Enhanced software inventory is another significant facet of Advanced Insights for Intune. The Patch My PC (PMPC) Client gathers inventory data across a range of inventory properties to improve visibility and management of your estate.

The _Software_ page consists of the following tabs, which contain a collection of dashboard items:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><a href="software-page.md#system-apps">System Apps</a></td><td valign="top"><a href="software-page.md#user-apps">User Apps</a></td><td valign="top"><a href="software-page.md#browser-extensions">Browser Extensions</a></td><td valign="top"><a href="software-page.md#msi-source-health">MSI Source Health</a></td></tr></tbody></table>

<figure><img src="../../../.gitbook/assets/image (4393).png" alt="&#x27;Software&#x27; page" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See [About Advanced/Patch Insights for Intune Dashboards](./) and [Working with Advanced/Patch Insights for Intune Dashboards](../working-dashboards.md) for more information.

Also, only devices running the Patch My PC (PMPC) Client will appear on this page. See [Manage the Patch My PC Client](../../manage/settings/client.md) for more details on deploying and managing the PMPC Client.
{% endhint %}

The layout of the views differs depending on the tab you select.

## System Apps

The **System Apps** tab is split into the following sections:

* [Statistics](software-page.md#statistics)
* [Total System Applications](software-page.md#total-system-applications)

### Statistics

The top row of the **Systems App** page is called _Statistics_ and displays the following statistics.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows the number of…</th></tr></thead><tbody><tr><td valign="top">Total system applications</td><td valign="top">Applications installed in the SYSTEM context in your environment, including the app title, publisher, and number of instances found.</td></tr></tbody></table>

<figure><img src="../../../.gitbook/assets/image (4395).png" alt="&#x27;Software&#x27; page" width="563"><figcaption></figcaption></figure>

When you click a statistic, the device list modal for that statistic opens, displaying more information.

<figure><img src="../../../.gitbook/assets/image (4396).png" alt="Device list modal" width="563"><figcaption></figcaption></figure>

### Total System Applications

The _Total System Applications_ section shows the following.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows information about the…</th></tr></thead><tbody><tr><td valign="top">Title</td><td valign="top">Name of the software.</td></tr><tr><td valign="top">Publisher</td><td valign="top">Name of the publisher of the software.</td></tr><tr><td valign="top">Versions</td><td valign="top">Total number of different versions installed</td></tr><tr><td valign="top">Total Installed</td><td valign="top">Total number of instances of the software installed.</td></tr></tbody></table>

Clicking an individual record shows the **Devices With System Application: <**_**software\_name**_**> version** view, which displays the following:

<table><thead><tr><th width="193.77783203125" valign="top">Field</th><th valign="top">Displays the...</th></tr></thead><tbody><tr><td valign="top">Computer Name</td><td valign="top">Name of the device on which this software is installed.</td></tr><tr><td valign="top">User Name</td><td valign="top">Name of the user signed in when the software inventory scan ran.</td></tr><tr><td valign="top">Display Version</td><td valign="top">Version of the software.</td></tr><tr><td valign="top">Publisher</td><td valign="top">Publisher of the software.</td></tr><tr><td valign="top">Registry Key</td><td valign="top">Registry Key created for the software when it was installed.</td></tr></tbody></table>

{% hint style="success" %}
**Tip**

As is standard, clicking a record in a device list modal allows you to drill down to display more information about the selected record.
{% endhint %}

## User Apps

The **User Apps** tab is split into the following sections:

* [Statistics](software-page.md#statistics-1)
* [Total User Applications](software-page.md#total-user-applications)

### Statistics

The top row of the **User Apps** page is called _Statistics_ and displays the following statistics.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows the number of…</th></tr></thead><tbody><tr><td valign="top">Total user applications</td><td valign="top">Applications installed in any user profiles, including the app title, publisher, and number of instances found.</td></tr></tbody></table>

<figure><img src="../../../.gitbook/assets/image (4397).png" alt="&#x27;User Apps&#x27; page" width="563"><figcaption></figcaption></figure>

When you click a statistic, the device list modal for that statistic opens, displaying more information.

<figure><img src="../../../.gitbook/assets/image (4398).png" alt="Device list modal" width="563"><figcaption></figcaption></figure>

### Total User Applications

The _Total User Applications_ section shows the following.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows information about the…</th></tr></thead><tbody><tr><td valign="top">Title</td><td valign="top">Name of the software.</td></tr><tr><td valign="top">Publisher</td><td valign="top">Name of the publisher of the software.</td></tr><tr><td valign="top">Total Installed</td><td valign="top">Total number of instances of the software installed.</td></tr></tbody></table>

Clicking an individual record shows the **Devices With User Application: <**_**software\_name**_**> version** view, which displays the following:

<table><thead><tr><th width="193.77783203125" valign="top">Field</th><th valign="top">Displays the...</th></tr></thead><tbody><tr><td valign="top">Computer Name</td><td valign="top">Name of the device on which this software is installed.</td></tr><tr><td valign="top">Installed For User</td><td valign="top">Name of the user for whom the software is installed.</td></tr><tr><td valign="top">Display Version</td><td valign="top">Version of the software.</td></tr><tr><td valign="top">Publisher</td><td valign="top">Publisher of the software.</td></tr></tbody></table>

{% hint style="success" %}
**Tip**

As is standard, clicking a record in a device list modal allows you to drill down to display more information about the selected record.
{% endhint %}

## Browser Extensions

The **Browser Extensions** tab is split into the following sections:

* [Statistics](software-page.md#statistics-2)
* [Total Browser Extensions](software-page.md#total-browser-extensions)

### Statistics

The top row of the **Browser Extensions** page is called _Statistics_ and displays the following statistics.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows the number of…</th></tr></thead><tbody><tr><td valign="top">Total browser extensions</td><td valign="top">Firefox, Chrome, and Edge browser extensions installed in your environment, including the title of the extension and the number of instances found.</td></tr></tbody></table>

<figure><img src="../../../.gitbook/assets/image (4399).png" alt="&#x27;Total browser extensions&#x27;" width="563"><figcaption></figcaption></figure>

When you click a statistic, the device list modal for that statistic opens, displaying more information.

<figure><img src="../../../.gitbook/assets/image (4400).png" alt="Device list modal" width="563"><figcaption></figcaption></figure>

### Total Browser Extensions

The _Total Browser Extensions_ section shows the following.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows information about the…</th></tr></thead><tbody><tr><td valign="top">Title</td><td valign="top">Name of the browser extension.</td></tr><tr><td valign="top">Publisher</td><td valign="top">Name of the publisher of the browser extension.</td></tr><tr><td valign="top">Total Installed</td><td valign="top">Total number of instances of the browser extension installed.</td></tr></tbody></table>

Clicking an individual record shows the **Devices With Browser Extension: \<extension**_**\_name**_**>** view, which displays the following:

<table><thead><tr><th width="193.77783203125" valign="top">Field</th><th valign="top">Displays the...</th></tr></thead><tbody><tr><td valign="top">Computer Name</td><td valign="top">Name of the device on which this browser extension is installed.</td></tr><tr><td valign="top">Installed For User</td><td valign="top">Name of the user the browser extension is installed for.</td></tr><tr><td valign="top">Version</td><td valign="top">Version of the browser extension.</td></tr><tr><td valign="top">Browser</td><td valign="top">Name of the browser.</td></tr><tr><td valign="top">Browser Profile</td><td valign="top">Name of the browser profile where the browser extension is installed.</td></tr></tbody></table>

{% hint style="success" %}
**Tip**

As is standard, clicking a record in a device list modal allows you to drill down to display more information about the selected record.
{% endhint %}

## MSI Source Health

The **MSI Source Health** tab provides visibility into devices that may experience MSI repair, update, uninstall, or patching failures because the original MSI installation source is missing. It helps administrators proactively identify and troubleshoot affected devices before software management issues occur.

It is split into the following sections:

* [Statistics](software-page.md#statistics-3)
* [Missing MSI Sources](software-page.md#missing-msi-sources)
* [All Missing MSI Sources](software-page.md#all-missing-msi-sources)

### Statistics

The top row of the **MSI Source Health** page is called _Statistics_ and displays the following statistics.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows the number of…</th></tr></thead><tbody><tr><td valign="top">Count of devices where MSI sources are missing</td><td valign="top">Devices where MSI source health issues have been detected.</td></tr><tr><td valign="top">Missing MSI sources detected across all devices</td><td valign="top">Devices where MSI source health issues have been detected.</td></tr></tbody></table>

<figure><img src="../../../.gitbook/assets/image (4401).png" alt="&#x27;Software&#x27; page" width="563"><figcaption></figcaption></figure>

### Missing MSI Sources

The _Missing MSI Sources_ section shows MSI installations that cannot resolve their installation source and will encounter 'System Error 1612' on installation actions. Grouped by MSI Code. This section shows the following.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows information about the…</th></tr></thead><tbody><tr><td valign="top">MSI Code</td><td valign="top">MSI code for the software.</td></tr><tr><td valign="top">Display Name</td><td valign="top">Name of the software.</td></tr><tr><td valign="top">Publisher</td><td valign="top">Name of the publisher of the software.</td></tr><tr><td valign="top">Package Name</td><td valign="top">Name of the MSI package.</td></tr><tr><td valign="top">Devices</td><td valign="top">The total number of devices affected.</td></tr></tbody></table>

Clicking an individual record shows the **Devices With MSI Source Issues: <**_**software\_name**_**>** view, which displays the following:

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows information about the…</th></tr></thead><tbody><tr><td valign="top">MSI Code</td><td valign="top">MSI code for the software.</td></tr><tr><td valign="top">Display Name</td><td valign="top">Name of the software.</td></tr><tr><td valign="top">Display Version</td><td valign="top">Version of the software.</td></tr><tr><td valign="top">Publisher</td><td valign="top">Name of the publisher of the software.</td></tr><tr><td valign="top">Package Name</td><td valign="top">Name of the MSI package.</td></tr><tr><td valign="top">Computer Name</td><td valign="top">Name of the affected device.</td></tr><tr><td valign="top">User Name</td><td valign="top">Username affected.</td></tr></tbody></table>

{% hint style="success" %}
**Tip**

As is standard, clicking a record in a device list modal allows you to drill down to display more information about the selected record.
{% endhint %}

### All Missing MSI Sources

The _All Missing MSI Sources_ section shows a flat table of all missing MSI source instances. This section shows the following.

<table><thead><tr><th width="193.77783203125" valign="top">Statistic</th><th valign="top">Shows information about the…</th></tr></thead><tbody><tr><td valign="top">MSI Code</td><td valign="top">MSI code for the software.</td></tr><tr><td valign="top">Display Name</td><td valign="top">Name of the software.</td></tr><tr><td valign="top">Publisher</td><td valign="top">Name of the publisher of the software.</td></tr><tr><td valign="top">Package Name</td><td valign="top">Name of the MSI package.</td></tr><tr><td valign="top">Computer Name</td><td valign="top">Name of the affected device.</td></tr><tr><td valign="top">User Name</td><td valign="top">Username affected.</td></tr></tbody></table>

{% hint style="success" %}
**Tip**

As is standard, clicking a record in a device list modal allows you to drill down to display more information about the selected record.
{% endhint %}

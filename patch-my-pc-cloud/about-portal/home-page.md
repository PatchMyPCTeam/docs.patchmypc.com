# Home page of the Patch My PC Cloud Portal

_Applies to: Patch My PC (PMPC) Cloud_

{% hint style="danger" %}
**Public Preview**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

All Patch My PC (PMPC) Cloud management-related tasks are performed through the browser-based Cloud Portal. When you sign in to PMPC Cloud using the following link, you see the **Home** page.

[https://portal.patchmypc.com/](https://portal.patchmypc.com/)

{% hint style="info" %}
**Note**

The **Home** page is currently available to Enterprise Customers only.
{% endhint %}

The version of the **Home** page you see depends on your PMPC Cloud subscription type.

If you are an **Enterprise Plus** subscriber, you will see this version of the **Home** page:

<figure><img src="../../.gitbook/assets/image (1681).png" alt="Enterprise Plus ‘Home’ page" width="563"><figcaption></figcaption></figure>

Whereas if you are an **Enterprise Premium** subscriber, you will see this version of the **Home** page:

<figure><img src="../../.gitbook/assets/image (1682).png" alt="Enterprise Premium ‘Home’ page" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The differences between the **Home** page versions are explained below.
{% endhint %}

The Home page is split into the following tiled areas:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><a href="home-page.md#environment-overview">Environment Overview</a></td><td valign="top"><a href="home-page.md#new-apps">New Apps</a></td><td valign="top"><a href="home-page.md#unmanaged-applications">Unmanaged Applications</a></td></tr><tr><td valign="top"><a href="home-page.md#latest-catalog-additions">Latest Catalog Additions</a></td><td valign="top"><a href="home-page.md#videos">Videos</a></td><td valign="top"><a href="home-page.md#news-and-links">News &#x26; Links</a></td></tr><tr><td valign="top"><a href="home-page.md#managed-apps-install-states">Managed Apps Install States</a></td><td valign="top"><a href="home-page.md#license-information">License Information</a></td><td valign="top"><a href="home-page.md#share-your-feedback">Share Your Feedback</a></td></tr></tbody></table>

{% hint style="info" %}
**Note**

See the relevant section below for more information.
{% endhint %}

## Environment Overview

The **Environment Overview** section of the **Home** page provides an overview of the Public Apps in your environment, which refreshes each time you sign in to the Portal.

{% hint style="info" %}
**Note**

You can press `F5` to refresh the data on the **Home** page.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1683).png" alt="&#x27;Environment Overview&#x27; section" width="563"><figcaption></figcaption></figure>

The **Environment Overview** section contains the following:

<table><thead><tr><th width="253.33331298828125" valign="top">Section</th><th valign="top">Shows the...</th></tr></thead><tbody><tr><td valign="top">Deployments Up to Date</td><td valign="top">Percentage of your managed app deployments that are currently publishing the latest available version. PMPC automatically updates your deployments as new versions are released. A high percentage means your deployments are keeping pace with the latest releases across all managed apps.</td></tr><tr><td valign="top">Compliance Percentage<strong>*</strong></td><td valign="top">Percentage of your managed app updates that have been fully applied across your environment - that is, updates where no devices are left needing them. <br><br>Unlike <strong>Deployments Up to Date</strong> (which reflects the version you're publishing), this metric reflects the actual state of your devices: it reaches 100% for an update only once every device has installed it. A high percentage means your devices are fully patched across all managed apps.<br><br>This chart is shown instead of <strong>Deployments Up to Date</strong>.</td></tr><tr><td valign="top">Number of Deployments</td><td valign="top">Total number of deployments</td></tr><tr><td valign="top">Clients Deployed<strong>*</strong></td><td valign="top">Total number of PMPC Clients deployed instead of the Number of Deployments.</td></tr><tr><td valign="top">Updates</td><td valign="top">Total number of app updates that PMPC published for any apps deployed over the last 12 months</td></tr><tr><td valign="top">Resolved CVEs</td><td valign="top">Total number of CVEs resolved in those updates over the last 12 months</td></tr><tr><td valign="top">Top 3 vulnerabilities resolved</td><td valign="top">Most significant CVEs that have been remediated by PMPC deployments in your environment over the past 7 days. Each entry shows the CVE identifier and its severity score, so you can see at a glance which high-impact vulnerabilities your recent updates have addressed.<br><br>Clicking a CVE displays more information about that specific CVE.</td></tr><tr><td valign="top">Devices Patched</td><td valign="top">Total number of devices that are patched.</td></tr><tr><td valign="top">Pending Updates with CVEs<strong>**</strong></td><td valign="top">Total number of apps in your environment with CVEs that have outstanding updates on your devices</td></tr><tr><td valign="top">Hours saved</td><td valign="top">Total number of work-hours saved based on multiplying every update action by four hours, as that is the average amount of time it takes to do one update manually</td></tr></tbody></table>

**\*\*** Enterprise Premium only

**\*** Requires the PMPC Client to be installed - These tiles rely on device-level data reported by the PMPC Client. If you have a Premium license but have not installed the Client on your devices, no data will be reported and these tiles will appear empty. Once the Client is installed and devices begin reporting, the tiles will populate automatically.

## New Apps

The **New Apps** section shows apps we have added to the PMPC App Catalog in the past three months.

<figure><img src="../../.gitbook/assets/image (1684).png" alt="&#x27;New Apps&#x27; section" width="563"><figcaption></figcaption></figure>

Clicking **View All** opens the **App Catalog** and shows a filtered list of all apps added in the past three months.

{% hint style="info" %}
**Note**

The **New Apps** section only appears with the [Unmanaged Applications](home-page.md#unmanaged-applications) section when we have detected apps (based on [Discovery](../discovery/) data) that are unmanaged.

If no discovery data is detected, the [Latest Catalog Additions](home-page.md#latest-catalog-additions) section is shown instead of both the **New Apps** and **Unmanaged Applications** sections.
{% endhint %}

## Unmanaged Applications

The **Unmanaged Applications** section of the **Home** page shows apps we have detected (based on [Discovery data)](../discovery/) that are unmanaged my PMPC Cloud.

<figure><img src="../../.gitbook/assets/image (1685).png" alt="&#x27;Unmanaged Applications&#x27; section" width="563"><figcaption></figcaption></figure>

Clicking an unmanaged app opens its properties screen, allowing you to [deploy](../deployments/) it.

{% hint style="info" %}
**Note**

The **Unmanaged Applications** section only appears with the [New Apps](home-page.md#new-apps) section when we have detected apps (based on [Discovery](../discovery/) data) that are unmanaged.

If no discovery data is detected, the [Latest Catalog Additions](home-page.md#latest-catalog-additions) section is shown instead of both the **New Apps** and **Unmanaged Applications** sections.
{% endhint %}

## Latest Catalog Additions

If you have no Discovery data, the **Latest Catalog Additions** section is shown on the **Home** page instead of the [Unmanaged Applications](home-page.md#unmanaged-applications) section.

The **Latest Catalog Additions** section of the **Home** page shows apps we have added to the PMPC App Catalog.

<figure><img src="../../.gitbook/assets/image (1686).png" alt="&#x27;Latest Catalog Additions&#x27; section" width="563"><figcaption></figcaption></figure>

Any newly added items are marked as **New** for three months.

{% hint style="info" %}
**Note**

Multiple versions of the same app may appear separately because each version is treated as a distinct catalog item.
{% endhint %}

## Videos

The **Videos** section of the **Home** page contains links to various videos we have created.

Videos can be played directly on the **Home** page, and the player supports typical video playback and control options. This section auto-updates as we add content.

<figure><img src="../../.gitbook/assets/image (1687).png" alt="&#x27;Videos&#x27; section" width="563"><figcaption></figcaption></figure>

## News & Links

The **News & Links** section of the **Home** page contains two tabs:

* **Blog –** Contains a list of articles from our blog. Click an article to read the full article or click **View all posts** to open our blog in a new page.
* **News –** Contains the items from our [CVE Insights newsfeed](https://cveinsights.com/news) that are relevant to apps deployed in your environment. Click a news item to read the full article or click **View all news** to open our newsfeed in a new page.

<figure><img src="../../.gitbook/assets/image (1688).png" alt="&#x27;News &#x26; Links&#x27; section" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

This section auto-updates as we add content.
{% endhint %}

## Managed Apps Install States

The **Managed Apps Install States** section of the **Home** page shows the [Managed App Install States (Donut chart)](../insights-intune/about-dashboards/intune-page.md#managed-app-install-states-donut-chart), which provides a count of Windows and macOS managed app install states, based on data from Intune.

<figure><img src="../../.gitbook/assets/image (1689).png" alt="&#x27;Managed Apps Install States&#x27; section" width="563"><figcaption></figcaption></figure>

## License Information

The **License Information** section of the **Home** page gives you a clear overview of how many devices you are currently patching and how that compares to your subscriptions' device limit.

{% hint style="info" %}
**Note**

The **License Usage** tile displays the count of devices patched based on the following rules:

* If at least one deployment is assigned to **All Users** or **All Devices**, the tile displays the total number of Windows devices active within the last 21 days (macOS devices are excluded).
* If no deployments are assigned to **All Users** or **All Devices**, the device count is calculated separately for each deployed app by adding together the number of devices (in the following deployment states: Failed, Installed, Not Applicable, Not Installed, and Pending Install). The highest total across all apps is then used as the **Devices Patched** count.
* If no Deployments exist, the device count is **0**.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1676).png" alt=""><figcaption></figcaption></figure>



## Share Your Feedback

The **Share Your Feedback** section of the **Home** page provides links to independent, external review platforms so you can share your feedback about your Patch My PC experience.

<figure><img src="../../.gitbook/assets/image (1670).png" alt=""><figcaption></figcaption></figure>


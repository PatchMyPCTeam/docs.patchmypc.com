# Home page of the Patch My PC Cloud Portal

_Applies to: Patch My PC (PMPC) Cloud_

{% hint style="danger" %}
**PRIVATE PREVIEW**

This feature is currently only available through an invitation-only Private Preview, as both it and the documentation are under development, incomplete, and subject to change.

Please do not share links to these docs with others outside of the Private Preview.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

All Patch My PC (PMPC) Cloud management-related tasks are performed through the browser-based Cloud Portal. When you sign in to PMPC Cloud using the following link, you see the **Home** page.

[https://portal.patchmypc.com/](https://portal.patchmypc.com/)

The version of the **Home** page you see depends on your PMPC Cloud subscription type.

If you are an **Enterprise Plus** subscriber, you will see this version of the **Home** page:

<figure><img src="../../.gitbook/assets/image (183).png" alt="Enterprise Plus ‘Home’ page" width="563"><figcaption></figcaption></figure>

Whereas if you are an **Enterprise Premium** subscriber, you will see this version of the **Home** page:

<figure><img src="../../.gitbook/assets/image (186).png" alt="Enterprise Premium ‘Home’ page" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The differences between the **Home** page versions are explained below.
{% endhint %}

The Home page is split into the following tiled areas:

* [Environment Overview](home-page.md#environment-overview)
* [Latest Catalog Additions](home-page.md#latest-catalog-additions)
* [Videos](home-page.md#videos)
* [Documentation & Resources](home-page.md#documentation-and-resources)
* [Share Your Feedback](home-page.md#share-your-feedback)
* [License Information](home-page.md#license-information)

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

<figure><img src="../../.gitbook/assets/image (263).png" alt="‘Environment Overview’ section" width="563"><figcaption></figcaption></figure>

The **Environment Overview** section contains the following:

<table><thead><tr><th width="253.33331298828125" valign="top">Section</th><th valign="top">Shows the...</th></tr></thead><tbody><tr><td valign="top">Deployments Up to Date</td><td valign="top">Percentage of deployments that are up to date</td></tr><tr><td valign="top">Compliance Percentage<strong>*</strong></td><td valign="top"><p>Percentage of all managed apps in your environment that are up to date (i.e. every device has the latest version and there are no updates pending).</p><p> </p><p>This chart is shown instead of <strong>Deployments Up to Date</strong>.</p></td></tr><tr><td valign="top">Number of Deployments</td><td valign="top">Total number of deployments</td></tr><tr><td valign="top">Clients Deployed<strong>*</strong></td><td valign="top">Total number of PMPC Clients deployed instead of the Number of Deployments</td></tr><tr><td valign="top">Updates</td><td valign="top">Total number of app updates that PMPC published for any apps deployed over the last 12 months</td></tr><tr><td valign="top">Resolved CVEs</td><td valign="top">Total number of CVEs resolved in those updates over the last 12 months</td></tr><tr><td valign="top">Top 3 vulnerabilities resolved</td><td valign="top">Top three vulnerabilities resolved as part of the <em>Resolved CVEs</em> count</td></tr><tr><td valign="top">Most Vulnerable Apps<strong>*</strong></td><td valign="top"><p>Apps in your environment with known security vulnerabilities (CVEs), ranked by the highest CVE severity score and then by how many devices have the app installed, so you can prioritize which apps to patch first.</p><p> </p><p>This is shown instead of the <strong>Top 3 vulnerabilities resolved</strong></p></td></tr><tr><td valign="top">Devices Patched<strong>**</strong></td><td valign="top">Total number of devices that are patched</td></tr><tr><td valign="top">Pending Updates with CVEs<strong>**</strong></td><td valign="top">Total number of apps in your environment with CVEs that have outstanding updates on your devices</td></tr><tr><td valign="top">Hours saved</td><td valign="top">Total number of man-hours saved based on multiplying every update action by four hours, as that is the average amount of time it takes to do one update manually</td></tr></tbody></table>

&#x20;**\*\*** Enterprise Premium only

**\*** Requires the PMPC Client to be installed

## Latest Catalog Additions

The **Latest Catalog Additions** section of the **Home** page shows apps we have added to the PMPC App Catalog.

<figure><img src="../../.gitbook/assets/image (336).png" alt="‘Latest Catalog Additions’ section" width="563"><figcaption></figcaption></figure>

Any newly added items are marked as **New** for seven days.

If we detect that an app is unmanaged in your environment, it is flagged with the yellow circle indicator, as shown below.

<figure><img src="../../.gitbook/assets/image (337).png" alt="Unmanaged app detected" width="132"><figcaption></figcaption></figure>

Clicking an unmanaged app opens its properties screen, allowing you to [deploy it](../deployments/deploy-app/).

## Videos

The **Videos** section of the **Home** page contains links to various videos we have created.

Videos can be played directly on the **Home** page, and the player supports typical video playback and control options.

<figure><img src="../../.gitbook/assets/image (334).png" alt="‘Videos’ section" width="563"><figcaption></figcaption></figure>

## Documentation & Resources

The **Documentation & Resources** section of the **Home** page contains links to useful resources such as our support portal, product documentation, ideas and feedback portal, and learning hub.

<figure><img src="../../.gitbook/assets/image (273).png" alt="‘Documentation &#x26; Resources’ section" width="563"><figcaption></figcaption></figure>

## Share Your Feedback

The **Share Your Feedback** section of the **Home** page provides links to independent, external review platforms so you can share your feedback about your Patch My PC experience.

<figure><img src="../../.gitbook/assets/image (271).png" alt="‘Share Your Feedback’ section" width="563"><figcaption></figcaption></figure>

## License Information

The **License Information** section of the **Home** page shows useful licensing information.

If you are an Enterprise Plus customer, the **License Information** section shows you which Enterprise Premium features you are missing, which you can try out by clicking the **Free Trial** button.

If you already have an Enterprise Premium license, you can click the **Upgrade Now** button to upgrade your current PMPC Cloud Company to Enterprise Premium.

<figure><img src="../../.gitbook/assets/image (269).png" alt="‘License Information’ section" width="563"><figcaption></figcaption></figure>

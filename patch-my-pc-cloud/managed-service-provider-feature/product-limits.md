# Patch My PC Cloud Product Limits for Managed Service Provider Licenses

_Applies to: Patch My PC Cloud_

Managed Service Provider (MSP) Plus licenses of Patch My PC (PMPC) Cloud have the following limits depending on your license type, as detailed in the following table.

{% hint style="info" %}
**Note**

Non-MSP MSP licenses have different limits, as detailed in [Patch My PC Cloud Product Limits](../product-limits.md).
{% endhint %}

<table><thead><tr><th valign="top">Maximum Limit</th><th valign="top">MSP Parent</th><th valign="top">MSP Child</th></tr></thead><tbody><tr><td valign="top">Total no. of Custom Apps you can create</td><td valign="top">100</td><td valign="top">100</td></tr><tr><td valign="top">Total upload size of all files (including Custom App primary files + all additional files)</td><td valign="top">100 GB</td><td valign="top">100 GB</td></tr><tr><td valign="top">Total size of a single app (primary installer file + all additional files)</td><td valign="top">29.9 GB</td><td valign="top">29.9 GB</td></tr><tr><td valign="top">Total no. files that can be uploaded per app (including Custom App primary files + all additional files)<strong>*</strong></td><td valign="top">1,000</td><td valign="top">1,000</td></tr><tr><td valign="top">Total no. Publisher connections</td><td valign="top">5</td><td valign="top">5</td></tr><tr><td valign="top">Total no. Intune connections</td><td valign="top">1</td><td valign="top">1</td></tr><tr><td valign="top">Total no. deployments can create</td><td valign="top">1,000</td><td valign="top">1,000</td></tr><tr><td valign="top">Total no. deployments can create with extra files</td><td valign="top">25</td><td valign="top">25</td></tr><tr><td valign="top">Total no. macOS deployments can create</td><td valign="top">1,000</td><td valign="top">1,000</td></tr></tbody></table>

**\*** If you need to upload more than this limit for an app, create a ZIP file containing all of the files and upload this, but please note that if you upload a ZIP file, we do not automatically unzip it. See [How to package Visual Studio 2022 as a Custom App](https://patchmypc.com/kb/visual-studio-2022-custom/) for an example.

{% hint style="info" %}
**Note**

A Managed Service Provider (MSP) can create a maximum of 1,000 deployments for themselves and an additional 1,000 for each child company they manage.&#x20;

They can also create a maximum of 25 deployments with additional files for themselves and an additional 25 deployments with additional files for each child company they manage.
{% endhint %}

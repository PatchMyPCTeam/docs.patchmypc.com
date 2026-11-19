# "Overview" Page

{% hint style="info" %}
**Private Preview**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (1678).png" alt=""><figcaption></figcaption></figure>

The Overview page of Patch My PC Advanced Insights & Patch Insights for Intune shows the patching activity, vulnerability remediation, deployment performance, managed applications and estimated time savings for your PMPC Cloud Company over a selected reporting period. Use the page to review recent activity, investigate application and CVE detail, and export evidence of the value delivered by PMPC.&#x20;

{% hint style="info" %}
Note\
The Value of Time Saved is an estimate based on editable assumptions. It is not a measured saving. Period comparisons use the previous equivalent reporting period, not a baseline from before your organisation started using PMPC.
{% endhint %}

### Reporting period

The Overview page displays data for the last three months by default. Use the reporting-period control to select 1M, 3M, 6M, 1Y, YTD, Lifetime, or Custom. For a custom period, enter the start and end dates.

## Statistics

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Metric</td><td valign="top">What it shows</td></tr><tr><td valign="top">Updates Published</td><td valign="top">Updates delivered during the selected reporting period, including the change from the equivalent previous period and the number of affected apps.</td></tr><tr><td valign="top">Vulnerabilities Remediated</td><td valign="top">CVEs addressed by delivered updates, including Critical and High counts and the highest CVSS score in the period.</td></tr><tr><td valign="top">Value of Time Saved</td><td valign="top">An estimate calculated from updates delivered, hours per update and hourly rate. The assumptions can be adjusted to reflect your organisation.</td></tr><tr><td valign="top">Apps Under Management</td><td valign="top">Applications currently managed, with supporting device and publisher counts.</td></tr><tr><td valign="top">Deployment Success Rate</td><td valign="top">The percentage of successful deployments and the change from the previous equivalent period.</td></tr><tr><td valign="top">Highest CVSS in Period</td><td valign="top">The highest CVSS score recorded in the period, together with the related CVE and product.</td></tr><tr><td valign="top">Devices Fully Patched</td><td valign="top">Fully patched devices as a count and percentage of the devices in scope at the end of the period.</td></tr></tbody></table>

## Engineering Effort Avoided

This statistic estimates the manual packaging effort avoided during the selected period. The page calculates the estimate as:

<p align="center">Updates delivered x 3.5 hours per update</p>

## Report sections

Most Actively Updated Apps ranks applications by the number of releases during the selected period.

Products With Highest CVE Count highlights the products with the most CVEs. Product variants are combined so that a product is not listed more than once.

Deployed App Activity Summary compares updates, CVEs, and maximum CVSS for the selected period, the last 12 months, and lifetime.

Apps Being Deployed or Updated lists the applications in management today, including current version, platform, device count, and recent activity.

Detailed CVE Activity lists remediated CVEs, severity, CVSS, the update version that addressed each CVE, and the remediation date.

{% hint style="info" %}
Counting rule\
The application lists reflect applications in management today, regardless of when each application was first added. Historical values are calculated from catalog releases in the selected period.
{% endhint %}

## Filter and export data

Use the reporting-period control to apply a standard range, or select Custom and enter start and end dates.

Use the filters, search, and pagination controls within each section to focus on the records you need.

Select Download Report in the page header to create a shareable copy of the whole Overview page.

## Use the Overview page

Regular review - Select 3M to review recent update volume, deployment performance, and vulnerability remediation.

Annual or renewal review - Select 1Y, Lifetime, or a custom contract period, then export the page.

Focused investigation - Search Detailed CVE Activity for a CVE, application, or vendor, or filter the results by severity.

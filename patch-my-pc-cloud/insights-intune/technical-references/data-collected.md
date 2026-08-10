# Data Collected By Patch My PC Advanced/Patch Insights for Intune

_Applies to: Advanced/Patch Insights for Intune_

This article details the data collected by Patch My PC (PMPC) Advanced/Patch Insights for Intune using Microsoft Graph only.

## How Intune Data Collection Works

On the first time launch of a tab/dashboard view, a data caching process runs to collect data that populates the specific dashboard items. Intune data is requested by the customer from their tenant via a background task that sends a graph API POST request to the export reports endpoint.

Whilst report generation/processing is in process the following message is shown.

<figure><img src="../../../.gitbook/assets/image (4247).png" alt="Loading of Advanced Insights for Intune using Microsoft graph APIs" width="563"><figcaption></figcaption></figure>

Once the data export generation has completed for all requested reports, Advanced Insights for Intune processes the data export and stores the results in the database. The dashboard then loads fully.

{% hint style="danger" %}
**Important**

We store your Intune data in a secure database for a total of three (3) hours, after which it is automatically deleted from our systems.&#x20;
{% endhint %}

## Reports used

The data to populate the dashboards is obtained from the following two graph API endpoints:

1. **Export reports endpoint -** (/deviceManagement/reports/exportJobs)
2. **Live graph calls –** (/deviceManagement/)

The Export Reports used as of 15<sup>th</sup> April 2026 as shown below.

<table><thead><tr><th valign="top">Export Report Name</th><th align="center" valign="top">Devices dashboard</th><th align="center" valign="top">Applications dashboard</th><th align="center" valign="top">Compliance dashboard</th><th align="center" valign="top">Configuration dashboard</th><th align="center" valign="middle">Operating Systems dashboard</th></tr></thead><tbody><tr><td valign="top">DevicesWithInventory</td><td align="center" valign="top">X</td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="top">X</td><td align="center" valign="middle">X</td></tr><tr><td valign="top">DeviceEncryption</td><td align="center" valign="top">X</td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="top">X</td><td align="center" valign="middle">X</td></tr><tr><td valign="top">AllAppsList</td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="middle"> </td></tr><tr><td valign="top">AppInstallStatusAggregate</td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="middle"> </td></tr><tr><td valign="top">AppInvAggregate</td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="middle"> </td></tr><tr><td valign="top">PolicyNonComplianceAggVer3</td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="top"> </td><td align="center" valign="middle"> </td></tr><tr><td valign="top">PolicyComplianceAggReportV3</td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="top"> </td><td align="center" valign="middle"> </td></tr><tr><td valign="top">ConfigurationPolicyAggregate</td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="middle"> </td></tr><tr><td valign="top">UnhealthyDefenderAgents</td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="middle"> </td></tr><tr><td valign="top">AutopilotV1DeploymentStatus</td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top">X</td><td align="center" valign="middle"> </td></tr><tr><td valign="top">EAWFADeviceList</td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="top"> </td><td align="center" valign="middle">X</td></tr></tbody></table>

Live graph requests are used to populate device and application modal views, as well as a specific selection of individual dashboard items, which are noted in the preceding sections of this documentation.

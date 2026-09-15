---
description: 'Applies to: Patch My PC Advanced Insights for Configuration Manager'
---

# Advanced Insights "Threat Analytics" Dashboard

The Threat Analytics dashboard turns your Configuration Manager software update compliance data into a picture of CVE (Common Vulnerabilities and Exposures) risk. Instead of thinking in terms of individual updates, it lets a Configuration Manager administrator see which vulnerabilities are most prevalent and most severe across the estate, exactly which updates remediate each one, and whether those updates are already deployed and reaching compliance.

{% hint style="info" %}
Threat Analytics correlates published vulnerability intelligence with the updates your devices actually require. The CVE metadata; severity scores, affected products, remediating updates and notes, is sourced by the Patch My PC service from vendor and industry vulnerability feeds (including the Microsoft Security Response Center (MSRC), NIST and Red Hat). This is then matched against:

* the **Microsoft update manifest** (Microsoft security updates synchronised into Configuration Manager), and
* the **Patch My PC catalog** (third-party application updates).

A device is only counted against a CVE when Configuration Manager reports that it **requires** an update that remediates that CVE.
{% endhint %}

Because vulnerability exposure is evaluated across all managed devices, the **collection selector does not apply** to this dashboard (it shows _Collection Filter not applicable_). Results are still limited by your Role-Based Access Control (RBAC) scope.

### Summary statistics

| Statistic                      | Meaning                                                                                                                                                                |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Vulnerable Devices**         | The number of managed devices that require at least one update associated with a CVE, shown as a count and as a percentage of managed devices.                         |
| **Critical Devices**           | The subset of vulnerable devices that are exposed to a **critical** CVE (a CVE with a CVSS base score of 9 or higher).                                                 |
| **Microsoft Critical CVEs**    | The number of distinct critical (base score ≥ 9) Microsoft CVEs present in your environment. Click the tile for the full **Microsoft Critical CVEs** list (see below). |
| **Microsoft Critical Updates** | The number of critical Microsoft security updates needed to remediate those critical CVEs. Click the tile for more detail.                                             |

### Microsoft Common Vulnerability Exposure

The main table lists the Microsoft CVEs associated with updates that are **required by at least one device**. Each row is a vulnerability, ordered so the most widely exposed appear first.

| Column            | Description                                                                                                                                                                                                                                                                                        |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **CVRF**          | The Microsoft Common Vulnerability Reporting Framework release (month) the CVE was published in.                                                                                                                                                                                                   |
| **CVE**           | The CVE identifier.                                                                                                                                                                                                                                                                                |
| **Title**         | The vulnerability title.                                                                                                                                                                                                                                                                           |
| **Devices**       | The number of devices in scope that require a remediating update for this CVE.                                                                                                                                                                                                                     |
| **BaseScore**     | The CVSS base score and severity (for example, _9.8 (Critical)_).                                                                                                                                                                                                                                  |
| **TemporalScore** | The CVSS temporal score, which adjusts the base score for real-world factors such as exploit maturity and remediation availability.                                                                                                                                                                |
| **Vector**        | Hover the information icon to see the **processed vector string** broken down into plain language (attack vector, attack complexity, privileges required, user interaction, scope, confidentiality/integrity/availability impact, exploit code maturity, remediation level and report confidence). |

&#x20;Click any row to open the **CVE detail modal** (described below).

### Patch My PC Update Vulnerability Exposure

This table mirrors the Microsoft table but covers CVEs remediated by **Patch My PC catalog** (third-party application) updates required by at least one device — for example, browser and application vulnerabilities.

| Column             | Description                                                         |
| ------------------ | ------------------------------------------------------------------- |
| **CVE**            | The CVE identifier.                                                 |
| **CVETitle**       | The title of the affected product/update.                           |
| **CVEDescription** | The published description of the vulnerability.                     |
| **Devices**        | The number of devices requiring the remediating Patch My PC update. |
| **BaseScore**      | The CVSS base score and severity.                                   |
| **Vector**         | The processed vector string (hover the information icon).           |

### Cyber Essentials

The Cyber Essentials panel tracks **critical update compliance** against the 14-day patching expectation used by the Cyber Essentials scheme. It lists the critical updates that are still missing from one or more devices:

| Column         | Description                                                                                                           |
| -------------- | --------------------------------------------------------------------------------------------------------------------- |
| **ArticleID**  | The KB article for the update.                                                                                        |
| **DatePosted** | The date the update was released.                                                                                     |
| **Missing**    | The number of devices still missing the update.                                                                       |
| **Status**     | **Breached** when the update has been available for 14 days or more, **Warning** at 7 days or more, otherwise **OK**. |

This gives an at-a-glance view of whether critical patching is keeping pace with the timescales an assessment would expect.

### Microsoft Critical CVEs list

Clicking the **Microsoft Critical CVEs** statistic (or its _Click for more details_ banner) opens the full list of critical CVEs (base score ≥ 9). It behaves like the main table — CVRF, CVE, Title, Devices, BaseScore, TemporalScore — with a quick search box and the same **VectorString** hover breakdown.

### CVE detail modal

Clicking a CVE opens a modal with four tabs. Together they take you from _understanding_ the vulnerability to _knowing exactly what to do about it_.

#### Vulnerability tab

Shows the **Susceptible Products** — the products the vulnerability applies to — with the threat type (for example, _Remote Code Execution_), BaseScore, TemporalScore and vector. This is the published metadata describing the CVE.

#### Exposure tab

This is the tab that tells the administrator **what to do**. It shows only what is relevant to _your_ environment:

* **Exposed Devices** – the devices that actually require an update for this CVE, with computer name, user and online status. Checkboxes and a **Bulk Actions** menu let you act on selected devices.
* **Required Microsoft Security Updates** – the **subset** of the CVE's updates that are genuinely **required by at least one device in your environment**. Each update shows its title, how many devices **Required** it, and the current **Compliance (%)**.

{% hint style="success" %}
Start here. The Exposure tab filters out the noise and shows the specific updates that will remediate the CVE on the devices that need them, along with how close you already are to full compliance.
{% endhint %}

#### Remediations tab

Shows **all** Microsoft security updates referenced by this CVE — not just the ones your environment needs — with ArticleID, DateRevised, Title, and the **Installed**, **Required** and **Unknown** device counts plus **Compliance (%)**.

Because a single CVE is typically remediated across many operating systems, architectures and product versions, this list is usually long and **most rows will not be relevant to any one environment**. Rows can also appear as _not present in configuration manager_: this usually means the referenced update has been superseded or expired, or has not yet been synchronised into the Configuration Manager database.

#### Notes tab

Shows any additional notes published for the CVE (for example, mitigations or workarounds where the remediation is not simply a Microsoft security update). Where the Remediations tab is sparse, the Notes tab is often where the relevant guidance is found.

#### Understanding Compliance (%)

On both the Exposure and Remediations tabs, **Compliance (%)** for an update is calculated as the proportion of in-scope devices where the update is either already installed or not applicable:

$$\text{Compliance (\%)} = \frac{\text{Installed} + \text{Not Applicable}}{\text{Total in-scope devices}} \times 100$$

A low percentage on a required update highlights where deployment work remains; 100% means every relevant device is already remediated.

### Related data sources

For administrators who want to trace the dashboard back to source:

* CVE intelligence (scores, vectors, susceptible products, referenced KBs and notes) is provided by the Patch My PC service from vendor and industry feeds.
* Device exposure and update compliance are derived from Configuration Manager update compliance data (`fn_ListUpdateCIs`, `Update_ComplianceStatus`, `v_UpdateScanStatus`) for both Microsoft updates and the Patch My PC catalog.
* Critical thresholds use a CVSS base score of **9 or higher**; Cyber Essentials status uses the update's age since release (7-day warning, 14-day breach).

All figures are limited by your RBAC scope; the collection selector does not apply to this dashboard.

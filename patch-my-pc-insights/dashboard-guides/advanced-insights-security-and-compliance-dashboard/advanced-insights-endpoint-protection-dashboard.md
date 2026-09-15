---
description: 'Applies to: Patch My PC Advanced Insights for Configuration Manager'
---

# Advanced Insights Endpoint Protection Dashboard

{% hint style="info" %}
The Endpoint Protection dashboard reflects the antimalware health data that Configuration Manager already collects for its **Endpoint Protection Status** node. Advanced Insights reads this data directly from the ConfigMgr site database view v\_EndpointProtectionStatus and the EP\_Malware table - it does not recalculate or re-evaluate device health itself.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (1101).png" alt=""><figcaption></figcaption></figure>

Every panel on this dashboard is scoped by the **collection selector** at the bottom of each tile (for example, _All Desktop and Server Clients_) and is further limited by your Role-Based Access Control (RBAC) scope. Changing the collection re-runs the panel against only the members of that collection.

The dashboard is made up of four summary donut charts across the top and two monitoring panels below:

* **Endpoint Protection Status** – overall protection health for client devices
* **Definition File Age** – how current each device's antimalware definitions are
* **Last Scan Age** – how recently each device completed a scan
* **Detected Malware** – threats detected across the estate in the last 30 days
* **Malware Outbreak Monitoring** – detections and remediation results over the last 24 hours
* **Malware Activity on Devices** – a device-level list of detections in the last 30 days

***

### Endpoint Protection Status

This donut chart summarises the overall antimalware health of every device in the selected collection. Each device is placed into **exactly one** category, in the following priority order:

| Category          | Meaning                                                                                                      |
| ----------------- | ------------------------------------------------------------------------------------------------------------ |
| **Protected**     | The Endpoint Protection / Microsoft Defender client is installed and reporting a healthy state.              |
| **At Risk**       | The client is installed but is reporting one or more health problems (see below).                            |
| **Not Installed** | The device is a managed client but the Endpoint Protection client has not yet been installed.                |
| **Not Supported** | The device cannot run the managed Endpoint Protection client (for example, an unsupported operating system). |
| **Inactive**      | The device is a client but is currently flagged inactive in Configuration Manager.                           |
| **Not Client**    | The resource is not a Configuration Manager client.                                                          |
| **Unknown**       | No Endpoint Protection status could be matched for the device.                                               |

Clicking any segment of the donut opens a drill-through list of the devices in that category, showing the computer name, domain, primary user and online status. From there you can click an individual device to open its full device view.

#### Why is a device shown as "At Risk"?

This is the most common question we receive about this dashboard, so it is worth explaining in detail.

A device is counted as **At Risk** when its record in the Configuration Manager view v\_EndpointProtectionStatus is flagged as at risk (internally, the EpAtRisk value is greater than zero) **and** the device is not already classified as Protected. Because the categories are evaluated in priority order - Protected first - a device only appears as At Risk if ConfigMgr did **not** consider it healthy.

Advanced Insights does not decide what "At Risk" means. The classification is produced by Configuration Manager itself, from the health information the Endpoint Protection / Microsoft Defender agent reports back from each client. Advanced Insights simply displays the value ConfigMgr has already stored. This means the count here will always match the "At risk" count in the built-in ConfigMgr Endpoint Protection Status node for the same collection.

Configuration Manager rolls a device into the **At risk** state when the antimalware client reports one or more unhealthy conditions. Common examples include:

* **Real-time protection is disabled, turned off, or snoozed.**
* **Antimalware definitions (signatures) are out of date.** These are the same definitions summarised in the _Definition File Age_ chart.
* **A required scan is overdue or has not completed** — a full or quick scan is pending or has never run.
* **The antimalware engine or platform is out of date, has failed, or requires a restart to finish updating.**
* **Malware was detected but not fully remediated** — remediation is pending, requires a restart, requires manual steps, or failed.
* **The product or subscription has expired**, so the client is no longer receiving protection updates.

A device can be At Risk for more than one of these reasons at the same time. To find the specific reason for a given device, click the **At Risk** segment to list the affected devices, then open the device to review its Endpoint Protection detail (or review the same device in the ConfigMgr Endpoint Protection Status node / the device's Antimalware health information).

{% hint style="info" %}
Because the _Definition File Age_ and _Last Scan Age_ charts draw from the same ConfigMgr view, they are useful companions when investigating At Risk devices. A large "Over 7 days" definition group or "Over 31 days" scan group often overlaps heavily with the At Risk population.
{% endhint %}

***

### Definition File Age

This chart shows how current the antimalware definitions (signatures) are on each device in the collection. Devices are grouped by the age of their latest definition file:

* **No Signature** – no definition file has been reported.
* **Up to 1 day**, **Up to 3 days**, **Up to 7 days** – definitions updated within that window.
* **Over 7 days** – definitions are more than seven days old.

Definitions that are more than a few days old are a frequent contributor to devices appearing in the **At Risk** category, because out-of-date signatures cannot detect the newest threats. Clicking a segment lists the affected devices.

***

### Last Scan Age

This chart shows how recently each device completed an antimalware scan, grouped by age:

* **Up to 2 days**, **Up to 8 days**, **Up to 31 days** – last scan completed within that window.
* **Over 31 days** – no completed scan reported in more than 31 days.

A device that has not scanned in a long time may not have detected malware that is already present, and an overdue scan can also contribute to an **At Risk** status. Clicking a segment lists the affected devices.

***

### Detected Malware

This chart summarises the distinct threats detected across the selected collection in the **last 30 days**, sized by how many devices each threat was seen on. The example screenshot shows Tool:Win32/EICAR\_Test\_File, which is the industry-standard harmless test detection commonly used to confirm that antimalware and reporting are working end to end.

Clicking a threat drills through to the devices affected by that specific threat.

***

### Malware Outbreak Monitoring

This panel plots malware activity across the **last 24 hours**, broken down by hour. For each hour it shows:

* **Detections** – the total number of malware detections (the line/marker series).
* **Remediation Success** – detections that were successfully cleaned, quarantined, removed, blocked or otherwise actioned.
* **Remediation Failed** – detections where the remediation action did not succeed.

Use this panel to spot a sudden spike in detections that might indicate an outbreak, and to confirm at a glance whether those detections were successfully remediated.

***

### Malware Activity on Devices

This is a device-level table of every malware detection in the selected collection over the **last 30 days**. Columns include:

* **Remediation** – whether the remediation action succeeded (_Success_) or not (_Failed_).
* **Detected** – the local date and time of the detection.
* **ComputerName** – the affected device (with an online/offline indicator).
* **UserName** – the primary or top console user of the device.
* **ThreatName** – the detected threat.

You can quick-search, sort, page and export this list. Click a row to open the affected device, or to see the full remediation action and the file path of the detection.

***

### Related data sources

For administrators who want to trace these panels back to source, the dashboard is built from standard Configuration Manager objects:

* **Endpoint Protection Status**, **Definition File Age**, **Last Scan Age** – the v\_EndpointProtectionStatus view.
* **Detected Malware**, **Malware Outbreak Monitoring**, **Malware Activity on Devices** – the EP\_Malware table joined to the threat catalog views (v\_ThreatCatalog, v\_ThreatCategories, v\_ThreatSeverities).

All panels are additionally filtered by the selected collection and by your RBAC scope, so two administrators may see different totals for the same collection if their permitted scopes differ.

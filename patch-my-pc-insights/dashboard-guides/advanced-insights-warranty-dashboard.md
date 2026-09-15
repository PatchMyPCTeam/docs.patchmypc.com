---
description: 'Applies to: Patch My PC Advanced Insights for Configuration Manager'
---

# Advanced Insights "Warranty" Dashboard

<figure><img src="../../.gitbook/assets/image (1108).png" alt=""><figcaption></figcaption></figure>

The Warranty dashboard shows the manufacturer warranty status of your managed hardware - which devices are in warranty, expiring, expired, or have no warranty data available - together with a timeline of upcoming expiries and a breakdown by vendor.

Unlike most Advanced Insights dashboards, warranty information does not come fro m Configuration Manager. It is retrieved by the **Patch My PC warranty service**, which looks up each device's serial number against the hardware vendor's warranty API and **caches** the result in a local SQLite database on the Advanced Insights server. The dashboard reads from that cache.

### Before you start: configure warranty

{% hint style="warning" %}
The Warranty dashboard is empty until warranty lookups have been enabled, credentials have been supplied, and at least one caching run has completed. Warranty caching **must** be enabled, the dashboard cannot be used without it.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1109).png" alt=""><figcaption></figcaption></figure>

Warranty is configured under **Administration → Settings → External Services → Warranty**:

* **Enabled** – allows warranty data to be retrieved from the vendor APIs.
* **Enable Warranty Caching** – stores the retrieved data locally so it can populate the dashboard. The dashboard requires this to be enabled.

You then supply the API credentials for each vendor you use. Credentials are stored **encrypted**.

| Vendor     | Required credentials                                                                                                                                                                                                                                  |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Dell**   | Dell API **Client ID** and **Client Secret**.                                                                                                                                                                                                         |
| **Lenovo** | Lenovo API **Client Token**.                                                                                                                                                                                                                          |
| **HP**     | HP warranty collection is supported **only through HP Workforce Experience (WeX)** — the legacy HP Warranty API is not supported. Select whether you are a **US** or **EU** based customer, then provide the WeX **Client ID** and **Client secret**. |

{% hint style="info" %}
For the steps to obtain each vendor's credentials, see the dedicated external-services documentation:

* Dell Warranty API
* Lenovo Warranty API
* HP Warranty (Workforce Experience)

If your organisation routes external traffic through a proxy, configure it in the **Network Proxy** section on the same page. Changing proxy settings requires a restart of the Advanced Insights API website on the server before they take effect.
{% endhint %}

Only physical devices from supported vendors are looked up. Virtual machines (for example VMware, Hyper-V "Virtual" models and Nutanix AHV) are excluded.

### Summary statistics

#### Bulk Processing

The **Bulk Processing** tile controls and reports on the caching job that populates the whole dashboard. It shows the current **Status** (for example, _Not currently processing_ or actively processing), a progress bar, the **Last ran** date and time, and how long the last run took.

{% hint style="info" %}
**To refresh the warranty data, click the Bulk Processing tile.** This starts a new caching run that re-queries the vendor APIs for your devices and updates the local cache. Because it calls external APIs for every device, a run can take some time; the tile shows progress and, once finished, the new "Last ran" timestamp. Bulk Processing is a server-wide operation — it is not limited by the collection selector.
{% endhint %}

#### Unknown Devices

The number of devices for which **no warranty data is available,** i.&#x65;**.** the vendor lookup did not return a result. The progress line shows how many devices _do_ have warranty data (for example, _warranty data for 15 of 25 devices_, 60%).

A device is **Unknown** when the warranty service could not obtain a result for it. Common reasons include:

* The device is from a **manufacturer that is not supported** (only Dell, Lenovo, Toshiba/ProBook and HP via WeX are looked up).
* **Credentials for that vendor have not been configured**, so its devices cannot be queried.
* The device's **serial number is missing or not recognised** by the vendor.
* The device **has not been processed yet** — it was added since the last caching run. Click **Bulk Processing** to run a fresh lookup.

#### Expired Warranties

The number of devices that are **out of warranty**. The progress line shows how many devices are currently in warranty (for example, _0 of 25 devices are in warranty_).

#### Expiring within 30 days

The number of in-warranty devices whose warranty **ends within the next 30 days**. Click the tile for more detail. This is a deliberately short, action-focused window — note that it uses a different threshold to the "Expiring Soon" slice of the Warranty Status chart below (which uses six months).

### Warranty Expiration

This chart plots warranty expiries across a rolling window (by default roughly ±18 months), grouped by month. Use the slider above the chart to zoom into a narrower time range. Each month's devices are coloured by state:

* **Expired** – warranties that have already ended.
* **This Month** – warranties ending in the current month.
* **Expiring** – warranties ending soon (within six months).
* **In Warranty** – warranties ending further out (more than six months away).

Use this view to plan hardware refresh budgets and spot clusters of devices coming out of warranty at the same time.

### Warranty Status

A donut chart summarising the warranty state of processed devices in the selected collection:

| Status              | Meaning                                                                                   |
| ------------------- | ----------------------------------------------------------------------------------------- |
| **In Warranty**     | The device is in warranty and its latest warranty end date is more than six months away.  |
| **Expiring Soon**   | The device is in warranty but its latest warranty end date is within the next six months. |
| **Out of Warranty** | The device's warranty has ended.                                                          |
| **Unknown**         | No warranty result is available for the device (see _Unknown Devices_ above).             |

This chart is scoped by the **collection selector** beneath it and by your RBAC scope.

### Warranty vendors

A donut chart breaking down processed devices by **manufacturer**, so you can see the vendor mix of your estate at a glance. Devices whose manufacturer could not be determined are grouped as _Unknown_. This chart is also scoped by the collection selector.

### Warranty data

A device-level table of all available warranty data for the selected collection. You can quick-search, sort, filter each column, page through the results and export the list.

| Column             | Description                                                                     |
| ------------------ | ------------------------------------------------------------------------------- |
| **WarrantyStatus** | In Warranty, Expiring Soon, Out of Warranty or Unknown (as defined above).      |
| **ComputerName**   | The device name.                                                                |
| **Username**       | The primary or top console user of the device.                                  |
| **Serial**         | The hardware serial number used for the warranty lookup.                        |
| **Manufacturer**   | The device manufacturer.                                                        |
| **Model**          | The device model (Lenovo devices show the friendly model name where available). |
| **ShipDate**       | The manufacturer ship date, where the vendor provides it.                       |
| **StartDate**      | The start date of the latest warranty.                                          |
| **EndDate**        | The end date of the latest warranty.                                            |

Where a device has multiple warranty entries, the dashboard uses the **latest** warranty end date to determine its status and the dates shown.

### Related data sources

Warranty data is held in a local SQLite database on the Advanced Insights server, populated by the Patch My PC warranty service:

* Device inventory sent for lookup is drawn from Configuration Manager(v\_GS\_COMPUTER\_SYSTEM, v\_GS\_COMPUTER\_SYSTEM\_PRODUCT, v\_GS\_PC\_BIOS), excluding virtual machines.
* Cached warranty results are stored in the CalDevice, CalWarrantyResult, CalWarrantyInfo and related tables and are refreshed when you run Bulk Processing.

The status donut, vendor donut, expiration chart and data table are scoped by the selected collection and by your RBAC scope; the Bulk Processing job runs server-wide.

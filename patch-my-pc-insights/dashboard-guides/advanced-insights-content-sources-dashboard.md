---
description: 'Applies to: Patch My PC Advanced Insights for Configuration Manager'
---

# Advanced Insights "Content Sources" Dashboard

<figure><img src="../../.gitbook/assets/image (1110).png" alt=""><figcaption></figcaption></figure>

The Content Sources dashboard answers a question that is normally very hard to see in Configuration Manager: **where are my clients actually downloading their content from?** For the last 30 days it shows how much content each client pulled, broken down by the source that served it — an on-premises distribution point, a peer, Windows BranchCache, Delivery Optimization, or directly from Microsoft — and lets you drill all the way down to individual devices, hosts and content items.

This makes it easy to see the **impact of peer caching**, spot **fall-back to Microsoft** (content pulled from the internet instead of a local source), and understand **which distribution points and peers are serving which clients**.

Every panel is controlled by **two selectors**:

* a **collection selector** (for example, _All Desktop and Server Clients_), and
* a **location / boundary group selector** (shown as _Everywhere_ by default). This lets you narrow the view to a specific boundary group, to all internet clients, or to clients not associated with any boundary group.

All panels are additionally limited by your Role-Based Access Control (RBAC) scope, and all figures cover the **last 30 days**.

### Content source types

Throughout the dashboard, content is attributed to one of the following sources:

| Source                 | What it means                                                                                                                                                                                                |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Distribution Point** | Content served by an on-premises Configuration Manager distribution point.                                                                                                                                   |
| **Cloud DP**           | Content served by a cloud distribution point / cloud management gateway.                                                                                                                                     |
| **Microsoft**          | Content pulled directly from Microsoft over the internet (Windows Update / Microsoft Update / Delivery Optimization cloud). High values here indicate **fall-back to Microsoft** rather than a local source. |
| **Peer Cache**         | Content served by another client acting as a Configuration Manager Peer Cache source.                                                                                                                        |
| **BranchCache**        | Content shared between clients using Windows BranchCache.                                                                                                                                                    |
| **DO Peer**            | Content shared by another device through Delivery Optimization peer-to-peer.                                                                                                                                 |
| **DO Server**          | Content served by a Delivery Optimization server source (for example, Microsoft Connected Cache).                                                                                                            |

### Summary statistics

The four tiles across the top show the total volume of content served by the key sources over the last 30 days, each with the approximate percentage of the overall total downloaded:

| Statistic              | Meaning                                                                                             |
| ---------------------- | --------------------------------------------------------------------------------------------------- |
| **Distribution Point** | Total volume served by on-premises distribution points.                                             |
| **Cloud DP**           | Total volume served by cloud distribution points.                                                   |
| **Microsoft**          | Total volume pulled directly from Microsoft.                                                        |
| **Peer Cache**         | Total volume served by peer cache clients — a measure of how much bandwidth peer caching is saving. |

### Client Content by Source

A donut chart summarising the total content volume for the selected collection and location, broken down by source type. It gives an at-a-glance picture of how much of your content delivery is local (distribution points, peers, BranchCache) versus pulled from Microsoft.

The two dropdowns beneath the donut are the collection and location selectors described above.

### Client Content by Date

A stacked chart of daily client download activity over the last 30 days, with each source type as a coloured series (Cloud DP, Peer Cache, Distribution Point, Microsoft, BranchCache, DO Peer, DO Server) and a **Total** line across the top. Use the slider above the chart to zoom into a shorter time range, and hover any day to see the exact megabytes served by each source that day.

This is the best view for spotting patterns — for example a spike in **Microsoft** downloads on a patch-release day, or how much **DO Peer** traffic offsets distribution point load.

#### Drilling into the detail

<figure><img src="../../.gitbook/assets/image (1111).png" alt=""><figcaption></figcaption></figure>

Clicking into the **Client Content by Date** panel opens the **Client Content by Date** detail modal with five tabs, letting you look at the same 30 days of activity from different angles:

| Tab          | What it shows                                                                                                                                                                                                                                                                                                                                     |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Content**  | Each distinct item of content downloaded — Description, **Type**, the number of **Clients** that downloaded it, and the **Total** volume. Content that cannot be matched to a known object appears as _Unknown/Orphaned Content_.                                                                                                                 |
| **Devices**  | Each client device (**ComputerName**), the **Total** content it downloaded, and the **HostName** it downloaded from — the quickest way to see which clients are pulling from MICROSOFT.COM versus a local distribution point or peer.                                                                                                             |
| **Type**     | A roll-up of downloaded volume by content **Type** — for example Update, 3rdPartyUpdate, Application, Package and Other.                                                                                                                                                                                                                          |
| **Host**     | A summary of data served by each **HostName**, with **IsDPServer** and **IsClient** flags, the **ClientVersion** where the host is a client, and the **Total** volume served. This makes it obvious which distribution points carried the load and how much came from MICROSOFT.COM or aggregate peer sources such as Deliver Optimization Peers. |
| **Activity** | The full, row-level client activity: **ComputerName**, **Technology** (source type), **Host**, **Type**, **Description** and **Total** for every download event.                                                                                                                                                                                  |

Every tab supports quick search, column sorting and filtering, paging and export, so you can answer questions such as "which devices fell back to Microsoft for the latest cumulative update?" or "which distribution point served the most content this month?".

<figure><img src="../../.gitbook/assets/image (1112).png" alt=""><figcaption></figcaption></figure>

### Related data sources

For administrators who want to trace the dashboard back to source:

* Download activity comes from the ConfigMgr ClientDownloadHistory, ClientDownloadHistorySources and ClientDownloadHistoryBoundaryGroups data.
* Each download is attributed to a source using its distribution point type (1 = Cloud DP, 3 = Peer Cache, 4 = Distribution Point, 5 = BranchCache, 6 = DO Peer, 7 = DO Server, 8 = Microsoft).
* Volumes are reported in megabytes and rolled up to GB/TB for display.

All figures are limited by the selected collection, the selected location / boundary group, and your RBAC scope.

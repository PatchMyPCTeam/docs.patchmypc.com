---
description: 'Applies to: Patch My PC Advanced Insights for Configuration Manager'
---

# Page 1

{% hint style="info" %}
This dashboard reports on Configuration Manager **classic Packages** (package type 0) only, it does not include Applications, Driver Packages, Boot Images, OS Images, or Software Update Packages. The built-in Configuration Manager client upgrade and piloting packages are also excluded so the counts reflect the packages you manage. Data is read directly from the ConfigMgr site database, so the totals match the Packages node in the Configuration Manager console.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (1103).png" alt=""><figcaption></figcaption></figure>

The dashboard is made up of a row of summary statistics at the top and a detailed **Packages** table below. Unlike most dashboards, the statistics here are not scoped by a device collection, a package is a site-wide object, so the counts describe every classic package in your permitted RBAC scope.

### Summary statistics

Each statistic is clickable and opens a list of the packages it counts. The colour of a tile indicates whether the condition is informational (grey), worth reviewing (amber), or a potential problem (red).

| Statistic             | Meaning                                                                                                                                                                                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **All packages**      | The total number of classic packages in your scope.                                                                                                                                                                                                    |
| **Not Distributed**   | Packages that are not distributed to any distribution point (they have no targeted DPs). Devices cannot install content that has not been distributed.                                                                                                 |
| **Local Source Path** | Packages whose source path is a **local** path on the site server (not a UNC `\\server\share` path). Local source paths are fragile — the content can be lost if the server is rebuilt and is harder to migrate — so these are highlighted for review. |
| **Scheduled Update**  | Packages configured with a content **refresh schedule**. These periodically re-evaluate and redistribute their source content, which can generate recurring content processing on your infrastructure.                                                 |

### Packages table

The table lists every classic package in scope. You can quick-search, sort, filter each column, page through the results and export the list.

| Column              | Description                                                                                                                                                        |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **PkgID**           | The Configuration Manager Package ID.                                                                                                                              |
| **Manufacturer**    | The manufacturer recorded on the package (shows `N/A` when not set).                                                                                               |
| **PackageName**     | The package name.                                                                                                                                                  |
| **Version**         | The package version, where one is recorded.                                                                                                                        |
| **Size (MB)**       | The source content size. Blank where the package has no source content.                                                                                            |
| **Deployments**     | The number of deployments (advertisements) that reference the package.                                                                                             |
| **TaskSequences**   | The number of task sequences that reference the package.                                                                                                           |
| **Distributed**     | Distribution progress as _installed of targeted_ distribution points (for example, `2 of 2`).                                                                      |
| **Distributed (%)** | The same progress as a percentage, shown as a progress bar. A package sitting below 100% has not finished distributing to all of its targeted distribution points. |

A package showing 0 distributed with no targeted distribution points is the same population counted by the **Not Distributed** statistic above.

### Package detail

<figure><img src="../../../.gitbook/assets/image (1104).png" alt=""><figcaption></figcaption></figure>

Clicking a package opens its detail view, which has three tabs:

* **General** – core properties of the package: Package ID, Source Version and Source Version Date, Package Name, Size, Manufacturer, Version, Source Path and Description. Alongside this a **Distribution Points** panel lists each distribution point (ServerName), its content **InstallStatus** (for example, _Package Installation complete_) and the **SummaryDate** the status was last reported. This is the quickest way to see exactly which distribution point a package has failed to reach.
* **Programs** – the programs (command lines) defined on the package.
* **Deployments** – the deployments that target the package.

### Related data sources

For administrators who want to trace the dashboard back to source, it is built from standard Configuration Manager objects:

* Package properties and counts – fn\_rbac\_Package (filtered to PackageType = 0).
* Distribution progress and per-DP status – v\_PackageStatusRootSummarizer and the package distribution status views.
* Deployment and task sequence counts – v\_Advertisement and v\_TaskSequencePackageReferences.

All figures are limited by your RBAC scope, so two administrators may see different totals if their permitted scopes differ.

---
description: Network port and IIS Application Pool Identity
---

# Insights IIS Configuration selection

_Applies to: Patch My PC Advanced Insights_

Advanced Installer will create two websites and related application pools. The Dashboard website (_Advanced Insights Frontend_) is the site you will access to view dashboards and reports, the other site (_Advanced Insights Api_) is internally referenced only.

> Ensure the network requirements are reviewed here: \[insights-network-requirements.md]\(../advanced-and-patch-insights-requirements-and-prerequisites/insights-network-requirements.md "mention")

The IIS Configuration page allows you to set the dashboard port and IIS application pool identity to your requirements. The port is what will be used when browsing the portal (e.g., _https://adv01.contoso.com:444_). The API port is read-only. Firewall rules will be automatically created for the dashboard, and API websites.

> The installer will automatically recommend the best available port for the dashboard website. You can change this if you wish.

The IIS Application Pool identity used for both the Advanced Insights Frontend and Api application pools is 'LocalSystem' by default. An alternative identity (Active Directory account) can be used if required. More details on IIS application pool identity here: [advanced-insights-iis-application-pool-identity.md](../advanced-insights-iis-application-pool-identity.md "mention")

> When setting a custom ID for the IIS application pools, you must ensure the Active Directory account being used has the required SQL permissions to the Configuration Manager database. See: \[insights-sql-permission-requirements.md]\(../insights-sql-permission-requirements.md "mention")

**Examples:**

In this example, the installer automatically determined that the best available port was 444. IIS Application Pool left as default 'LocalSystem'.

![Example](/_images/image-(4336).png)

In this example a custom IIS application pool identity has been set:

![IIS app pool set](/_images/image-(4337).png)

Confirm the required Dashboard Port and if required, IIS application pool identity and click **Next**.

> \*\*Note\*\*
>
> If you have any feedback or comments on our docs, please email \[docs@patchmypc.com]\(mailto:docs@patchmypc.com).
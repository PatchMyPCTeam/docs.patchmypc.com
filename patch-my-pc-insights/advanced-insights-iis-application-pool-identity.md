---
description: Advanced Insights IIS Application Pool Identity
---

# Advanced Insights IIS Application Pool Identity

_Applies to: Patch My PC Advanced Insights_

Starting with version 2.4.1, the installation of Advanced Insights supports the configuration of a custom IIS Application Pool identity. A default installation of Advanced Insights sets 'LocalSystem' as the identity for both the Advanced Insights Api and Frontend IIS application pools.

A custom identity (Active Directory account) can be set as part of the installation either for a new install or upgrade. When using a custom identity, the account is also granted full control file system permissions on the following directory path: _C:\ProgramData\AdvancedInsights._

See - [insights-iis-configuration-selection.md](download-and-install-insights/insights-iis-configuration-selection.md "mention")

The IIS application pool identity can also been modified for existing installs too.

See - [modify-insights-iis-app-pool-identity.md](modify-insights/modify-insights-iis-app-pool-identity.md "mention")
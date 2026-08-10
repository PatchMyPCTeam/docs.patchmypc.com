# Overview of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Patch My PC (PMPC) Publisher is our on-premises publishing service that automates the creation, update, and lifecycle management of third-party applications and updates for Microsoft management platforms such as Configuration Manager (ConfigMgr), WSUS, and Intune.

Publisher integrates with:

* Microsoft Windows Server Update Services (WSUS)
* Microsoft Configuration Manager (ConfigMgr)
* Microsoft Intune

It allows organizations to deploy and maintain third-party software using the same native workflows they already use for Microsoft updates and applications.

![Patch My PC Publisher](/_images/image-(4743).png)

## Capabilities

Publisher downloads the Patch My PC catalog to retrieve curated metadata for third-party applications. Based on your configuration, it can:

* Publish third-party updates to WSUS.
* Create and update applications in ConfigMgr.
* Create and update Win32 apps (and updates) in Intune.
* Maintain and update previously published third-party applications and updates.

All publishing actions respect the target platform's native security, authentication, and deployment mechanisms.

Publisher does not replace WSUS, ConfigMgr, or Intune. It extends them by automating third-party application packaging and update publishing.
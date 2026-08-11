# WSUS Software Requirements for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Patch My PC (PMPC) Publisher's support for Microsoft Windows Server Update Services (WSUS) depends on the:

* [Operating system](software.md#operating-system)
* [WSUS Role](software.md#wsus-role)

## Operating System

Publisher depends on the underlying Windows Server operating system version.

Publisher supports WSUS when it is installed on Windows Server versions within Microsoft’s supported lifecycle.

The table below reflects WSUS support based on the Windows Server operating system version.

<table><thead><tr><th valign="top">Platform</th><th valign="top">Core WSUS API Support</th><th valign="top">Full WSUS Server Role Support</th></tr></thead><tbody><tr><td valign="top">Windows 11</td><td valign="top">Supported</td><td valign="top">Not Supported</td></tr><tr><td valign="top">Windows Server 2012</td><td valign="top">Not Supported</td><td valign="top">Not Supported</td></tr><tr><td valign="top">Windows Server 2016</td><td valign="top">Supported</td><td valign="top">Supported</td></tr><tr><td valign="top">Windows Server 2019</td><td valign="top">Supported</td><td valign="top">Supported</td></tr><tr><td valign="top">Windows Server 2022</td><td valign="top">Supported</td><td valign="top">Supported</td></tr><tr><td valign="top">Windows Server 2025</td><td valign="top">Supported</td><td valign="top">Supported</td></tr></tbody></table>

> \*\*Important\*\*
>
> Installing WSUS on operating systems that are no longer supported by Microsoft is not supported.
>
> Publishing to WSUS requires a supported Windows Server operating system with the WSUS role installed. Windows 11 is supported only for standalone Intune publishing and requires the WSUS UpdateServices API provided by the RSAT WSUS tools for catalog read operations. See \[Intune Software Requirements]\(../intune-requirements/software.md) for more information.

## WSUS Role

Before enabling third-party patching with Publisher, WSUS must be correctly installed and configured. In ConfigMgr environments, WSUS should already be installed as part of the initial configuration of a Software Update Point (SUP) role.

While this document does not cover how to install WSUS, it’s important to understand what the WSUS server role installs and the supporting components it relies on, especially when preparing an environment for third-party patching with Publisher.

> \*\*Note\*\*
>
> See [Deploy Windows Server Update Services](https://learn.microsoft.com/en-us/windows-server/administration/windows-server-update-services/deploy/deploy-windows-server-update-services) for more information on how to install the WSUS role in a WSUS-standalone environment and [Install and configure a software update point](https://learn.microsoft.com/en-us/intune/configmgr/sum/get-started/install-a-software-update-point) for information on how to install WSUS by way of configuring the SUP site system role in ConfigMgr.

When the WSUS role is installed either standalone or as part of a ConfigMgr SUP, it automatically deploys and configures several core components required for update publishing, synchronization, and client scanning.

WSUS is installed through **Server Manager** and requires the following components:

* **Windows Server Update Services (WSUS)** role - required to host update metadata and content.
* **RSAT Management tools**
  * Windows Server Update Services Tools
    * WSUS Management Console (MMC snap-in)
    * Supporting PowerShell and administrative components

![WSUS Roles and Features](/_images/image-(384 "WSUS Roles and Features") (1).png>)
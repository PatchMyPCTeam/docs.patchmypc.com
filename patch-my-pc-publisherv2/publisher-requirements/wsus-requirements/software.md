# Software

_Applies to: Patch My PC Publisher V2.x_

## Operating System

WSUS support is dependent on the underlying Windows Server operating system version.

The Publisher supports WSUS when it is installed on Windows Server versions that are within Microsoft’s supported lifecycle.

The table below reflects WSUS support based on the Windows Server operating system version.

| Platform            | Core WSUS API Support | Full WSUS Server Role Support |
| ------------------- | --------------------- | ----------------------------- |
| Windows 11          | Supported             | Not Supported                 |
| Windows Server 2012 | Not Supported         | Not Supported                 |
| Windows Server 2016 | Supported             | Supported                     |
| Windows Server 2019 | Supported             | Supported                     |
| Windows Server 2022 | Supported             | Supported                     |
| Windows Server 2025 | Supported             | Supported                     |

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>WSUS installed on operating systems that have reached end of support from Microsoft is not supported.</p>
<p>Publishing to WSUS requires a supported Windows Server operating system with the WSUS role installed. Windows 11 is supported only for standalone Intune publishing and requires the WSUS UpdateServices API provided by the RSAT WSUS tools for catalog read operations. See [Intune Software Requirements](../intune-requirements/software.md) for more information.</p>
</blockquote>

## WSUS Role

Before enabling third-party patching with the Publisher, Windows Server Update Services (WSUS) must be correctly installed and configured. In ConfigMgr environments, WSUS should already be installed as part of the initial configuration of a Software Update Point (SUP) role.

While this doc does not cover how to install WSUS, it’s important to understand what the WSUS server role installs and the supporting components it relies on, especially when preparing an environment for third-party patching with the Publisher.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>For more information on how to install the WSUS role in a WSUS-standalone environment, see <a href="https://learn.microsoft.com/en-us/windows-server/administration/windows-server-update-services/deploy/deploy-windows-server-update-services">https://learn.microsoft.com/en-us/windows-server/administration/windows-server-update-services/deploy/deploy-windows-server-update-services</a></p>
<p>For information on how to install WSUS by way of configuring the SUP site system role in ConfigMgr, see <a href="https://learn.microsoft.com/en-us/intune/configmgr/sum/get-started/install-a-software-update-point">https://learn.microsoft.com/en-us/intune/configmgr/sum/get-started/install-a-software-update-point</a></p>
</blockquote>

When the WSUS role is installed, either standalone or as part of a ConfigMgr SUP, it automatically deploys and configures several core components required for update publishing, synchronization, and client scanning.WSUS is installed through Server Manager and requires the following components:

* **Windows Server Update Services (WSUS)** role\
  This is the core role required to host update metadata and content.
* **RSAT Management tools**
  * Windows Server Update Services Tools
    * WSUS Management Console (MMC snap-in)
    * Supporting PowerShell and administrative components

![WSUS Roles and Features](/_images/image-(384).png "WSUS Roles and Features")
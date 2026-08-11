# Software

_Applies to: Patch My PC Publisher V2.x_

## Overview

The Publisher can be installed on either a Windows client or Windows Server operating system (see [Core Requirements](../core-requirements.md)) when publishing applications and updates solely to Microsoft Intune. However, even in Intune-only scenarios, particularly when the Publisher is installed on a Windows client operating system, specific WSUS components are still required. These components provide the WSUS API functionality needed to process and deserialize the update catalog format usedby Patch My PC.

{% hint style="success" %}
**Tip**

Some organizations have strict security or operational requirements that mandate the use of the Publisher instead of Patch My PC Cloud, or require separation of duties between Intune and ConfigMgr/WSUS administration teams. In these cases, it is fully supported to deploy a separate instance of the Publisher dedicated solely to Intune publishing, even if another Publisher instance already exists for WSUS or ConfigMgr.&#x20;

This approach aligns with least-privilege principles, allowing permissions, credentials, and administrative access to be scoped specifically to the Intune publishing workflow.
{% endhint %}

{% hint style="warning" %}
**Important**

The Publisher **does not need to be installed on each device** receiving applications or updates from Intune.

The Publisher is used only to publish applications and updates into Intune. Once published, delivery, installation, and enforcement on client devices is handled entirely by the Intune Management Extension (IME), which is already automatically installed on Intune-managed Windows devices.

Installing the Publisher on individual client devices **is not required** and provides no benefit for application or update deployment.
{% endhint %}

## Windows Server Operating System

If the Publisher is already being used with ConfigMgr and/or WSUS, and the same Publisher instance will also be used for Intune, the software requirements for [ConfigMgr](../configmgr-requirements/software.md) or [WSUS](../wsus-requirements/software.md) will already satisfy the WSUS API component requirements to publish to Intune.

If the Publisher is being used exclusively for Intune, a full WSUS role installation is not required. In this case, only the WSUS API components must be installed to allow Publisher to process update metadata and interact with WSUS libraries used during publishing. The steps below explain how to install the required components for this scenario.

### Install the WSUS UpdateServices API

1. Open an **elevated PowerShell** window.
2. Run the following command:

```powershell
Install-WindowsFeature UpdateServices-API
```

3. To confirm the UpdateServices API is installed, run:

```powershell
Get-WindowsFeature UpdateServices-API
```

The feature should show as **Installed**.

<figure><img src="../../../.gitbook/assets/image (389).png" alt="Get-WindowsFeature UpdateServices-API" width="563"><figcaption></figcaption></figure>

## Windows Client Operating System

When installing the Publisher on a Windows 11 device, which is typical for Intune-only publishing scnearios, the WSUS RSAT tools must be installed. A full WSUS role installation is _not_ required. If the RSAT tools are not installed, you will see the following messaage when [installing the Publisher](../../download-and-install.md).

<figure><img src="../../../.gitbook/assets/image (390).png" alt="WSUS RSAT tools missing" width="272"><figcaption></figcaption></figure>

The steps below explain how to install the required components for this scenario.

### Install WSUS RSAT Tools

1. Open an **elevated PowerShell** window.
2. Run the following command:

```powershell
Add-WindowsCapability -Online -Name Rsat.WSUS.Tools~~~~0.0.1.0
```

3. To confirm the WSUS RSAT tools were installed successfully, run:

```powershell
Get-WindowsCapability -Online -Name Rsat.WSUS.Tools~~~~0.0.1.0
```

The output should show the capability state as **Installed**.

<figure><img src="../../../.gitbook/assets/image (391).png" alt="Get-WindowsCapability -Online -Name Rsat.WSUS.Tools~~~~0.0.1.0" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

It is typicall for the download and installation of the WSUS RSAT tools to take \~15 minutes. Review `C:\Windows\Logs\CBS\CBS.log` and `C:\Windows\Logs\DISM\dism.log` for the download and installation progress.
{% endhint %}

# Software

_Applies to: Patch My PC Publisher V2.x_

## Operating System

The Publisher supports ConfigMgr when it is installed on Windows Server versions that are within Microsoft’s supported lifecycle.

The table below reflects ConfigMgr support based on the Windows Server operating system version.

| Platform            | Support State |
| ------------------- | ------------- |
| Windows Server 2012 | Not Supported |
| Windows Server 2016 | Supported     |
| Windows Server 2019 | Supported     |
| Windows Server 2022 | Supported     |
| Windows Server 2025 | Supported     |

## ConfigMgr Supported Versions

ConfigMgr uses a Current Branch servicing model with 2 releases per year, typically in March and September. Each version is supported by Microsoft for 18 months from its release date. After 18 months, the version reaches end of support and no longer receives updates or technical support from Microsoft.

{% hint style="info" %}
**Note**

Starting with version 2609, ConfigMgr will transition to a single, annual, release cadence.
{% endhint %}

The Publisher supports ConfigMgr versions that are still within Microsoft’s supported lifecycle.

The table below reflects the current Microsoft support lifecycle for ConfigMgr Current Branch versions.

| Version | Support Start    | Support End        | Support Status |
| ------- | ---------------- | ------------------ | -------------- |
| 2403    | April 22, 2024   | October 22, 2025   | Unsupported    |
| 2409    | December 4, 2024 | June 6, 2026       | Supported      |
| 2503    | March 31, 2025   | September 30, 2026 | Supported      |
| 2509    | December 2025    | May 12, 2027       | Supported      |

{% hint style="warning" %}
**Note**

Running unsupported or end of life versions of ConfigMgr is not supported.
{% endhint %}

For more information on the ConfigMgr product lifecycle, see [https://learn.microsoft.com/en-us/lifecycle/products/microsoft-configuration-manager](https://learn.microsoft.com/en-us/lifecycle/products/microsoft-configuration-manager).

## ConfigMgr Remote Console

The ConfigMgr Remote Console exposes some SDK helper files that the Publisher utilises to connect to the SMS Provider. More information on how to install the console can be found at [https://learn.microsoft.com/en-us/intune/configmgr/core/servers/deploy/install/install-consoles](https://learn.microsoft.com/en-us/intune/configmgr/core/servers/deploy/install/install-consoles)

{% hint style="info" %}
**Note**

The installation file for the remote console can typically be found on the Site Server share. For example:-

\\\site-server.contoso.com\SMS\_xxx\tools\ConsoleSetup\ConsoleSetup.exe
{% endhint %}

{% hint style="warning" %}
**Important**

A reboot is normally needed after installing the ConfigMgr remote console otherwise you might see the following error logged in PatchMyPC.log:-\
\
_"An error occurred while connecting to Sms provider as System: Unable to find the Assembly: AdminUI.WqlQueryEngine, Version=5.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35 \[PatchMyPC\_Sccm.AssemblyResolver+AssemblyNotFoundException] HResult: -2146233088"_
{% endhint %}

If the ConfigMgr Remote Console is _not_ installed, the following message is also indicated in the Publisher when attempting to [Configure the SMS Provider](../../publisher-reference/configure-the-sms-provider-connection.md).

<figure><img src="../../../.gitbook/assets/image (75).png" alt="Configure the SMS Provider - Missing SDK" width="563"><figcaption></figcaption></figure>

## WSUS Role

For the Publisher to be able to code-sign PowerShell detection scripts for ConfigMgr applications, the WSUS role must be installed on the Publisher system.

While [limited WSUS API access](../intune-requirements/software.md#install-the-wsus-updateservices-api) may be sufficient for some operations, such as deserializing the Patch My PC Catalog, the Publisher can _only_ use code-signing certificates, to sign ConfigMgr detection scripts, from the "WSUS" local certificate store. Certificates located in other Windows certificate stores are not supported for signing ConfigMgr application detection scripts.

Additionally, the WSUS role is also required to publish updates, selected on the [Updates](../../administration/updates/) tab, that will be synchronized from WSUS into ConfigMgr during a SUP sync. For more information about the WSUS role requirement, see: [WSUS Requirements](../wsus-requirements/).


---
description: Prerequisites for installing the Publisher with Configuration Manager.
---

# Requirements

_Applies to: On-premises Publisher_

{% hint style="success" %}
Before you get started, make sure you take advantage of our [free trial](https://patchmypc.com/free-trial)!
{% endhint %}

When installing the Publisher for Configuration Manager, please ensure you meet the following requirements:

### Software:

* [Microsoft .NET Framework](https://learn.microsoft.com/en-us/dotnet/framework/migration-guide/versions-and-dependencies) 4.6.2 or above
* Internet connection
* The relevant [domain names for Patch My PC have been added to your firewall's allowlist](https://patchmypc.com/list-of-domains-used-for-downloads-in-patch-my-pc-update-catalog)
* Install the Publisher on top-most WSUS/Software Update Point in the environment
* Appropriate disk space depending on the number of products enabled
* Install the Configuration Manager console
* Supported Operating Systems
  * Windows Server 2012, Windows Server 2016, Windows Server 2019, Windows Server 2022, Windows Server 2019 and Windows Server 2025
  * Windows Server Update Services (WSUS) installed and configured

{% hint style="info" %}
More information on supported Configuration Manager and WSUS versions can be found at [https://patchmypc.com/supported-versions-of-configuration-manager-and-wsus-for-patch-my-pc](https://patchmypc.com/supported-versions-of-configuration-manager-and-wsus-for-patch-my-pc)
{% endhint %}

{% hint style="info" %}
The Patch My PC Publisher will require the user launching the Publisher tool to be a local administrator on the server. This requirement is for both the installation as well as running the Publisher after it has been installed and configured.
{% endhint %}

### Hardware:

The Publisher is a lightweight Windows application with a GUI frontend and a Windows service backend. The hardware requirements can be found below.

* CPU: 2 CPU or more
* Memory: 8GB of RAM or more
* Disk Space: 80GB of disk space or more
  * The amount of disk space required will depend on the number of selected products.

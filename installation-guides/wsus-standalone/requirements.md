---
description: Requirements for installing WSUS Standalone mode.
---

# Requirements

_Applies to: On-premises Publisher_

{% hint style="success" %}
Before you get started, make sure you take advantage of our [free trial](https://patchmypc.com/free-trial)!
{% endhint %}

Standalone WSUS mode is **only required when you are not using Configuration Manager** for software updates and are **only using WSUS**. When enabled, published third-party updates will appear directly in the WSUS console.&#x20;

{% hint style="info" %}
**Note:**

To publish updates with the customization options available in the Publisher, you will need the [Enterprise Patch subscription level](https://patchmypc.com/frequently-asked-questions#subscription-comparisons).  &#x20;
{% endhint %}

When installing the Publisher for **WSUS Standalone**, please ensure you meet the following requirements:

### Software:

* [Microsoft .NET Framework](https://learn.microsoft.com/en-us/dotnet/framework/migration-guide/versions-and-dependencies) 4.6.2 or above
* Internet connection
* The relevant [domain names for Patch My PC have been added to your firewall's allowlist](https://patchmypc.com/list-of-domains-used-for-downloads-in-patch-my-pc-update-catalog)
* Install the Publisher on the top-level WSUS server in the hierarchy
* Appropriate disk space depending on the number of products enabled
* Supported Operating Systems
  * Windows Server 2012, Windows Server 2016, Windows Server 2019, Windows Server 2022, Windows Server 2025
  * Windows Server Update Services (WSUS) installed and configured

{% hint style="info" %}
The Patch My PC Publisher will require the user launching the Publisher tool to be a local administrator on the server.
{% endhint %}

### Hardware:

The Publisher is a lightweight Windows application with a GUI frontend and a Windows service backend. The hardware requirements can be found below.

* CPU: 2 CPU or more
* Memory: 8GB of RAM or more
* Disk Space: 80GB of disk space or more
  * The amount of disk space required will depend on the number of selected products.

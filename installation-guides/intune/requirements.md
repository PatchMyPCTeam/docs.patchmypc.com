---
description: Prerequisites for installing the Publisher with Intune.
---

# Requirements

_Applies to: On-premises Publisher_

<blockquote class="wp-block-quote">
<p>Before you get started, make sure you take advantage of our <a href="https://patchmypc.com/free-trial">free trial</a>!</p>
</blockquote>

When installing the Publisher for an Intune-only configuration, ensure you meet the following requirements:

### Software:

* [Microsoft .NET Framework](https://learn.microsoft.com/en-us/dotnet/framework/migration-guide/versions-and-dependencies) 4.6.2 or above
* An Internet connection
* The relevant [domain names for Patch My PC have been added to your firewall's allowlist](https://patchmypc.com/list-of-domains-used-for-downloads-in-patch-my-pc-update-catalog)
* Appropriate disk space depending on the number of products enabled
* Supported Operating Systems
  * Windows 10 or Windows 11
    * When using Windows 10/11, the [RSAT: Windows Server Updates Services](https://docs.microsoft.com/en-us/windows-server/remote/remote-server-administration-tools#BKMK_Thresh) needs to be installed.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See the <a href="https://patchmypc.com/windows-server-update-services-not-installed#howtofixit">How to fix</a> section of the <a href="https://patchmypc.com/windows-server-update-services-not-installed">Windows Server Update Services is not installed</a> Knowledge Base article for details on how to install RSAT.</p>
</blockquote>

* Windows Server 2012, Windows Server 2016, Windows Server 2019, Windows Server 2022, Windows Server 2025
  * When using Windows Server, only the WSUS API component needs to be installed, not full WSUS.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The Publisher displays the following dialog if the WSUS prerequisites are not installed:\</p>
<p>&#x20;         **Windows Server Update Services is not installed.**</p>
<p>See the <a href="https://patchmypc.com/windows-server-update-services-not-installed">Windows Server Update Services is not installed</a> Knowledge Base article for details on how to resolve this.</p>
</blockquote>

### Hardware:

The Publisher is a lightweight Windows application with a GUI frontend and a Windows service backend. The hardware requirements can be found below.

* CPU: 2 CPU or more
* Memory: 8GB of RAM or more
* Disk Space: 80GB of disk space or more
  * The amount of disk space required will depend on the number of selected products.
# Core Requirements for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This section details the core requirements for Patch My PC (PMPC) Publisher, which apply regardless of the management platform being used.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><a href="core-requirements.md#permissions">Permissions</a></td><td valign="top"><a href="core-requirements.md#software">Software</a></td><td valign="top"><a href="core-requirements.md#hardware">Hardware</a></td><td valign="top"><a href="core-requirements.md#network">Network</a></td></tr></tbody></table>

{% hint style="success" %}
**Tip**

Before you get started, make sure you take advantage of our [free trial](https://patchmypc.com/free-trial)
{% endhint %}

## Permissions

Publisher requires the following permissions:

* [Local Administrator](core-requirements.md#local-administrator)
* [Service Account](core-requirements.md#service-account)

### Local Administrator

The user installing and/or accessing the Publisher application to configure third-party applications and updates must be an administrator on the computer where the Publisher is installed.

{% hint style="info" %}
**Note**

Publisher currently does not support a remote console. The Publisher application must be accessed directly on the device where it’s installed. However, you can use Remote Desktop to access the application. Only one instance of the Publisher application can be open at a time.
{% endhint %}

### Service Account

By default, the Publisher service runs as local **SYSTEM**.

In most environments, this is the recommended configuration, and no service account is required. A group Managed Service Account can be used when the Publisher service must authenticate to network resources that do not support the computer account identity. A common example is an authenticated proxy used for Publisher downloads.

When using a gMSA, review [gMSA support for the Publisher](../technical-references/gsma-support.md) before configuration.

## Software

Publisher has the following software requirements:

* [Microsoft .NET Framework](https://learn.microsoft.com/en-us/dotnet/framework/migration-guide/versions-and-dependencies) 4.6.2 or above
* Supported Operating Systems
  * Windows Server 2016, 2019, 2022, or 2025
  * Windows 11

{% hint style="danger" %}
**Important**

Publisher can be installed on Windows 11 only if it is being used solely to publish applications and updates to Intune.
{% endhint %}

## Hardware <a href="#hardware" id="hardware"></a>

Publisher has the following hardware requirements:

* CPU: 2 CPUs or more
* Memory: 8GB or more of RAM

### Disk Space

Publisher requires 120 GB of free disk space.

{% hint style="info" %}
**Note**

120 GB is an estimated requirement based on enabling approximately 700 products in Publisher. The average application size across all apps in our catalog is around 180 MB, with individual apps ranging from 1 MB to 2 GB.

The disk space recommendation covers the space Publisher needs to download and package vendor installers. Actual storage requirements may be higher depending on the number of products and the platforms you publish to.

For example, ConfigMgr requires space for the application content source folder, retained app versions, and the content library. WSUS duplicates content in both the UpdateServicesPackages and WSUS Content folders.&#x20;

See the platform-specific sections for more detailed guidance.
{% endhint %}

The table below illustrates the estimated disk space requirements based on the number of applications you plan to enable in Publisher. These estimates are based on the average application size across our catalog.&#x20;

{% hint style="danger" %}
**Important**

As actual sizes can vary significantly, with individual apps ranging from 1 MB to 1.9 GB, these values should be used for illustrative purposes only.

Additional disk space considerations are needed when publishing applications/updates to [ConfigMgr](configmgr-requirements/disk-space.md) and [WSUS](wsus-requirements/disk-space.md).
{% endhint %}

<table><thead><tr><th valign="top">Enabled Apps</th><th valign="top">Space Required</th></tr></thead><tbody><tr><td valign="top">250</td><td valign="top">40.0 GB</td></tr><tr><td valign="top">500</td><td valign="top">80.0 GB</td></tr><tr><td valign="top">750</td><td valign="top">120.0 GB</td></tr><tr><td valign="top">1000</td><td valign="top">160.0 GB</td></tr></tbody></table>

## Network

### Core Firewall Exceptions

Publisher requires access to the following URLs for core functionality.

{% hint style="info" %}
**Note**

There are additional network requirements when using Publisher with [ConfigMgr](configmgr-requirements/network.md) and [Intune](intune-requirements/network.md).
{% endhint %}

<table><thead><tr><th width="225" valign="top">Domain</th><th width="243" valign="top">Reason</th><th width="82" valign="top">Port</th><th width="104" valign="top">Protocol</th></tr></thead><tbody><tr><td valign="top">patchmypc.com</td><td valign="top">Catalog download</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">content.patchmypc.com</td><td valign="top">Icons, scripts and other resources</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">api.patchmypc.com</td><td valign="top">Licensing validation</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">portal.patchmypc.com</td><td valign="top">Patch My PC Cloud services</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">us.portal.patchmypc.com</td><td valign="top">Patch My PC Cloud services</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">eu.portal.patchmypc.com</td><td valign="top">Patch My PC Cloud services</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">signalr-us.patchmypc.com</td><td valign="top">Patch My PC Cloud services</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">signalr-eu.patchmypc.com</td><td valign="top">Patch My PC Cloud services</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">login.microsoftonline.com</td><td valign="top">Patch My PC Cloud services</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">*.digicert.com</td><td valign="top">CRL checking</td><td valign="top">80</td><td valign="top">http</td></tr><tr><td valign="top">timestamp.digicert.com</td><td valign="top">timestamping</td><td valign="top">80</td><td valign="top">http</td></tr><tr><td valign="top">ocsp.digicert.com</td><td valign="top">timestamping</td><td valign="top">80</td><td valign="top">http</td></tr></tbody></table>

{% hint style="info" %}
**Note**

The Publisher requires access to `timestamp.digicert.com` and `ocsp.digicert.com` to support timestamping operations. Additional DigiCert hostnames may appear in network monitoring, such as `ocsp.digicert.cn`, because the specific OCSP or CRL endpoint Windows contacts for a given domain are not predetermined.&#x20;

When Windows CryptoAPI processes certificate validation, it follows the certificate chain and resolves whichever revocation endpoint is referenced by that chain at runtime, which can vary by region and certificate. These endpoints are not chosen or contacted directly by Publisher, which is why the `*.digicert.com` wildcard is required.
{% endhint %}

### Local Configuration API

Publisher communicates with a local API running on the same server. It typically uses port 9001. If 9001 is unavailable, Publisher tries the next available port in sequence, such as 9002 or 9003, etc.

Ensure local firewall rules allow both inbound and outbound local traffic on the active port. If connections to localhost on that port are blocked, Publisher will be unable to communicate with the local API.

To determine which port is currently assigned, review this registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Patch My PC Publishing Service\ConfigApiPort`

### Vendor Firewall Exceptions

The [List of Domains for Update Content (Based on Products Enabled for Published)](https://patchmypc.com/kb/list-domains-firewall-allowlist-when/#h-list-of-domains-for-update-content-based-on-products-enabled-for-published) list contains domains that must be accessible to download update content for the products you have enabled in Publisher. It ensures your environment can reach the necessary vendor or content delivery URLs to retrieve installer files during the publishing process.

{% hint style="info" %}
**Note**

Given the large number of applications supported in the Patch My PC catalog, we recommend allowing outbound HTTP (port 80) and HTTPS (port 443) traffic. Creating and maintaining explicit allow lists for each vendor domain can be labor-intensive, and vendor-hosted installer URLs are subject to change without notice. Blocking these URLs could disrupt the publishing process and prevent updates from being downloaded successfully.
{% endhint %}

{% hint style="danger" %}
**Important**

If your network filters based on user-agent, make sure to allow **Patch My PC Publishing Service\*** to ensure downloads are not blocked.
{% endhint %}

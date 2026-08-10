# Core Requirements

_Applies to: Patch My PC Publisher V2.x_

{% hint style="success" %}
**Tip**

Before you get started, make sure you take advantage of our [free trial](https://patchmypc.com/free-trial)
{% endhint %}

This section details requirements for the Publisher that apply regardless of the platform being used.

## Permissions

Publisher requires the following permissions:

### Local Administrator

The user installing and/or accessing the Publisher application, to configure third-party applications and updates, must be an administrator on the computer where the Publisher is installed.

{% hint style="info" %}
**Note**

The Publisher currently does not support a remote console. The Publisher application must be accessed directly on the device where it’s installed. However, you can use Remote Desktop to access the application. Only one instance of the Publisher application can be open at a time.
{% endhint %}

### Service Account

By default, the Publisher service runs as local SYSTEM.

In most environments, this is the recommended configuration, and no service account is required. A group Managed Service Account can be used when the Publisher service must authenticate to network resources that do not support the computer account identity. A common example is an authenticated proxy used for Publisher downloads.

When using a gMSA, review [gMSA support for the Publisher](../publisher-reference/gmsa-support-for-the-publisher.md) before configuration.

## Software

* [Microsoft .NET Framework](https://learn.microsoft.com/en-us/dotnet/framework/migration-guide/versions-and-dependencies) 4.6.2 or above
* Supported Operating Systems
  * Windows Server 2016
  * Windows Server 2019
  * Windows Server 2022
  * Windows Server 2019
  * Windows Server 2025
  * Windows 11

{% hint style="warning" %}
**Important**

The Publisher can be installed on Windows 11 only if it is soley being used to publish applications and updates to Intune.
{% endhint %}

## Hardware <a href="#hardware" id="hardware"></a>

* CPU: 2 CPU or more
* Memory: 8GB of RAM or more

## Disk Space

* Disk Space: 120 GB&#x20;

The table below illustrates the estimated disk space requirements based on the number of applications you plan to enable in the Publisher. These estimates are based on the average application size across our catalog. Please note that actual sizes can vary significantly, with individual apps ranging from 1.01 MB to 1.81 GB. Therefore these numbers should be used for illustrative purposes only.

Additional disk space considerations are needed when publishing applications/updates to [ConfigMgr ](configmgr-requirements/disk-space.md)and [WSUS](wsus-requirements/disk-space.md).

{% hint style="info" %}
**Note**

120 GB is an estimated requirement based on enabling approximately 700 products in the Publisher. The average application size, calculated from all apps in our catalog, is around 180 MB, with individual apps ranging from 1 MB to 2 GB.

The disk space recommendation covers the space the Publisher needs to download and package vendor installers. Actual storage requirements may be higher depending on the number of products and the platforms you publish to.&#x20;

For example, ConfigMgr requires space for the application content source folder, retained app versions, and the content library. WSUS duplicates content in both the UpdateServicesPackages and WSUS Content folders.&#x20;

See the platform-specific sections for more detailed guidance.
{% endhint %}

| Enabled Apps | Space Required |
| ------------ | -------------- |
| 250          | 40.0 GB        |
| 500          | 80.0 GB        |
| 750          | 120.0 GB       |
| 1000         | 160.0 GB       |

## Network

### Core Firewall Exceptions

The Publisher requires access to the following URLs for core functionality. There are additional network requirements when using the Publisher with [ConfigMgr](configmgr-requirements/network.md) and [Intune](intune-requirements/network.md).

<table><thead><tr><th width="249">Domain</th><th width="243">Reason</th><th>Port</th><th>Protocol</th></tr></thead><tbody><tr><td>patchmypc.com</td><td>Catalog download</td><td>443</td><td>https</td></tr><tr><td>content.patchmypc.com</td><td>Icons, scripts and other resources</td><td>443</td><td>https</td></tr><tr><td>api.patchmypc.com</td><td>Licensing validation</td><td>443</td><td>https</td></tr><tr><td>portal.patchmypc.com</td><td>Patch My PC Cloud services</td><td>443</td><td>https</td></tr><tr><td>us.portal.patchmypc.com</td><td>Patch My PC Cloud services</td><td>443</td><td>https</td></tr><tr><td>eu.portal.patchmypc.com</td><td>Patch My PC Cloud services</td><td>443</td><td>https</td></tr><tr><td>signalr-us.patchmypc.com</td><td>Patch My PC Cloud services</td><td>443</td><td>https</td></tr><tr><td>signalr-eu.patchmypc.com</td><td>Patch My PC Cloud services</td><td>443</td><td>https</td></tr><tr><td>login.microsoftonline.com</td><td>Patch My PC Cloud services</td><td>443</td><td>https</td></tr><tr><td>*.digicert.com</td><td>CRL checking</td><td>80</td><td>http</td></tr><tr><td>timestamp.digicert.com</td><td>timestamping</td><td>80</td><td>http</td></tr><tr><td>ocsp.digicert.com</td><td>timestamping</td><td>80</td><td>http</td></tr></tbody></table>

{% hint style="info" %}
**Note**

The Publisher requires access to `timestamp.digicert.com` and `ocsp.digicert.com` to support timestamping operations. Additional DigiCert hostnames may appear in network monitoring, such as `ocsp.digicert.cn` , because the specific OCSP or CRL endpoint Windows contacts is not predetermined.&#x20;

When Windows CryptoAPI processes certificate validation, it follows the certificate chain and resolves whichever revocation endpoint is referenced by that chain at runtime, which can vary by region and certificate. These endpoints are not chosen or contacted directly by the Publisher, which is why the wildcard `*.digicert.com` is required.
{% endhint %}

### Local Configuration API

The Publisher communicates with a local API running on the same server. It typically uses port 9001. If 9001 is unavailable, the Publisher will try the next available port in sequence, such as 9002 or 9003 and so on.

Ensure local firewall rules allow both inbound and outbound local traffic on the active port. If connections to localhost on that port are blocked, the Publisher will not be able to communicate with the local API.

To determine which port is currently assigned, review this registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Patch My PC Publishing Service\ConfigApiPort`

### Vendor Firewall Exceptions

The following list contains domains that must be accessible to download update content for the products you have enabled in the Publisher. It ensures that your environment can reach the necessary vendor or content delivery URLs to retrieve installer files during the publishing process.

{% embed url="https://patchmypc.com/kb/list-domains-firewall-allowlist-when/#h-list-of-domains-for-update-content-based-on-products-enabled-for-published" %}
List of domains for vendor installer content
{% endembed %}

{% hint style="info" %}
**Note**

Given the large number of applications supported in the Patch My PC catalog, we recommend allowing outbound HTTP (port 80) and HTTPS (port 443) traffic. Creating and maintaining explicit allow lists for each vendor domain can be labor-intensive, and vendor-hosted installer URLs are subject to change without notice. Blocking these URLs could disrupt the publishing process and prevent updates from being downloaded successfully.
{% endhint %}

{% hint style="warning" %}
**Important**

If your network filters based on user-agent, make sure to allow `Patch My PC Publishing Service*` to ensure downloads are not blocked.
{% endhint %}

## Platform Specific Requirements

For additional platform requirements specific to Configmgr, WSUS or Intune, use the links below.

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><p><a href="configmgr-requirements/">ConfigMgr Requirements</a></p><p>Specific requirements for publishing apps and updates to ConfigMgr</p></td><td></td></tr><tr><td><p><a href="wsus-requirements/">WSUS Requirements</a></p><p>Specific requirements for publishing updates to WSUS</p></td><td></td></tr><tr><td><p><a href="intune-requirements/">Intune Requirements</a></p><p>Specific requirements for publishing apps and updates to Intune</p></td><td></td></tr></tbody></table>

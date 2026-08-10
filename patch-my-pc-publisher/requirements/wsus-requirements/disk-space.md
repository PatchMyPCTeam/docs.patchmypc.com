# WSUS Disk Space Requirements for  Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Third-party update publishing using Patch My PC (PMPC) Publisher leverages the Microsoft Windows Server Update Services (WSUS) API, which stages, processes, and signs update content directly within the WSUS content folder.

Understanding where this content is created and stored is important for accurate disk sizing and capacity planning.

The third-party publishing workflow uses several locations during the publish process:

1. **UpdateServicesPackages**\
   All third-party update binaries are first downloaded and staged in the **UpdateServicesPackages** folder. This is where the WSUS API processes the update content prior to publication.
2. **CAB file creation**\
   Once the update content is staged, WSUS creates a CAB file in the same folder to encapsulate the update metadata and binaries.
3. **Temporary signing location**\
   The CAB file is then temporarily copied to a working folder under `%ProgramFiles%`, where it is digitally signed using the configured code-signing certificate.
4. **Final WSUSContent placement**\
   After signing, the CAB file is moved into the **WSUSContent** folder, where it is served to clients during update downloads.

The **120GB** overall disk space requirement detailed in [Core Requirements](../core-requirements.md) accounts for the space needed by Publisher to download and package vendor installers before they are published, and for the Windows operating system.

The amount of space consumed by WSUS depends on:

* Number of updates published
* Average update size
* How frequently updates are refreshed or superseded.&#x20;

{% hint style="info" %}
**Note**

As third-party updates vary widely in size, disk space requirements should be treated as estimates rather than fixed values.
{% endhint %}

The table below provides illustrative estimates based on average third-party update sizes and common publishing patterns. These figures are intended to help with planning and should be adjusted based on your environment and product selection.

<table><thead><tr><th align="right" valign="top">Enabled Updates</th><th align="right" valign="top">Retained Versions</th><th align="right" valign="top">UpdateServicesPackages</th><th width="141" align="right" valign="top">WSUSContent</th></tr></thead><tbody><tr><td align="right" valign="top">250</td><td align="right" valign="top">0</td><td align="right" valign="top">80.0 GB</td><td align="right" valign="top">40.0 GB</td></tr><tr><td align="right" valign="top">250</td><td align="right" valign="top">1</td><td align="right" valign="top">160.0 GB</td><td align="right" valign="top">80.0 GB</td></tr><tr><td align="right" valign="top">250</td><td align="right" valign="top">2</td><td align="right" valign="top">240.0 GB</td><td align="right" valign="top">120.0 GB</td></tr><tr><td align="right" valign="top">250</td><td align="right" valign="top">3</td><td align="right" valign="top">320.0 GB</td><td align="right" valign="top">160.0 GB</td></tr><tr><td align="right" valign="top">500</td><td align="right" valign="top">0</td><td align="right" valign="top">180.0 GB</td><td align="right" valign="top">90.0 GB</td></tr><tr><td align="right" valign="top">500</td><td align="right" valign="top">1</td><td align="right" valign="top">360.0 GB</td><td align="right" valign="top">180.0 GB</td></tr><tr><td align="right" valign="top">500</td><td align="right" valign="top">2</td><td align="right" valign="top">540.0 GB</td><td align="right" valign="top">270.0 GB</td></tr><tr><td align="right" valign="top">500</td><td align="right" valign="top">3</td><td align="right" valign="top">720.0 GB</td><td align="right" valign="top">360.0 GB</td></tr><tr><td align="right" valign="top">750</td><td align="right" valign="top">0</td><td align="right" valign="top">260.0 GB</td><td align="right" valign="top">130.0 GB</td></tr><tr><td align="right" valign="top">750</td><td align="right" valign="top">1</td><td align="right" valign="top">520.0 GB</td><td align="right" valign="top">260.0 GB</td></tr><tr><td align="right" valign="top">750</td><td align="right" valign="top">2</td><td align="right" valign="top">780.0 GB</td><td align="right" valign="top">390.0 GB</td></tr><tr><td align="right" valign="top">750</td><td align="right" valign="top">3</td><td align="right" valign="top">1040.0 GB</td><td align="right" valign="top">520.0 GB</td></tr><tr><td align="right" valign="top">1000</td><td align="right" valign="top">0</td><td align="right" valign="top">360.0 GB</td><td align="right" valign="top">180.0 GB</td></tr><tr><td align="right" valign="top">1000</td><td align="right" valign="top">1</td><td align="right" valign="top">720.0 GB</td><td align="right" valign="top">360.0 GB</td></tr><tr><td align="right" valign="top">1000</td><td align="right" valign="top">2</td><td align="right" valign="top">1080.0 GB</td><td align="right" valign="top">540.0 GB</td></tr><tr><td align="right" valign="top">1000</td><td align="right" valign="top">3</td><td align="right" valign="top">1440.0 GB</td><td align="right" valign="top">720.0 GB</td></tr></tbody></table>

{% hint style="success" %}
**Tip**

**UpdateServicesPackages** contains the published third-party update binaries _plus_ an unsigned copy of the cab files that ends up in the WSUS Content directory.
{% endhint %}

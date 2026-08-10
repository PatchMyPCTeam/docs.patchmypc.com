# Disk Space

_Applies to: Patch My PC Publisher V2.x_

Third-party update publishing leverages the WSUS API, which stages, processes, and signs update content directly within the WSUS content directory.

Understanding where this content is created and stored is important for accurate disk sizing and capacity planning.

The third-party publishing workflow uses several locations during the publish process:

1. **UpdateServicesPackages**\
   All third-party update binaries are first downloaded and staged in the UpdateServicesPackages directory. This is where the WSUS API processes the update content prior to publication.
2. **CAB file creation**\
   Once the update content is staged, WSUS creates a CAB file in the same directory to encapsulate the update metadata and binaries.
3. **Temporary signing location**\
   The CAB file is then temporarily copied to a working directory under `%ProgramFiles%`, where it is digitally signed using the configured code-signing certificate.
4. **Final WSUSContent placement**\
   After signing, the CAB file is moved into the WSUSContent directory, where it is served to clients during update downloads.

The **120GB** overall disk space requirement listed on our [core Publisher requirements](../core-requirements.md#disk-space) page accounts for the space needed by the Publisher to download and package vendor installers before they are published and for the Windows Operating system.

The amount of space consumed by WSUS depends on the number of updates published, the average update size, and how frequently updates are refreshed or superseded. Because third-party updates vary widely in size, disk space requirements should be treated as estimates, not fixed values.

The table below provides illustrative estimates based on average third-party update sizes and common publishing patterns. These figures are intended to help with planning and should be adjusted based on your environment and product selection.

| Enabled Updates | Retained Versions | UpdateServicesPackages | WSUSContent |
| --------------: | ----------------: | ---------------------: | ----------: |
|             250 |                 0 |                80.0 GB |     40.0 GB |
|             250 |                 1 |               160.0 GB |     80.0 GB |
|             250 |                 2 |               240.0 GB |    120.0 GB |
|             250 |                 3 |               320.0 GB |    160.0 GB |
|             500 |                 0 |               180.0 GB |     90.0 GB |
|             500 |                 1 |               360.0 GB |    180.0 GB |
|             500 |                 2 |               540.0 GB |    270.0 GB |
|             500 |                 3 |               720.0 GB |    360.0 GB |
|             750 |                 0 |               260.0 GB |    130.0 GB |
|             750 |                 1 |               520.0 GB |    260.0 GB |
|             750 |                 2 |               780.0 GB |    390.0 GB |
|             750 |                 3 |              1040.0 GB |    520.0 GB |
|            1000 |                 0 |               360.0 GB |    180.0 GB |
|            1000 |                 1 |               720.0 GB |    360.0 GB |
|            1000 |                 2 |              1080.0 GB |    540.0 GB |
|            1000 |                 3 |              1440.0 GB |    720.0 GB |

{% hint style="success" %}
**Tip**

**UpdateServicesPackages** contains the published third-party updates binaries _plus_ an un-signed copy oif the cab files that ends up in the WSUS Content directory.
{% endhint %}

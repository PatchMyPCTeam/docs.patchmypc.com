# Download and Install

_Applies to: Patch My PC Publisher V2.x_

> Please review the \[core Publisher requirements]\(publisher-requirements/core-requirements.md), which apply regardless of the platform being used, before beginning installation.

## Where should I install the Publisher?

When using the Publisher to publish both applications and updates to ConfigMgr, it should be installed on the top-level Software Update Point (SUP). In a ConfigMgr hierarchy, this would typically be the CAS which holds the Software Update Point role. This allows Publisher to publish updates directly into WSUS using the local WSUS API, ensuring that update metadata is created locally and then inherited naturally by any downstream WSUS servers.

In some environments, the Software Update Point role is hosted on a remote site system rather than the site server itself. In these cases, the Publisher should be installed on that remote server, provided it is the top-level SUP. The key requirement is not the site server, but the server hosting the top-level WSUS instance, as the Publisher must be co-located with WSUS to successfully publish update metadata.

For environments using WSUS only (without ConfigMgr), the same principle applies. The Publisher must be installed on the top-level WSUS server, as this is where update metadata is authored. When WSUS synchronizes, that metadata is then replicated to any downstream WSUS servers, ensuring consistency across the hierarchy.

If you are using the Publisher for Intune publishing only, it does not need to be installed on a WSUS or ConfigMgr server and can be installed on any suitable Windows system (see [Publisher Requirements](publisher-requirements/core-requirements.md#software) for supported operating systems). Because Publisher is capable of creating and managing applications and updates in Intune, it should be treated as a high-trust system and secured accordingly, with restricted access and appropriate credential protection.

Use the table below to understand where the Publisher should be installed in your environment.

| Scenario                                 | Where to install Publisher                       | Note                                                                                                                      |
| ---------------------------------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| **ConfigMgr (with WSUS)**                | **Top-level SUP**                                | The Publisher uses the local WSUS API to publish update metadata. Downstream WSUS servers inherit metadata automatically. |
| **ConfigMgr (with WSUS and remote SUP)** | **Remote site system hosting the top-level SUP** | The Publisher must be installed on the server hosting the top-level WSUS instance, not necessarily the site server.       |
| **WSUS only (no ConfigMgr)**             | **Top-level WSUS server**                        | Update metadata must be created on the upstream WSUS server so it can replicate to downstream WSUS servers.               |
| **Intune only**                          | **Any suitable Windows system**                  | The Publisher communicates directly with Intune via Microsoft Graph.                                                      |
| **Mixed environments**                   | **Top level WSUS Server /** **SUP**              | Install the Publisher on the top-level WSUS/SUP server if publishing updates to both ConfigMgr/WSUS and Intune.           |

> \*\*Tip\*\*
>
> Some customers who use Intune only choose to install the Publisher on a dedicated Azure virtual machine. A B2 size virtual machine or equivalent is commonly used.
>
> The virtual machine should still meet or exceed the \[minimum core requirements]\(publisher-requirements/core-requirements.md) and \[additional requirements needed for Intune publishing]\(publisher-requirements/intune-requirements/).

> \*\*Note\*\*
>
> If you intend to publish third-party applications and updates to Intune only, we generally recommend using Patch My PC Cloud, our cloud-based service, as it removes the need to manage on-premises infrastructure and simplifies ongoing operations.
>
> However, some customers are required to use the Publisher instead, such as those with restrictions around enterprise application usage, environments that require GCC High, or scenarios where cloud-hosted services are not permitted. In these cases, the Publisher provides a fully supported alternative that allows publishing to Intune while keeping control within your environment.

## Download the Publisher

To download the Publisher installer, follow the steps below:

1. Open a web browser.
2. Navigate to the following URL:\
   [**https://patchmypc.com/msi**](https://patchmypc.com/msi)

> \*\*Note\*\*
>
> SHA256: EAF6A570087C2B67D9A945EADB9BB7DD503B86BD1E145D41E80BE2770BC69414

1.  The download will begin automatically.<br>

    ![Download the Publisher from https://patchmypc.com/msi](<../.gitbook/assets/image-(404) (1).png>)
2. Once complete, confirm that the file **`PatchMyPC-Publishing-Service.msi`** has been downloaded.
3. Copy the installer to the target server, if required, then proceed to [Install the Publisher](download-and-install.md#install-publisher).

## Install the Publisher

After carefully observing and understanding the [requirements](publisher-requirements/), install Publisher by following the steps below:

1. Once you have [downloaded the Publisher](download-and-install.md#download-publisher), double click the msi to launch the installer.
2.  Click **Next** to begin the installation wizard. Agree to the terms of service and click **Next** again.<br>

    ![Install Publisher and accept the end-user license agreement](<../.gitbook/assets/image-(405) (1).png>)
3.  If you are only using the Publisher to publish applications and updates in Intune, you can check the **Enable Microsoft Intune standalone mode\*** box. Click **Next**.<br>

    ![Optionally select Intune standalone mode](<../.gitbook/assets/image-(406) (1).png>)

    \*Intune standalone mode simply removes some tabs in the Publisher that are specifically used for publishing applications and updates to ConfigMgr and WSUS. These tabs can be re-enabled retrospectively after installation from the Advanced tab in Publisher.
4.  Select a folder to install the Publisher, and click **Next**. The default folder is `C:\Program Files\Patch My PC\Patch My PC Publishing Service\`.<br>

    ![Select the folder for the Publisher installation files](<../.gitbook/assets/image-(407) (1).png>)
5.  When you are ready to being, click **Install**.<br>

    ![Begin Publisher installation](<../.gitbook/assets/image-(408) (1).png>)
6.  Click **Yes** if you receive a UAC prompt. When installation has completed, you can choose to not immediately launch the Publisher by un-checking **Launch Patch My PC Publishing Service**. Click **Finish**.<br>

    ![Authorize and Complete Installation](<../.gitbook/assets/image-(409) (1).png>)

### What Next?

Once the Publisher is installed, configure it based on how you plan to use it. Choose the scenario that best matches your environment:

* [Scenario 1: ConfigMgr - Applications only](scenario-based-guidance/installation-and-configuration/scenario-1-configmgr-applications-only.md)
* [Scenario 2: ConfigMgr - Applications and Updates (WSUS)](scenario-based-guidance/installation-and-configuration/scenario-2-configmgr-applications-and-updates-wsus.md)
* [Scenario 3: WSUS (Standalone)](scenario-based-guidance/installation-and-configuration/scenario-3-wsus-standalone.md)
* [Scenario 4: Intune – Applications and Updates](scenario-based-guidance/installation-and-configuration/scenario-4-intune-applications-and-updates.md)
* [Scenario 5: Mixed environment (ConfigMgr, WSUS and Intune)](scenario-based-guidance/installation-and-configuration/scenario-5-mixed-environment-configmgr-wsus-and-intune.md)

# Where to Install Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Where you install Patch My PC (PMPC) Publisher depends on your environment:

* [ConfigMgr (with WSUS)](where.md#configmgr-with-wsus)
  * [ConfigMgr (with WSUS and remote SUP)](where.md#configmgr-with-wsus-and-remote-sup)
* [WSUS only (no ConfigMgr)](where.md#wsus-only-no-configmgr)
* [Intune only](where.md#intune-only)
* [Mixed environments](where.md#mixed-environments)

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Please review the [Core Requirements for Publisher](../requirements/core-requirements.md) before continuing, as these apply regardless of the platform being used, before beginning installation.</p>
</blockquote>

## ConfigMgr (with WSUS)

When using Publisher to publish both applications and updates to Microsoft ConfigMgr, Publisher should be installed on the top-level Software Update Point (SUP).&#x20;

In a ConfigMgr hierarchy, this would typically be the CAS, which holds the SUP Site System role. This allows Publisher to publish updates directly into WSUS using the local WSUS API, ensuring that update metadata is created locally and then inherited naturally by any downstream WSUS servers.&#x20;

### ConfigMgr (with WSUS and remote SUP)

In some environments, the SUP role is hosted on a remote Site System rather than the Site Server itself. In these cases, Publisher should be installed on that remote server, provided it is the top-level SUP.&#x20;

The key requirement is not the Site Server, but the server hosting the top-level WSUS instance, as Publisher must be co-located with WSUS to successfully publish update metadata.

## WSUS only (no ConfigMgr)

For environments using WSUS only (without ConfigMgr), Publisher must be installed on the top-level WSUS server, as this is where update metadata is authored.&#x20;

When WSUS synchronizes, that metadata is then replicated to any downstream WSUS servers, ensuring consistency across the hierarchy.

## Intune only

If you are using Publisher for Intune publishing only, it does not need to be installed on a WSUS or ConfigMgr server and can be installed on any suitable Windows system (see [Core Software Requirements](../requirements/core-requirements.md#software) for supported operating systems).&#x20;

As Publisher can create and manage applications and updates in Intune (through direct communication with Intune via Graph calls), it should be treated as a high-trust system and secured accordingly, with restricted access and appropriate credential protection.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Some customers who use only Intune choose to install Publisher on a dedicated Azure virtual machine. A B2-size virtual machine or equivalent is commonly used.&#x20;</p>
<p>The virtual machine should still meet or exceed the [minimum core requirements](../requirements/core-requirements.md) and [additional requirements needed for Intune publishing](../requirements/intune-requirements/).</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you intend to publish third-party applications and updates to Intune only, we generally recommend using Patch My PC Cloud, our cloud-based service, as it removes the need to manage on-premises infrastructure and simplifies ongoing operations.&#x20;</p>
<p>However, some customers are required to use Publisher instead (such as those with restrictions around enterprise application usage, environments that require GCC High, or scenarios where cloud-hosted services are not permitted).</p>
<p>In these cases, Publisher provides a fully supported alternative that allows publishing to Intune whilst keeping control within your environment.</p>
</blockquote>

## Mixed environments

If you are publishing updates to both ConfigMgr/WSUS and Intune, you should install Publisher on the top-level WSUS/SUP server.
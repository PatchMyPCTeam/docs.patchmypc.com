# ConfigMgr Software Requirements for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Patch My PC (PMPC) Publisher has the following ConfigMgr Software Requirements:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><a href="software.md#configmgr-operating-systems">Operating Systems</a></td><td valign="top"><a href="software.md#configmgr-supported-versions">Supported Versions</a></td><td valign="top"><a href="software.md#configmgr-remote-console">Remote Console</a></td><td valign="top"><a href="software.md#wsus-role">WSUS Role</a></td></tr></tbody></table>

## ConfigMgr Operating Systems

Publisher supports Microsoft Configuration Manager (ConfigMgr) when it is installed on versions of Windows Server currently supported by Microsoft’s supported lifecycle.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Use the <a href="https://learn.microsoft.com/en-us/lifecycle/products/">Search Product and Services Lifecycle Information</a> page to determine which versions of Windows Server are currently supported.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Publisher can be installed on Windows 11 only if it is used solely to publish applications and updates to Intune.</p>
</blockquote>

## ConfigMgr Supported Versions

ConfigMgr uses a Current Branch servicing model with two releases per year, typically in March and September. Each version is supported by Microsoft for 18 months from its release date. After 18 months, support ends for a version, and it no longer receives updates or technical support from Microsoft.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Starting with version 2609, ConfigMgr will transition to a single, annual release cadence.</p>
</blockquote>

Publisher supports ConfigMgr versions that are still within Microsoft’s supported lifecycle.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See <a href="https://learn.microsoft.com/en-us/lifecycle/products/microsoft-configuration-manager">Microsoft Configuration Manager</a> for more details of the support dates for each version of ConfigMgr.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Running unsupported or end-of-life versions of ConfigMgr is unsupported.</p>
</blockquote>

## ConfigMgr Remote Console

The ConfigMgr Remote Console exposes some SDK helper files Publisher utilizes to connect to the SMS Provider.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See <a href="https://learn.microsoft.com/intune/configmgr/core/servers/deploy/install/install-consoles">Install the Configuration Manager console</a> for more information on how to install the console.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>The installation file for the remote console is typically located on the Site Server share, e.g.:</p>
<p>**\\\site-server.contoso.com\SMS\_xxx\tools\ConsoleSetup\ConsoleSetup.exe**</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>A reboot is normally required after installing the ConfigMgr remote console; otherwise, you might see the following error logged in **PatchMyPC.log**:</p>
<p>_`An error occurred while connecting to Sms provider as System: Unable to find the Assembly: AdminUI.WqlQueryEngine, Version=5.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35 [PatchMyPC_Sccm.AssemblyResolver+AssemblyNotFoundException] HResult: -2146233088`_</p>
</blockquote>

If the ConfigMgr Remote Console is _not_ installed, the following message is also indicated in the Publisher when attempting to [Configure the SMS Provider](../../manage/configmgr-apps-tab/base-install-options/connection-source-options.md#configure-sms-provider-connection).

![Configure the SMS Provider - Missing SDK](/_images/image-(75).png "Configure the SMS Provider - Missing SDK")

## WSUS Role

For Publisher to code-sign PowerShell detection scripts for ConfigMgr applications, the WSUS role must be installed on the Publisher system.

While [limited WSUS API access](../intune-requirements/software.md#install-the-wsus-updateservices-api) may be sufficient for some operations (such as deserializing the Patch My PC Catalog), Publisher can _only_ use code-signing certificates to sign ConfigMgr detection scripts from the WSUS local certificate store.&#x20;

Certificates located in other Windows certificate stores are not supported for signing ConfigMgr application detection scripts.

Additionally, the WSUS role is required to publish updates, selected on the [WSUS Updates ](../../manage/wsus-updates-tab/)tab, which are synchronized from WSUS into ConfigMgr during a SUP sync.&#x20;

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [WSUS Requirements](../wsus-requirements/) for more information about the WSUS role requirements.</p>
</blockquote>
# ConfigMgr Network Requirements for  Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

If Patch My PC (PMPC) Publisher is installed on the Microsoft ConfigMgr Site Server, no additional network requirements are needed beyond those listed on the [core Publisher requirements](../core-requirements.md) page.&#x20;

However, if Publisher is installed on a remote device, the following additional requirements must also be met:

<table><thead><tr><th width="137" valign="top">Remote Port</th><th width="104" valign="top">Protocol</th><th width="161" valign="top">Purpose</th><th width="177" valign="top">Direction</th></tr></thead><tbody><tr><td valign="top">1433</td><td valign="top">TCP</td><td valign="top">Scan for supported products</td><td valign="top">Publisher TO Configmgr SQL Server</td></tr><tr><td valign="top">135</td><td valign="top">TCP</td><td valign="top">RPC Endpoint Mapper</td><td valign="top">Publisher TO SMS Provider</td></tr><tr><td valign="top">445</td><td valign="top">TCP</td><td valign="top">SMB</td><td valign="top">Publisher TO Server hosting the Content Source Folder</td></tr><tr><td valign="top">49152 - 65535 *</td><td valign="top">TCP</td><td valign="top">RPC Dynamic Port Range</td><td valign="top">Publisher TO SMS Provider</td></tr></tbody></table>

**\*** Default dynamic RPC port range.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The Site Server ultimately determines which SMS Provider is contacted. Consideration should be given to all Site Systems that hold the SMS Provider Site System role.</p>
</blockquote>
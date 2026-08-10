# Network

_Applies to: Patch My PC Publisher V2.x_

If the Publisher is installed on the Site Server, no additional network requirements are needed beyond those listed on the [core Publisher requirements](../core-requirements.md#network) page. However, if the Publisher is installed on a remote computer, the following additional requirements must also be met:-

| Remote Port      | Protocol | Purpose                     | Direction                                            |
| ---------------- | -------- | --------------------------- | ---------------------------------------------------- |
| 1433             | TCP      | Scan for supported products | Publisher > Configmgr SQL Server                     |
| 135              | TCP      | RPC Endpoint Mapper         | Publisher > SMS Provider                             |
| 445              | TCP      | SMB                         | Publisher > Server hosting the Content Source Folder |
| 49152 - 65535 \* | TCP      | RPC Dynamic Port Range      | Publisher > SMS Provider                             |

**\*** Default dynamic RPC port range.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The Site Server ultimately determines which SMS Provider is contacted. Consideration should be given for all Site Systems that hold the SMS Provider Site System role.</p>
</blockquote>
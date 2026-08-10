# Access and Permissions Reference for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*PRE-RELEASE DOCUMENTATION\*\*
>
> This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.
>
> Once this feature is released, it will be announced, and this banner will be removed.

Access to Patch My PC (PMPC) Publisher is controlled by both:

* Your Windows account
* The local groups on the server running the Publisher **PatchMyPCService**.

There is no separate Publisher login and no per-user password to manage. You grant someone access by adding their account (or a domain group they belong to) to the relevant group(s) on the server.

## How it works

* When you connect, Windows proves who you are. The **PatchMyPCService** then looks at which of its groups your account belongs to and grants the matching capabilities.
* Publisher automatically creates a series of local groups (all beginning with **PatchMyPC-**.) on the server the first time the **PatchMyPCService** starts.

> \*\*Important\*\*
>
> The \*\*PatchMyPC-\\\*\*\* groups are created without any members except for the access that local administrators already have. Until you add members, only server administrators can manage the Publisher.

* To grant access, an administrator adds a user or a domain group to one of those groups on the server. Nested domain groups are honored, so adding an AD group works, and its members inherit the access.
* Local administrators on the server automatically have full access to everything.

### Groups and Access

Add a user or domain group to the group that matches the access you want to delegate.

<table><thead><tr><th valign="top">Server group</th><th valign="top">Grants</th><th valign="top">Typical use</th></tr></thead><tbody><tr><td valign="top">Built-in Administrators</td><td valign="top">Everything</td><td valign="top">Server administrators - full control.</td></tr><tr><td valign="top">PatchMyPC-Administrator</td><td valign="top">Everything (same as a local administrator, for the Publisher).</td><td valign="top">Delegate full Publisher control without granting server administrator rights.</td></tr><tr><td valign="top">PatchMyPC-Reader</td><td valign="top">Read-only view of every area.</td><td valign="top">Auditors or staff who should see configuration but change nothing.</td></tr><tr><td valign="top">PatchMyPC-Wsus-Read<br>PatchMyPC-Wsus-Write</td><td valign="top">View/manage WSUS updates and settings.</td><td valign="top">WSUS owners.</td></tr><tr><td valign="top">PatchMyPC-ConfigMgr-Read<br>PatchMyPC-ConfigMgr-Write</td><td valign="top">View/manage ConfigMgr (SCCM) applications and settings.</td><td valign="top">ConfigMgr owners.</td></tr><tr><td valign="top">PatchMyPC-Intune-Read<br>PatchMyPC-Intune-Write</td><td valign="top">View/manage Intune applications and settings.</td><td valign="top">Intune owners.</td></tr><tr><td valign="top">PatchMyPC-Certificate-Write</td><td valign="top">View and manage code-signing and certificate configuration.</td><td valign="top">Whoever manages signing.</td></tr><tr><td valign="top">PatchMyPC-CloudConnection-Write</td><td valign="top">View and manage the Patch My PC Cloud connection.</td><td valign="top">Whoever manages the Cloud link.</td></tr><tr><td valign="top">PatchMyPC-CoreSettings-Write</td><td valign="top">View and manage core, global service settings.</td><td valign="top">Senior Publisher administrators.</td></tr><tr><td valign="top">PatchMyPC-ServiceAction-Write</td><td valign="top">View and trigger service actions such as sync and publish.</td><td valign="top">Operators who run syncs and publishes.</td></tr><tr><td valign="top">PatchMyPC-StagedContent-Read<br>PatchMyPC-StagedContent-ReadWrite</td><td valign="top">List/upload and delete files in the service content repository.</td><td valign="top">Advanced content management.</td></tr></tbody></table>

> \*\*Note\*\*
>
> A \*\*Write\*\* group always includes the matching \*\*Read\*\* access. If someone needs both read and write in an area, put them in the \*\*-Write\*\* group only. You do not need to add them to the \*\*-Read\*\* group.

## Granting access

To delegate access to a user:

1. On the server, open **Computer Management | Local Users and Groups | Groups** (or use your usual group management tooling).
2. Find the **PatchMyPC-\*** group for the access you want to grant.
3. Add the user, or domain group whose membership is managed centrally.

> \*\*Tip\*\*
>
> To ease maintenance, we recommend using domain groups. In this way, you only need to maintain membership of the relevant groups to control access without needing to access the server.

4. The change takes effect the next time the user connects. Users can [confirm their access](access-permissions-reference.md#confirming-access).

## Confirming access

Clicking the _Show Granted Permissions Shield_ (!\[Show Granted Permissions Shield]\(/\_images/image-(4585 "Show Granted Permissions Shield").png>)) at the bottom of the Publisher opens the read-only **Permissions** screen showing a list of every Publisher permission and whether the signed-in user has been granted it, evaluated against the server the user is connected to. This feature works the same for local and remote Settings consoles.

![](../../../.gitbook/assets/image-\(4586\).png)

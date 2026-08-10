# User Roles Reference for Patch My PC Cloud

_Applies to: Patch My PC Cloud_

User roles in the Patch My PC (PMPC) Cloud portal control which administrative tasks a user can perform.

* [Available Roles](user-roles-reference.md#available-roles)
* [Permissions Reference](user-roles-reference.md#permissions-reference)

## Available Roles

Users can be assigned the following User Roles in the PMPC Cloud Portal:

<table><thead><tr><th width="183.22222900390625" valign="top">Role</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">Read-Only Admin</td><td valign="top">Can access all areas of the Cloud portal, but cannot make any changes. This role is intended for audit purposes.</td></tr><tr><td valign="top">Read-Only Report Admin</td><td valign="top"><p>Only have <strong>Read-Only</strong> access to the <strong>Advanced/Patch Insights</strong> and <strong>Settings</strong> nodes.</p><p>They have Read-Only access to:</p><ul><li>All reports in the PMPC Cloud (both PMPC Client and Intune Reports).</li><li>The <strong>Company</strong> and <strong>Users</strong> sections of the <strong>Settings</strong> node.</li></ul><p>They cannot create, edit or delete existing reports or clients.</p></td></tr><tr><td valign="top">Custom App Admin</td><td valign="top"><p>Can perform the following Custom App-related actions in PMPC Cloud:</p><ul><li>Create</li><li>Modify</li><li>Delete custom applications in Patch My PC Cloud.</li></ul><p>They cannot:</p><ul><li>Create or edit On-Premises Publisher and Intune connections.</li><li>Access the <strong>Settings</strong> node.</li><li>Manage Branding.</li><li>Manage User access requests.</li></ul></td></tr><tr><td valign="top">Intune App Admin</td><td valign="top"><p>Can perform the following actions in PMPC Cloud:</p><ul><li>Create, modify, and delete deployments.</li><li>Manage licensing, branding, notifications, and the Sync schedule.</li><li>Disconnect  an Intune connection.</li></ul><p>This role only has <strong>Read-Only</strong> access to the <strong>Advanced/Patch Insights</strong> and <strong>Settings</strong> nodes.</p><p>They cannot:</p><ul><li>Create, edit, or delete On-Premise Publisher and Custom Apps.</li><li>Access the <strong>Settings</strong> node.</li><li>Manage User access requests.</li></ul></td></tr><tr><td valign="top">Full Admin</td><td valign="top">Can manage all aspects of PMPC Cloud, except for user management.</td></tr><tr><td valign="top">Full Admin with Access Management</td><td valign="top">Can manage all aspects of PMPC Cloud, including user management.</td></tr></tbody></table>

## Permissions Reference

Use the following tables to help you decide which role you should assign a user in Patch My PC Cloud either directly through the Portal or by making them a member of the relevant Entra ID Security Group assigned a role:

| [App Catalog](user-roles-reference.md#app-catalog) | [Discovery](user-roles-reference.md#discovery) | [Deployments](user-roles-reference.md#deployments) | [Domains](user-roles-reference.md#domains) |
| -------------------------------------------------- | ---------------------------------------------- | -------------------------------------------------- | ------------------------------------------ |
| [Events](user-roles-reference.md#events)           | [Migration](user-roles-reference.md#migration) | [Settings](user-roles-reference.md#settings)       |                                            |

### App Catalog

<table><thead><tr><th width="134.66668701171875">Functionality</th><th width="120.22222900390625">Read-Only Admin</th><th width="151.3331298828125">Read-Only Report Admin</th><th width="164.666748046875">Custom App Admin</th><th>Intune App Admin</th><th>Full Admin</th><th>Full Admin with Access Management</th></tr></thead><tbody><tr><td>Patch My PC Apps</td><td>Read</td><td>Read</td><td>Read</td><td>Read</td><td>Read</td><td>Read</td></tr><tr><td>Custom Apps</td><td>Read</td><td>Read</td><td>Read and Write</td><td>Read</td><td>Read and Write</td><td>Read and Write</td></tr><tr><td>Binary Free Apps</td><td>Read</td><td>Read</td><td>Read</td><td>Read and Write</td><td>Read and Write</td><td>Read and Write</td></tr></tbody></table>

### Deployments

| Read-Only Admin | Read-Only Report Admin | Custom App Admin | Intune App Admin | Full Admin     | Full Admin with Access Management |
| --------------- | ---------------------- | ---------------- | ---------------- | -------------- | --------------------------------- |
| Read            | No Access              | No Access        | Read and Write   | Read and Write | Read and Write                    |

### Discovery

| Read-Only Admin | Read-Only Report Admin | Custom App Admin | Intune App Admin | Full Admin     | Full Admin with Access Management |
| --------------- | ---------------------- | ---------------- | ---------------- | -------------- | --------------------------------- |
| Read            | No Access              | No Access        | Read and Write   | Read and Write | Read and Write                    |

### Domains

| Read-Only Admin | Read-Only Report Admin | Custom App Admin | Intune App Admin | Full Admin | Full Admin with Access Management |
| --------------- | ---------------------- | ---------------- | ---------------- | ---------- | --------------------------------- |
| No Access       | No Access              | No Access        | No Access        | No Access  | Read and Write                    |

### Events

| Read-Only Admin | Read-Only Report Admin | Custom App Admin | Intune App Admin | Full Admin | Full Admin with Access Management |
| --------------- | ---------------------- | ---------------- | ---------------- | ---------- | --------------------------------- |
| Read            | No Access              | No Access        | Read             | Read       | Read                              |

### Migration

| Read-Only Admin | Read-Only Report Admin | Custom App Admin | Intune App Admin | Full Admin     | Full Admin with Access Management |
| --------------- | ---------------------- | ---------------- | ---------------- | -------------- | --------------------------------- |
| Read            | No Access              | No Access        | No Access        | Read and Write | Read and Write                    |

### Settings

| Functionality           | Read-Only Admin | Read-Only Report Admin | Custom App Admin | Intune App Admin | Full Admin       | Full Admin with Access Management |
| ----------------------- | --------------- | ---------------------- | ---------------- | ---------------- | ---------------- | --------------------------------- |
| Company                 | Read            | Read                   | Read             | Read             | Read and Write   | Read and Write                    |
| Users                   | Read            | Read                   | No Access        | No Access        | No Access        | Read and Write                    |
| Environments & Licenses | Read            | Read                   | Read             | Read and Write   | Read and Write   | Read and Write                    |
| Connections             | Read            | No Access              | Read             | Read and Write\* | Read and Write\* | Read and Write\*                  |
| Branding                | Read            | No Access              | No Access        | Read and Write   | Read and Write   | Read and Write                    |
| Notifications           | Read            | No Access              | No Access        | Read and Write   | Read and Write   | Read and Write                    |
| Sync Schedule           | Read            | No Access              | No Access        | Read and Write   | Read and Write   | Read and Write                    |
| Naming Conventions      | Read            | No Access              | No Access        | Read and Write   | Read and Write   | Read and Write                    |
| Templates               | Read            | No Access              | No Access        | Read and Write   | Read and Write   | Read and Write                    |

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>**\*** Disconnecting Intune or Publisher from your PMPC Cloud Company can have a severe impact. Please ensure you read [Disconnect a Connection in Patch My PC Cloud](../connections/disconnect-connection.md) before removing a connection from your Cloud Company.</p>
</blockquote>
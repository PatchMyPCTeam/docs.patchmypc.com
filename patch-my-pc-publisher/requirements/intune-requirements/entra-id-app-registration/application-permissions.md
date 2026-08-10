# Application Permissions for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

To allow Patch My PC (PMPC) Publisher to automatically create, update, and assign Win32 applications in Microsoft Intune, the Entra ID app registration must be granted a specific set of Microsoft Graph application permissions.

The table below lists the required and optional permissions, along with an explanation of how each permission is used by Publisher.

<table data-search="true"><thead><tr><th valign="top">Permission</th><th valign="top">Description</th><th valign="top">Used For</th></tr></thead><tbody><tr><td valign="top">DeviceManagementApps.ReadWrite.All</td><td valign="top">Read and write Intune applications</td><td valign="top">Create, update, and manage Win32 applications</td></tr><tr><td valign="top">DeviceManagementConfiguration.Read.All</td><td valign="top">Read Intune configuration data</td><td valign="top">Read assignment filter properties</td></tr><tr><td valign="top">DeviceManagementManagedDevices.Read.All</td><td valign="top">Read managed device information</td><td valign="top">Device inventory used by auto-publishing logic</td></tr><tr><td valign="top">DeviceManagementRBAC.Read.All</td><td valign="top">Read role-based access control information</td><td valign="top">Read scope tags and RBAC assignments</td></tr><tr><td valign="top">DeviceManagementServiceConfig.ReadWrite.All</td><td valign="top">Read and write Intune service configuration</td><td valign="top">Manage Enrollment Status Page (ESP) settings</td></tr><tr><td valign="top">GroupMember.Read.All</td><td valign="top">Read group memberships</td><td valign="top">Assign applications to Entra ID groups</td></tr></tbody></table>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>The **DeviceManagementServiceConfig.ReadWrite.All** permission is required to manage blocking apps in the Enrollment Status Page (ESP). This is the only feature in Publisher that relies on this permission.</p>
<p>Although we understand this permission may appear broad, Microsoft does not currently provide a more granular Graph permission for updating the blocking apps configuration within ESP profiles.</p>
<p>If you revoke this permission from the app registration application, Publisher will no longer be able to manage or keep ESP blocking apps up to date in Intune.</p>
</blockquote>

These permissions are not strictly required for publishing, but improve the user experience within the Publisher UI.

<table><thead><tr><th width="169.55560302734375" valign="top">Permission</th><th valign="top">Description</th><th valign="top">Used For</th></tr></thead><tbody><tr><td valign="top">User.ReadBasic.All</td><td valign="top">Read basic user profile information</td><td valign="top">Display user names when resolving group members</td></tr><tr><td valign="top">Device.Read.All</td><td valign="top">Read device properties</td><td valign="top">Display device names when resolving group members</td></tr></tbody></table>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Although Publisher can detect that groups contain members, without the optional permissions above, Publisher cannot resolve those members into readable user or device names in any group picker interface.</p>
</blockquote>

## Add API Permissions

To add the required Microsoft Graph **Application permissions** to the Entra ID app registration used by the Publisher:

1. Sign in to the **Microsoft Entra admin center**.
2. Navigate to **Entra ID | App registrations**.
3. Select the app registration created for Patch My PC Publisher (for example, _Patch My PC Publisher – Intune Connector_).
4. In the left-hand menu, select **API permissions**.
5. Select **Add a permission**.

![Add an API Permission](/_images/image-(394).png "Add an API Permission")

6. In the **Request API permissions** pane, choose **Microsoft Graph**.
7. Select **Application permissions** (not Delegated permissions).
8. Use the search box or expand the relevant categories and add the permissions listed in the table above, including:
   * Required
     * **DeviceManagementApps.ReadWrite.All**
     * **DeviceManagementConfiguration.Read.All**
     * **DeviceManagementManagedDevices.Read.All**
     * **DeviceManagementRBAC.Read.All**
     * **DeviceManagementServiceConfig.ReadWrite.All**
     * **GroupMember.Read.All**
   * Optional
     * **User.ReadBasic.All**
     * **Device.Read.All**
9. Select **Add permissions** to apply the selected permissions.
10. Select **Grant admin consent** and confirm the prompt to approve the permissions.<br>

    ![Grant admin consent](/_images/image-(395).png "Grant admin consent")

The image below reflects the required, granted, permissions.

![Granted API Permissions](/_images/image-(396).png "Granted API Permissions")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Granting admin consent requires an account with sufficient privileges, such as **Global Administrator** or **Privileged Role Administrator**. Until admin consent is granted, Publisher will be unable to authenticate successfully or perform Intune operations.</p>
</blockquote>
# API Permissions

_Applies to: Patch My PC Publisher V2.x_

## Overview

To permit the Publisher to automatically create, update, and assign Win32 applications in Microsoft Intune, the Entra ID app registration must be granted a specific set of Microsoft Graph application permissions.

The table below lists the required and optional permissions, along with an explanation of how each permission is used by the Publisher.

| Permission                                  | Description                                 | Used For                                       |
| ------------------------------------------- | ------------------------------------------- | ---------------------------------------------- |
| DeviceManagementApps.ReadWrite.All          | Read and write Intune applications          | Create, update, and manage Win32 applications  |
| DeviceManagementConfiguration.Read.All      | Read Intune configuration data              | Read assignment filter properties              |
| DeviceManagementManagedDevices.Read.All     | Read managed device information             | Device inventory used by auto-publishing logic |
| DeviceManagementRBAC.Read.All               | Read role-based access control information  | Read scope tags and RBAC assignments           |
| DeviceManagementServiceConfig.ReadWrite.All | Read and write Intune service configuration | Manage Enrollment Status Page (ESP) settings   |
| GroupMember.Read.All                        | Read group memberships                      | Assign applications to Entra ID groups         |

> \*\*Important\*\*
>
> \*\*DeviceManagementServiceConfig.ReadWrite.All\*\*
>
> The Read and write Microsoft Intune configuration permission is required to manage blocking apps in the Enrollment Status Page (ESP). This is the only feature in the Publisher that relies on this permission.
>
> We understand this permission may appear broad, however, Microsoft does not currently provide a more granular Graph permission for updating the blocking apps configuration within ESP profiles.
>
> If you choose to revoke this permission from the app registration application, the Publisher will no longer be able to manage or keep ESP blocking apps up to date in Intune.

These permissions are not strictly required for publishing, but improve the user experience within the Publisher UI.

| Permission             | Description                         | Used For                                          |
| ---------------------- | ----------------------------------- | ------------------------------------------------- |
| **User.ReadBasic.All** | Read basic user profile information | Display user names when resolving group members   |
| **Device.Read.All**    | Read device properties              | Display device names when resolving group members |

> \*\*Note\*\*
>
> Without the optional permissions above, the Publisher can detect that groups contain members, but it cannot resolve those members into readable \*\*user or device names\*\* in any group picker interface.

## How to add an API Permission

Follow the steps below to add the required Microsoft Graph **Application permissions** to the Entra ID app registration used by the Publisher.

1. Sign in to the **Microsoft Entra admin center**.
2. Navigate to **Entra ID > App registrations**.
3. Select the app registration created for Patch My PC Publisher (for example, _Patch My PC Publisher – Intune Connector_).
4. In the left-hand menu, select **API permissions**.
5. Select **Add a permission**.

![Add an API Permission](/_images/image-(394 "Add an API Permission") (1).png>)

5. In the **Request API permissions** pane, choose **Microsoft Graph**.
6. Select **Application permissions** (not Delegated permissions).
7. Use the search box or expand the relevant categories and add the permissions listed in the table above, including:
   * Required
     * DeviceManagementApps.ReadWrite.All
     * DeviceManagementConfiguration.Read.All
     * DeviceManagementManagedDevices.Read.All
     * DeviceManagementRBAC.Read.All
     * DeviceManagementServiceConfig.ReadWrite.All
     * GroupMember.Read.All
   * Optional
     * User.ReadBasic.All
     * Device.Read.All
8. Select **Add permissions** to apply the selected permissions.
9.  Select **Grant admin consent** and confirm the prompt to approve the permissions.<br>

    ![Grant admin consent](/_images/image-(395 "Grant admin consent") (1).png>)

The image below reflects the required, granted, permissions.

![Granted API Permissions](/_images/image-(396 "Granted API Permissions") (1).png>)

> \*\*Note\*\*
>
> Granting admin consent requires an account with sufficient privileges, such as \*\*Global Administrator\*\* or \*\*Privileged Role Administrator\*\*. Until admin consent is granted, the Publisher will not be able to authenticate successfully or perform Intune operations.
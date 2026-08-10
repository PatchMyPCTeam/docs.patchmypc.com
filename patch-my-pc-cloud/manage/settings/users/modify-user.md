# Modify a User in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Once a user has been successfully created in Patch My PC (PMPC) Cloud, they can be modified in the following ways:

* [Changing the user’s role](modify-user.md#modifying-the-role-assigned-to-a-user)
* [Managing Access Management privileges for a User](modify-user.md#managing-access-management-privileges-for-a-user)

## Modifying the role assigned to a User

To modify the role assigned to a user:

1. Navigate to the **Users** page.
2.  In the **Roles** column, click the down arrow and select the relevant role you want to assign to the user.\
    \
    For example, to change the user’s current role from **Full Admin** to **Custom App Admin**, click the down arrow beside the current role, then choose **Custom App Admin**.<br>

    ![Selecting the required user role from the list of roles dropdown](../../../../.gitbook/assets/image-\(2820\).png)

    \
    The role for the user will be updated and the **Success - Role changed** notification is displayed.<br>

    !["Success - Role changed" notification](../../../../.gitbook/assets/image-\(2350\).png)

> \*\*Note\*\*
>
> See \[User Roles]\(user-roles-reference.md) for more information on the user roles available.

## Managing Access Management privileges for a User

To manage whether a user is granted the **Access Management** privilege:

1. Navigate to the **Users** area.
2. In the **Roles** column, slide the **Access Management** slider to the right for the user you want to grant this permission.

![Using the slider to grant "Access Management" privileges](../../../../.gitbook/assets/image-\(2351\).png)

The **Success - Role changed** notification is displayed.

![The "Success - Role changed" notification](../../../../.gitbook/assets/image-\(2352\).png)

> \*\*Note\*\*
>
> To revoke this privilege, slide the \*\*Access Management\*\* slider to the left. If you are the last user in your company with this privilege, you will be unable to revoke it.
>
> If you try revoking it for yourself and there is at least one other user account with this privilege, you will see the following dialog box warning you that if you revoke access management you will be unable to manage user accounts in the portal.
>
> !\["Are you sure you want to revoke access management from your account" pop up]\(/\_images/image-(2461 "\\"Are you sure you want to revoke access management from your account\\" pop up").png>)

> \*\*Important\*\*
>
> As we recommend you have at least two users with Access Management privileges in your environment, if the portal detects you only have one, you will see the following warning message at the top of the portal:
>
> \*\*You currently have only one user with Access Management privileges. To prevent access issues in the future, please add a second user with Access Management privileges.\*\*
>
> Granting at least two users this privilege will remove this message. Likewise, if revoking Access Management privileges for a user results in only one user in your environment having this privilege, you will see the warning notification again.

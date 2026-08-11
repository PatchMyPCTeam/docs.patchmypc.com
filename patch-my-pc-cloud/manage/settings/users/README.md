# Manage Users In Patch My PC Cloud

_Applies to: Patch My PC Cloud_

A _user_ needs an account to sign in and use any of the features of Patch My PC (PMPC) Cloud.

There are two ways to grant access:

* Directly through the PMPC Portal as detailed below.
* By using Entra ID Security Groups.

All user account-related tasks are performed from the **Users** node of the PMPC portal, which is accessed by:

1. Sign in to the PMPC portal [https://portal.patchmypc.com/](https://portal.patchmypc.com/)
2.  Navigate to **Settings | Users**.<br>

    ![Navigating to "Settings | Users"](../../../../.gitbook/assets/image-\(988\).png)

The **Users** page is then displayed, allowing you to complete the following tasks:

* [Add a User](add-user.md)
* [Modify a User](modify-user.md)
* [Delete a User](delete-user.md)

!["Users" page](<../../../../.gitbook/assets/image-(989) (1).png>)

> \*\*Note\*\*
>
> When you first set up a PMPC Cloud company, the user creating the company is automatically assigned the \*\*Full Admin with Access Management\*\* role. To avoid access issues (such as this user leaving your company and not passing on their credentials/setting up another user with this role), we recommend either:
>
> \* \[Adding a second user]\(add-user.md) and assigning them this role.
>
> \* \[Adding an Entra ID group]\(using-entra-id-security-groups/add-entra-id-security-group.md) and assigning it the \*\*Full Admin with Access Management\*\* role.
>
> Once you’ve done this, we recommend you use Entra ID security groups to manage any additional users who need to have access to your PMPC Cloud company.
>
> You will see the banner at the top of the portal warning you only have one user with Access Management privileges until you create at least another user or grant an Entra ID Security Group this privilege.

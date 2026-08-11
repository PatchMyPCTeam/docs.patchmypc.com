# Remove an Entra ID Security Group in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

> \*\*Important\*\*
>
> When you remove an Entra ID Security Group, you are only removing that group’s access to your Patch My PC (PMPC) Cloud Company. You are not deleting the group from Entra ID.

To remove an Entra ID Security Group from PMPC Cloud:

1.  In the PMPC Cloud portal, navigate to **Settings | Users**.<br>

    ![Navigating to "Settings | Users"](../../../../../.gitbook/assets/image-\(2936\).png)
2.  Click the **Entra ID Groups** tab.<br>

    ![Clicking the "Entra ID Groups" tab](../../../../../.gitbook/assets/image-\(2937\).png)
3. Click the trashcan beside the relevant Entra ID Security Group you want to remove.

> \*\*Important\*\*
>
> You need to have at least one user or Entra ID Security Group assigned the \*\*Full Admin with Access Management\*\* user role at all times. You will be unable to delete an Entra ID Security Group assigned this role unless you have either one other user or Entra ID Security Group assigned this role.

![Clicking the trashcan beside the relevant Entra group you want to delete](../../../../../.gitbook/assets/image-\(2938\).png)

4. On the **Are you sure you want to remove <**_**group\_name**_**>** dialog box, click **Yes** to confirm the removal.

!['Are you sure' you want to remove group dialog box](../../../../../.gitbook/assets/image-\(3634\).png)

The portal auto-refreshes to show the group has been removed and the **Success – Group deleted** notification is shown.

![Portal auto-refreshing to show the group has been removed and the "Success – Group deleted" notification is shown](../../../../../.gitbook/assets/image-\(2940\).png)

When you remove an Entra ID Security Group, the **Group Role Removed** event is written to the **Events** node.

# Modify an Entra ID Security Group in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Once an Entra ID Security Group has been added to Patch My PC (PMPC) Cloud, you can change the role assigned to that group.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You cannot change the membership of an Entra ID Security Group from within the PMPC Cloud portal.</p>
</blockquote>

To change the role assigned to an Entra ID Security Group:

1.  In the PMPC Cloud portal, navigate to **Settings | Users**.<br>

    ![Navigating to "Settings | Users"](/_images/image-(2947).png "Navigating to “Settings | Users”")


2.  Click **Entra ID Groups**.<br>

    ![Clicking "Entra ID Groups"](/_images/image-(2948).png "Clicking “Entra ID Groups”")


3. Click the dropdown arrow in the **Group Role** column beside the group whose role you want to modify and select the new role.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>You will be unable to change the group’s role from **Full Admin with Access Management** to another role if this is the only group assigned that role and no users under the **Active Users** tab have been assigned the **Full Admin with Access Management** role.</p>
</blockquote>

![Clicking the dropdown arrow in the "Group Role" column beside the group whose role you want to modify and selecting the new role](/_images/image-(2949).png "Clicking the dropdown arrow in the “Group Role” column beside the group whose role you want to modify and selecting the new role")

The portal auto-refreshes to show the new role assigned to the group and the **Success – Role changed** notification is shown.

![Portal auto-refreshing to show the new role assigned to the group and the "Success – Role changed" notification is shown](/_images/image-(2950).png "Portal auto-refreshing to show the new role assigned to the group and the “Success – Role changed” notification is shown")

When you change the role of an Entra ID Security Group, the **Group role with name <**_**group\_name**_**> and id <**_**entra\_id\_security\_group\_id**_**> was changed to role <**_**new\_user\_role**_**>** event is written to the **Events** node.&#x20;
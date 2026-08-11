# Add an Entra ID Security Group in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

To add an Entra ID Security Group to Patch My PC (PMPC) Cloud:

1. Create the relevant group in Entra ID and add the relevant users.

> \*\*Note\*\*
>
> We recommend you create an Entra ID group for each \[PMPC Cloud User Role]\(../user-roles-reference.md) you plan to use.

2. In the PMPC Cloud portal, navigate to **Settings | Users**

![Navigating to 'Settings | Users'](/_images/image-(3687).png)

3. Click **Add Group**

![Clicking 'Add Group'](/_images/image-(3688).png)

4. On the **Available Groups** screen, click the checkbox beside the relevant Entra ID Security Group you want to add, then select the PMPC Cloud role you want to assign to this group from the **Role** dropdown.

![Selecting the relevant Entra ID group to add and which role it will be assigned in PMPC Cloud](/_images/image-(3689).png)

> \*\*Note\*\*
>
> If you assign an Entra ID Security Group the \*\*Full Admin with Access Management\*\* role, all of this group’s members will receive notifications such as access requests, new version notifications for Binary Free apps (if configured), claim ownership notifications, etc.

The selected Entra ID Security Group and the role you’ve assigned it appear in your portal

![The selected Entra ID Security Group and the role you've assigned it appear in your portal](/_images/image-(3690).png)

5. Repeat Step 4 to add any additional groups/roles.

> \*\*Important\*\*
>
> In the current release, you can add up to ten Entra ID Security Groups.

6. Click **Add**

![Clicking 'Add'](/_images/image-(3692).png)

The portal auto-refreshes, showing that the selected groups have been added, and the **Success – Group created** notification is shown.

![Portal auto-refreshes, showing the selected groups have been added and the 'Success – Group created' notification is shown](/_images/image-(3695).png)

When you add an Entra ID Security Group, the **Group role with id <**_**entra\_id\_security\_group\_id**_**> was created with role <**_**user\_role**_**>** event is written to the **Events** node.

> \*\*Note\*\*
>
> If a user belongs to multiple Entra ID Security groups with different permission levels, their effective permissions will reflect the highest level granted across those groups, as they inherit the combined set of all assigned permissions—unless an explicit Deny takes precedence.
>
> Likewise, if a user has been added directly to the portal using the \[Add a User]\(../add-user.md) process and they are also a member of one or more Entra ID Security Groups assigned different roles, the same applies, i.e., their effective role will be a combination of all of the roles assigned to them directly in the portal and to any Entra ID Groups they are a member of.
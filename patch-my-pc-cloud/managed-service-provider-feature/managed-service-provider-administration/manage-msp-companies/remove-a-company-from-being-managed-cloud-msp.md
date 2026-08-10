# Remove a Company from being Managed (Cloud MSP)

_Applies to: Patch My PC Cloud_

If a parent Patch My PC (PMPC) Cloud Managed Service Provider (MSP) company no longer wants to manage a child company, they can remove the Intune connection and then delete the company.

Likewise, if a child company no longer wishes to be managed by an MSP, they can unlink themselves from the MSP using the [Unlink a Child Company](remove-a-company-from-being-managed-cloud-msp.md#unlink-a-child-company) process below.

> \*\*Note\*\*
>
> To perform this process, you must be signed in as a user who is either a \*\*Full Admin\*\* or \*\*Full Admin with Access Management\*\*.

> \*\*Important\*\*
>
> Please note the following:
>
> \* You cannot delete a child company:
>
> \* If at least one user/group in that company is not assigned the \*\*Full Admin with Access Management\*\* user role.
>
> \* Without first removing the Intune connection. If you attempt to do this, you will see the \[Intune connection with the same Id found in another environment!]\(../../../troubleshoot/environments/intune-connection-with-the-same-id-found-in-another-environment-error-in-cloud.md) error.
>
> \* An MSP admin cannot delete a child company from the Company node using the \[Delete your Company]\(../../../manage/settings/company-settings/delete-company.md) process, as the option is unavailable.\\
>
> \\
>
> !\[Delete options unavailable on a child company]\(/\_images/image-(2798 "Delete options unavailable on a child company").png>)<br>
>
> \* Any Custom Apps for MSPs have been shared with and deployed from a child company, either unlinking or deleting a child company (either from the parent or child company), will:
>
> \* Delete the Custom App from the App Catalog of the child company.
>
> \* Delete any active deployments of the relevant Custom Apps.
>
> \* If you delete a child company that has App Sets deployed to it from the Parent Company, any deployments for apps that belong to those App Sets will be automatically deleted as part of the unlinking process.
>
> \* If an App Set is deployed to multiple companies, when the last company the App Set is deployed to is removed, the App Set itself will be automatically deleted.

### Remove the Intune connection for a Child Company

> \*\*Important\*\*
>
> If you remove the Intune connection for a Child Company that has App Sets deployed to it from the Parent Company, any deployments for apps that belong to those App Sets will be automatically deleted as part of the connection removal.
>
> If an App Set is deployed to multiple companies, when the last Intune connection is deleted from the last company an App Set is deployed to, the App Set itself will be automatically deleted.

To remove the Intune connection for a Child Company:

1. On the parent company, sign in as a user who is either a **Full Admin** or **Full Admin with Access Management**.
2. Navigate to the **MSP Customers** node.
3. Click your user name in the top right-hand corner.

![Clicking  your user name in the top right-hand corner](../../../../.gitbook/assets/image-\(1069\).png)

4. Select the child company to switch to.

![Selecting the child company](../../../../.gitbook/assets/image-\(1070\).png)

The portal refreshes to show the child company has been selected as the **Managed By <**_**msp\_name**_**>** indicator is shown in the header.

![](../../../../.gitbook/assets/image-\(1071\).png)

5. If the child company is no longer required and is going to be deleted, proceed to Step 6.\
   \
   If the child company is not going to be deleted, you should navigate to the **Users** node and follow the [Invitation from an Administrator](../../../manage/settings/users/add-user.md#invitation-from-an-administrator) process to add at least one user who is a member of the child company.\
   \
   This user should be assigned the **Full Admin with Access Management** role as they will be responsible for the ongoing management of the child company once the parent company no longer manages it.
6. Navigate to **Settings | Environments**.

![Navigating to the 'Environments' node](../../../../.gitbook/assets/image-\(1072\).png)

7. Click **Delete** beside Intune.

![Clicking 'Delete' beside 'Intune'](../../../../.gitbook/assets/image-\(1073\).png)

8. On the **Are you sure you want to disconnect Intune** popup, click **OK**.

![Clicking 'OK' on the 'Are you sure you want to disconnect Intune' popup](../../../../.gitbook/assets/image-\(1074\).png)

The portal refreshes to show that the Intune connection has been deleted and the **Success – Intune disconnected** notification is displayed.

![Portal refreshing to show that the Intune connection has been deleted and the 'Success – Intune disconnected' notification is displayed](../../../../.gitbook/assets/image-\(1075\).png)

You can now follow the [Delete a Child Company](remove-a-company-from-being-managed-cloud-msp.md#delete-a-child-company) process if you want to delete the child company.

### Delete a Child Company

Once the Intune connection for a Child Company has been removed, to delete a child company from a parent company:

1. On the parent company, sign in as a user who is either a **Full Admin** or **Full Admin with Access Management**.
2. Navigate to the **MSP Customers** node.
3. Click the trashcan () beside the child company you want to remove.

![Click the trashcan beside the child company you want to remove](../../../../.gitbook/assets/image-\(614\).png)

4. On the **Are you sure you want to delete <**_**child\_company\_name**_**> customer** dialog box, click **Yes**.

![](../../../../.gitbook/assets/image-\(615\).png)

The portal refreshes to show the child company has been deleted and the **Success – Customer <**_**child\_company\_name**_**> deleted** notification is shown.

![](../../../../.gitbook/assets/image-\(616\).png)

### Unlink a Child Company

If a child company no longer wishes to be managed by a parent MSP company, it can be unlinked from the parent MSP company.

> \*\*Note\*\*
>
> To perform this process requires you sign in as a user that is either a \*\*Full Admin\*\* or \*\*Full Admin with Access Management\*\*.

To unlink a child company from a parent MSP company:

1. Verify the parent MSP company has created at least one user in the child company (by following the [Invitation from an Administrator](../../../manage/settings/users/add-user.md#invitation-from-an-administrator) process).\
   \
   This user should be assigned the **Full Admin with Access Management** role as they will be responsible for the ongoing management of the child company once the parent company no longer manages it.
2. Sign in to the child company using a user with either the **Full Admin** or **Full Admin with Access Management** role.
3.  Navigate to **Settings | Company**.<br>

    ![Navigating to 'Settings | Company'](../../../../.gitbook/assets/image-\(2804\).png)
4. Scroll down to the **Your company is managed by an MSP (Managed Service Provider)** section, then click **Unlink MSP**

![Clicking 'Unlink MSP'](../../../../.gitbook/assets/image-\(2805\).png)

5. On the **Are you sure you want to Disconnect MSP** dialog box, click **Yes**.

![Clicking 'Yes' on the 'Are you sure you want to Disconnect MSP' dialog box](../../../../.gitbook/assets/image-\(2806\).png)

6. The **Customer <**_**parent\_company\_name**_**>** notification is displayed and you will prompted to enter a non-MSP+ license for the child company as it has been disconnected from the parent MSP company.

![Prompt to enter a non-MSP+ license key on the child company](../../../../.gitbook/assets/image-\(2807\).png)

7. Enter the license key and click **Activate Now**.

![Entering the license key and clicking 'Activate Now'](../../../../.gitbook/assets/image-\(805\).png)

> \*\*Note\*\*
>
> You cannot use a trial license for a company that an MSP has previously managed.

8.  On the **You have successfully activated your license** popup, click **Close**.

    ![Clicking 'Close' on the 'You have successfully activated your license' popup](../../../../.gitbook/assets/image-\(2809\).png)

The following event is created on the parent MSP company so they know a user at the child site has unlinked the child company from the parent company:

**Managed Company Relationship for <**_**child\_company\_name**_**> Removed by <**_**user\_name**_**>**

![Event on the parent company that a user at the child company has unlinked it from the parent company.](../../../../.gitbook/assets/image-\(2810\).png)

Also, the child company is automatically deleted from the parent company.

![Child company automatically deleted from the parent company](../../../../.gitbook/assets/image-\(2811\).png)

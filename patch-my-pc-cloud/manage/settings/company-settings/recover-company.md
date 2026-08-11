# Recover your Patch My PC Cloud Company

_Applies to: Patch My PC Cloud_

To prevent access issues to your Patch My PC (PMPC) Cloud company, we highly recommend granting at least two users the [Full Admin with Access Management](../users/user-roles-reference.md) user role.

> \*\*Note\*\*
>
> If you have only one user assigned the Full Admin with Access Management role, the \[You currently have only one user with Access Management privileges]\(../../../troubleshoot/users/you-currently-have-only-one-user-with-access-management-privileges-error-in-cloud.md) banner is displayed.

However, if you have not done this and the only user with this role leaves your company, you will no longer be able to manage both existing and new users within your PMPC Company.

Your only option is to attempt to recover your company, which involves providing us with specific details from the same Entra ID tenant as your PMPC Company to confirm your identity and validate your request. If successful, the user account performing the recovery will be granted the Full Admin with Access Management role.

> \*\*Note\*\*
>
> See the \[Creating an App Registration in Entra ID]\(../../../technical-references/entra-id-reference/create-an-app-registration-in-entra-id.md) process for details on how to create and obtain these values.

> \*\*Important\*\*
>
> We provide the functionality to disable a PMPC company from being recovered. However, we do not display and enable this by default because if it's enabled and you lose access to your company for whatever reason, neither of us can regain access to that company. This means you'll lose everything and need to create a new company and reconfigure it to match the old one. If you really want to enable this feature, please [open a support case](https://patchmypc.com/technical-support).

> \*\*Note\*\*
>
> If your PMPC Cloud company is either a Managed Service Provider Parent or Child company, you should follow the \[Recover an MSP Patch My PC Cloud Company]\(../../../managed-service-provider-feature/managed-service-provider-administration/manage-msp-companies/recover-an-msp-patch-my-pc-cloud-company.md) process.

## Requirements

The user performing the recovery process does not need to be an existing user in the PMPC Company being recovered.

However, to verify the ID of the user performing the recovery (who must have the **Application Administrator** role or higher), and ensure the person performing the action is an administrator of the company, we ask them to create various objects in the same Entra ID tenant as the PMPC Company being retrieved.

Once created, the values of these new objects and other existing objects need to be entered into our **Claim Ownership** wizard.

Although a user with these privileges can complete the Entra ID process and provide the required values to the user performing the recovery, we recommend that the same person creating the required objects perform the recovery in PMPC Cloud to avoid sharing the secrets with another user.

Also, the company that you are trying to recover access to must have been configured to [Enable Company Recovery](company-recovery.md).

## Recovering a Company

To recover a PMPC Company:

1. If the user attempting the recovery is an existing user and is already logged in, they must sign out of any portal sessions for that company.
2. Navigate to [https://portal.patchmypc.com/](https://portal.patchmypc.com/)

![Navigating the sign in page](/_images/image-(1190).png)

3. Click **Sign In** if the user attempting the recovery can sign in to multiple companies in PMPC Cloud.
4. Click **Sign Up** if any of the following applies to the user attempting recovery:
   1. The user only belongs to a single company i.e. the account is not used to manage multiple companies in PMPC Cloud.
   2. The user has not signed into the portal before and is not associated with an existing PMPC Cloud company.
5. On the **Select the Company You Want to Sign In To** screen, click **Recover Company**.

![Clicking 'Recover Company'](/_images/image-(2657).png)

The **Claim Ownership** wizard starts.

!['Claim Ownership' wizard](/_images/image-(3476).png)

6. From the **Company to Claim** dropdown, select the company you want to recover.

!['Company to Claim' dropdown](/_images/image-(3477).png)

The last five characters of the **Entra ID** to which your PMPC Company belongs are shown.

![Last five characters of the Entra ID to which your PMPC Company belongs are shown.](/_images/image-(3479).png)

7. Using the [Creating an App Registration in Entra ID](../../../technical-references/entra-id-reference/create-an-app-registration-in-entra-id.md) process, verify that the last five characters of the Entra ID match the last five characters of the **Directory (tenant) ID**.\
   \
   If they match, continue.\
   \
   If they don’t match, you are looking in the wrong Entra ID tenant and the ownership process will fail with the [Error - Claim Ownership Failed.](../../../troubleshoot/company/error-claim-ownership-failed-when-trying-to-recover-a-cloud-company.md)
8.  Continue following the [Creating an App Registration in Entra ID](../../../technical-references/entra-id-reference/create-an-app-registration-in-entra-id.md) process to create the relevant App Registration in your Entra ID tenant.\
    \
    From this process, you are going to need the following values:<br>

    • Object ID\
    • Application (client) ID for the PMPC Recovery App Registration\
    • PMPC Recovery client secret (the Entra ID App Registration Secret value).
9. Copy the following values from the [Creating an App Registration in Entra ID](../../../technical-references/entra-id-reference/create-an-app-registration-in-entra-id.md) process to their respective fields of the **Claim Ownership** wizard:

> \*\*Important\*\*
>
> You cannot use an App Registration that was created more than 72 hours ago to perform a company recovery. If you have an existing App Registration older than this, you must create a new one before continuing.
>
> After creating a new App Registration, we recommend waiting up to 30 minutes before using it for a company recovery. This allows time for the App Registration to fully propagate and become available across Microsoft Entra ID and Microsoft Graph services.

| Entra ID Value                                                 | Claim Ownership field |
| -------------------------------------------------------------- | --------------------- |
| Object ID                                                      | Object ID             |
| Application (client) ID for the PMPC Recovery App Registration | Client ID             |
| PMPC Recovery client secret.                                   | Secret                |

![Entering values into the 'Claim Ownership' screen](/_images/image-(3480).png)

10. Click **Continue**.

![Clicking 'Continue'](/_images/image-(3481).png)

11. If the user performing the recovery is an existing user within the PMPC Company, go to Step 15.
12. If the user performing the recovery is not an existing user within the PMPC Company, they will see the **User Info** page.

!['User Info' page](/_images/image-(2664).png)

13. Complete the **First Name** and **Last Name** fields, which will be used to create the new account and assign them the **Full Admin with Access Management** role if the recovery is successful.
14. Review the **Terms and conditions** and if you are happy, click to check the **Accept all Terms and conditions** checkbox, then click **Continue**.<br>

    ![Checking the 'Accept all Terms and conditions' checkbox, then clicking 'Continue'.](/_images/image-(2665).png)
15. The supplied information is checked.\
    \
    If the recovery process fails, see the **Resolution** section of the [Error – Claim Ownership Failed](../../../troubleshoot/company/error-claim-ownership-failed-when-trying-to-recover-a-cloud-company.md) article for troubleshooting help.\
    \
    If the recovery process is successful, the **Ownership Granted** popup is displayed.<br>

    !['Ownership Granted' popup](/_images/image-(2667).png)

> \*\*Important\*\*
>
> You have three attempts to recover a company. If recovery fails after the third attempt, you will need to wait 12 hours before you can attempt recovery again.

16. Click **Close** to complete the recovery process and display the **App Catalog** page of the recovered company.<br>

    !['App Catalog' page of the recovered company](/_images/image-(2668).png)

    \
    If you navigate to the **Users** node, you will see that the account used to perform the recovery process has been created (if applicable) and assigned the **Full Admin with Access Management** role.<br>

    !['Users' node showing the user account used to perform the recovery process has been created (if applicable) and assigned the 'Full Admin with Access Management role'.](/_images/image-(2669).png)

    \
    If you navigate to the **Events** node, you will see that the **Company Ownership Approved for <**_**user\_name**_**>** event confirming the name of the user who performed the recovery process.<br>

    ![](/_images/image-(2670).png)

    \
    The previous owner will also receive an email with the subject **Access Recovered to “PMPC\_<**_**company\_name**_**>”**, containing details of who performed the recovery and when.

> \*\*Note\*\*
>
> See \[Example Account Recovery Email]\(../../../technical-references/cloud-email-reference/example-cloud-account-recovery-email.md) for more details and an example of the email.

> \*\*Important\*\*
>
> Once you have successfully completed the recovery process, to avoid potential security issues and prevent unwanted re-use of these objects, you should follow the \[Deleting an App Registration in Entra ID]\(../../../technical-references/entra-id-reference/delete-an-app-registration-in-entra-id.md) process to delete the recovery objects created in your Entra ID.
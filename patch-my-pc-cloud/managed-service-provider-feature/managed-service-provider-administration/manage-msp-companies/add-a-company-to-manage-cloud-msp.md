# Add a Company to Manage (Cloud MSP)

_Applies to: Patch My PC Cloud_

Once the parent MSP company has been configured in Patch My PC (PMPC) Cloud with an MSP Plus license, you can add the relevant child companies to be managed.

You have two options for setting up child companies:

* If the company you want to add is already using PMPC Cloud, then you should follow the [Inviting a User to an MSP Company](../manage-msp-users/#inviting-a-user-to-an-msp-company) process.
* If the company you want to add is not already using PMPC Cloud, then you should follow the [Adding a Company to be Managed](add-a-company-to-manage-cloud-msp.md#adding-a-company-to-be-managed) process.

> \*\*Important\*\*
>
> We currently do not support a parent MSP company from taking over the management of an existing child PMPC Cloud company.

### Adding a Company to be Managed

To add a new PMPC Cloud company to be managed using the MSP Feature:

1. Sign in to the parent company where the MSP license has been enabled.
2.  Click the **MSP Customers** node.

    ![Clicking the 'MSP Customers' node](/_images/image-(2776).png)
3. On the **MSP Customers** page, click **Add Customer**.

![Clicking 'Add Customer'](/_images/image-(617 "Clicking 'Add Customer'") (1).png>)

4. Click **Connect** under the **Intune Connection** section.

![Clicking 'Connect' under the 'Intune Connection' section](/_images/image-(618 "Clicking 'Connect' under the 'Intune Connection' section") (1).png>)

5. On the **Sign in** screen, enter the Entra ID that is a Global Admin in the child company or click to select the relevant account from the list of already signed-in accounts. Then click **Next**.

!['Sign in' screen](/_images/image-(2780).png)

6. Enter the password and click **Sign in**.

![Entering the password and clicking 'Sign in'](/_images/image-(2781).png)

7. On the **Permissions requested** screen, click **Accept**.

> \*\*Note\*\*
>
> The account you are using to connect to the child company’s Intune tenant needs to have the \*\*Global Administrator\*\* role in the child company’s Entra ID to approve the PMPC Cloud enterprise app.
>
> We require these permissions to connect to the child company’s Intune tenant.
>
> See \[Permissions required for the Intune Apps]\(../../../technical-references/cloud-permissions-reference/permissions-required-for-intune-apps.md) for more details.

![Clicking 'Accept' on the 'Permissions requested' page](/_images/image-(2782).png)

> \*\*Tip\*\*
>
> You can click the down arrow beside each permission to get more information.

8. Verify Intune has **Connected** successfully.

![Intune connected successfully](/_images/image-(619 "Intune connected successfully") (1).png>)

9. On the **Create New Customer** page, enter the name of the customer to be managed in the **Customer Name** field.

> \*\*Note\*\*
>
> We support the characters \*\*À-ÿ\*\* (which includes characters from the Latin-1 Supplement Unicode block) for customer names.

![Enter the name of the customer in the 'Customer Name' field](/_images/image-(620 "Enter the name of the customer in the 'Customer Name' field") (1).png>)

10. Click **Terms and Conditions**.

![Clicking 'Terms and Conditions'](/_images/image-(621 "Clicking 'Terms and Conditions'") (1).png>)

11. Review the Terms and Conditions, and once you are happy, click the **X** in the top right-hand corner to return to the **Create New Customer** screen.

![Reviewing the Terms and Conditions](/_images/image-(3009).png)

12. Check the **Accept all Terms and conditions** checkbox, then click **Create**.

![Accepting the Terms and conditions then clicking 'Create'](/_images/image-(622).png)

The portal refreshes, showing the newly added customer and the **Success - Child Customer <**_**customer\_name**_**> created** notification.

![](/_images/image-(623) (1).png>)
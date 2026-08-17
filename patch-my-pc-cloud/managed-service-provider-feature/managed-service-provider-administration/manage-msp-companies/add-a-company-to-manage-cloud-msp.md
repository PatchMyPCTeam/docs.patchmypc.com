# Add a Company to Manage (Cloud MSP)

_Applies to: Patch My PC Cloud_

Once the parent MSP company has been configured in Patch My PC (PMPC) Cloud with an MSP Plus license, you can add the relevant child companies to be managed.

You have two options for setting up child companies:

* If the company you want to add is already using PMPC Cloud, then you should follow the [Inviting a User to an MSP Company](../manage-msp-users/#inviting-a-user-to-an-msp-company) process.
* If the company you want to add is not already using PMPC Cloud, then you should follow the [Adding a Company to be Managed](add-a-company-to-manage-cloud-msp.md#adding-a-company-to-be-managed) process.

{% hint style="warning" %}
**Important**

We currently do not support a parent MSP company from taking over the management of an existing child PMPC Cloud company.
{% endhint %}

### Adding a Company to be Managed

To add a new PMPC Cloud company to be managed using the MSP Feature:

1. Sign in to the parent company where the MSP license has been enabled.
2.  Click the **MSP Customers** node.

    <figure><img src="../../../../.gitbook/assets/image (2776).png" alt="Clicking the &#x27;MSP Customers&#x27; node" width="563"><figcaption></figcaption></figure>
3. On the **MSP Customers** page, click **Add Customer**.

<figure><img src="../../../../.gitbook/assets/image (617).png" alt="Clicking &#x27;Add Customer&#x27;" width="563"><figcaption></figcaption></figure>

4. Click **Connect** under the **Intune Connection** section.

<figure><img src="../../../../.gitbook/assets/image (618).png" alt="Clicking &#x27;Connect&#x27; under the &#x27;Intune Connection&#x27; section" width="213"><figcaption></figcaption></figure>

5. On the **Sign in** screen, enter the Entra ID that is a Global Admin in the child company or click to select the relevant account from the list of already signed-in accounts. Then click **Next**.

<figure><img src="../../../../.gitbook/assets/image (2779).png" alt="&#x27;Sign in&#x27; screen" width="510"><figcaption></figcaption></figure>

6. Enter the password and click **Sign in**.

<figure><img src="../../../../.gitbook/assets/image (2781).png" alt="Entering the password and clicking &#x27;Sign in&#x27;" width="515"><figcaption></figcaption></figure>

7. On the **Permissions requested** screen, click **Accept**.

{% hint style="info" %}
**Note**

The account you are using to connect to the child company’s Intune tenant needs to have the **Global Administrator** role in the child company’s Entra ID to approve the PMPC Cloud enterprise app.

We require these permissions to connect to the child company’s Intune tenant.

See [Permissions required for the Intune Apps](../../../technical-references/cloud-permissions-reference/permissions-required-for-intune-apps.md) for more details.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (2782).png" alt="Clicking &#x27;Accept&#x27; on the &#x27;Permissions requested&#x27; page" width="512"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

You can click the down arrow beside each permission to get more information.
{% endhint %}

8. Verify Intune has **Connected** successfully.

<figure><img src="../../../../.gitbook/assets/image (619).png" alt="Intune connected successfully" width="252"><figcaption></figcaption></figure>

9. On the **Create New Customer** page, enter the name of the customer to be managed in the **Customer Name** field.

{% hint style="info" %}
**Note**

We support the characters **À-ÿ** (which includes characters from the Latin-1 Supplement Unicode block) for customer names.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (620).png" alt="Enter the name of the customer in the &#x27;Customer Name&#x27; field" width="201"><figcaption></figcaption></figure>

10. Click **Terms and Conditions**.

<figure><img src="../../../../.gitbook/assets/image (621).png" alt="Clicking &#x27;Terms and Conditions&#x27;" width="200"><figcaption></figcaption></figure>

11. Review the Terms and Conditions, and once you are happy, click the **X** in the top right-hand corner to return to the **Create New Customer** screen.

<figure><img src="../../../../.gitbook/assets/image (3009).png" alt="Reviewing the Terms and Conditions" width="563"><figcaption></figcaption></figure>

12. Check the **Accept all Terms and conditions** checkbox, then click **Create**.

<figure><img src="../../../../.gitbook/assets/image (622).png" alt="Accepting the Terms and conditions then clicking &#x27;Create&#x27;"><figcaption></figcaption></figure>

The portal refreshes, showing the newly added customer and the **Success - Child Customer <**_**customer\_name**_**> created** notification.

<figure><img src="../../../../.gitbook/assets/image (623).png" alt="The portal refreshes, showing the newly added customer and the Success - Child Customer <customer_name> created notification." width="563"><figcaption></figcaption></figure>

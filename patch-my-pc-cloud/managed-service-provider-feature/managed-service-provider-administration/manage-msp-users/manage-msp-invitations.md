# Manage MSP Invitations

_Applies to: Patch My PC Cloud_

By using the invite functionality of the _Managed Service Provider_ feature of Patch My PC (PMPC) Cloud, the customer of the child company can allow the MSP to manage their PMPC Cloud company without granting them global admin rights.

{% hint style="info" %}
**Note**&#x20;

Please note the following:

* **Users not using PMPC Cloud -** If the users you plan to invite to your MSP company are not already using PMPC Cloud, you should follow the [Add a Company to Manage (Cloud MSP)](../manage-msp-companies/add-a-company-to-manage-cloud-msp.md) process.\
  \
  Any users created in the MSP parent company will automatically be assigned the same role in any child company, as child companies inherit user roles from the parent company. \
  \
  For example, if a user is created in the parent company and assigned the **Full Admin with Access Management** role, they will have the same role permissions in any child companies.&#x20;
*   **MSP Companies in different regions -** We currently do not support an MSP Parent Company being in a different region than the Child customer they want to invite. <br>

    A workaround for now is for the Child customer to delete their PMPC Cloud Portal Company and for the MSP to recreate it in the same region as their Parent Company.
{% endhint %}

Once a user has been invited, they will have to:

* [Accept the invitation](manage-msp-invitations.md#accept-the-invitation-to-an-msp-parent-company)
* [Decline the invitation](manage-msp-invitations.md#decline-the-invitation-to-an-msp-parent-company)

## Inviting a User to an MSP Company&#x20;

To invite a user to an existing MSP Company:&#x20;

1. Sign in to the parent PMPC Cloud MSP Company.
2. Navigate to **MSP Customers**

<figure><img src="../../../../.gitbook/assets/image (582).png" alt="Navigating to &#x27;MSP Customers&#x27;" width="563"><figcaption></figcaption></figure>

3. Click **Invite Customer**

<figure><img src="../../../../.gitbook/assets/image (583).png" alt="Clicking &#x27;Invite Customer&#x27;" width="563"><figcaption></figcaption></figure>

4. In the **Invite Customer** dialog box, enter the email address of the user within the child company you want to invite and click **Send**

<figure><img src="../../../../.gitbook/assets/image (584).png" alt="Entering the email address of the user within the child company you want to invite in the &#x27;Invite Customer&#x27; dialog box and clicking &#x27;Send&#x27;" width="266"><figcaption></figcaption></figure>

The pending invitation appears under the **Invitations** tab of the **MSP Customers** screen, along with the **Success** message that the invitation has been sent.

<figure><img src="../../../../.gitbook/assets/image (585).png" alt="Invitation appearing under the ‘Invitations’ tab and the ‘Success’ message that the invitation has been sent." width="563"><figcaption></figcaption></figure>

An event stating the invitation has been sent to the user (including their email address) is also written to the **Events** node.

{% hint style="success" %}
**Tip**

You can also copy an invitation’s link and send it to the user for them to click or resend the invite to them (only after 6 hours).
{% endhint %}

5. The user then needs to decide whether to accept or decline the invitation by clicking the **Review Invitation** button in the email, and then, after signing in to their PMPC Cloud company, either:
   1. [Accept the invitation](manage-msp-invitations.md#accept-the-invitation-to-an-msp-parent-company)
   2. [Decline the invitation](manage-msp-invitations.md#decline-the-invitation-to-an-msp-parent-company)

## Accept the Invitation to an MSP Parent Company

To accept the invitation to allow the MSP Parent company to manage your PMPC Company:

1. Click the **Terms and Conditions** link on the **Company Access Request** screen.

<figure><img src="../../../../.gitbook/assets/image (586).png" alt="Clicking the ‘Conditions’ link" width="563"><figcaption></figcaption></figure>

2. Review the Terms and Conditions, then click the **X** to close them.

<figure><img src="../../../../.gitbook/assets/image (587).png" alt="Reviewing the terms and conditions" width="563"><figcaption></figcaption></figure>

3. On the **Company Access Request** screen:
   1. Check the **Accept all Terms and Conditions** checkbox
   2. Select the relevant company you want to allow the MSP parent company to manage
   3. Click **Accept Invitation**

<figure><img src="../../../../.gitbook/assets/image (588).png" alt="Accepting the invitation" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If a company is greyed out on the **Company Access Request** screen, it’s either because it’s already being managed by an MSP or the user accepting the invitation does not have **Full Admin** rights in the company to be able to accept the invitation.

If no companies are available to select on the **Company Access Request** screen, the user has the option to click **Create new and Accept**, which will allow them to create a brand new company that can be managed by the MSP parent company.

![‘Create new and Accept’ option](<../../../../.gitbook/assets/image (589).png>)
{% endhint %}

The user is signed into their PMPC Cloud company, which now shows **Managed By&#x20;**_**\<msp\_parent\_company\_name>**_ in the header.

<figure><img src="../../../../.gitbook/assets/image (590).png" alt="PMPC Cloud portal showing ‘Managed By <msp_parent_company_name>’ in the header." width="563"><figcaption></figcaption></figure>

In the MSP Parent company, the company of the user who accepted the invitation is shown under the **Customers** tab of the **MSP Customers** screen.

<figure><img src="../../../../.gitbook/assets/image (591).png" alt="Company of the user who accepted the invitation is shown under the ‘Customers’ tab" width="563"><figcaption></figcaption></figure>

An event indicating that the user has accepted the invitation (including their email address) is also written to the **Events** node.

## Decline the Invitation to an MSP Parent Company

To decline the invitation to allow the MSP Parent company to manage your PMPC Cloud company, you can either ignore the invitation (which will expire 15 days after it was sent) or click **Decline** on the **Company Access Request** screen.

<figure><img src="../../../../.gitbook/assets/image (3683).png" alt="Clicking ‘Decline’ on the ‘Company Access Request’ screen to decline an invitation" width="563"><figcaption></figcaption></figure>

The **Select the Company You Want to Sign In To** screen is displayed.

<figure><img src="../../../../.gitbook/assets/image (3684).png" alt="‘Select the Company You Want to Sign In To’ screen is displayed." width="563"><figcaption></figcaption></figure>

In the MSP Parent company, the **Status** of the invitation changes to **Declined**

<figure><img src="../../../../.gitbook/assets/image (3685).png" alt="‘Status’ of the invitation changing to ‘Declined’ in the MSP Parent company" width="563"><figcaption></figcaption></figure>

An event indicating that the user has declined the invitation (including their email address) is also written to the **Events** node.

At this point, your only option is to either follow up with the relevant user to check why they declined the invitation or click the red trash can to delete the invitation.

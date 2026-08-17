# Add a User in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Users can be added to the PMPC Cloud portal by:

* [Invitation from an Administrator](add-user.md#invitation-from-an-administrator)
* [Users requesting access](add-user.md#users-requesting-access)

{% hint style="info" %}
**Note**

Users can also access the portal if they are members of one or more Entra ID Security Groups that have been added to the portal.

If a user has been added directly to the portal using the processes detailed in this article and they are also a member of an Entra ID Security Group that is granted access to the same PMPC Cloud company, they will appear both under the **Users** tab and a member of the relevant Entra ID Security Group(s) when following the [View an Entra ID Group's Membership](using-entra-id-security-groups/view-membership-entra-id-security-group.md) process.
{% endhint %}

### Invitation from an Administrator

To invite a new user to the PMPC Cloud portal:

1. Navigate to **Settings | Users**.
2.  Click **Invite User** in the header.<br>

    <figure><img src="../../../../.gitbook/assets/image-(722).png" alt=""><figcaption></figcaption></figure>
3.  On the **Invite User** screen, enter the user’s details.<br>

    <figure><img src="../../../../.gitbook/assets/image (2821).png" alt="Complete the details of the user you are inviting" width="262"><figcaption></figcaption></figure>

{% hint style="warning" %}
**Important**

The email address you enter must already have an Entra ID account associated with it. If it does not, that user cannot sign into PMPC Cloud.
{% endhint %}

4. Under the **Role** section, click the relevant option for the role you want to assign in the PMPC Cloud portal.

{% hint style="info" %}
**Note**

See [User Roles](user-roles-reference.md) for details of the available roles and which actions they can perform.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (2822).png" alt="Choosing which role to assign this user" width="262"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

Use the tooltips beside each role to gain a quick overview of the role and it's capabilities.
{% endhint %}

5.  Click **Invite**.\
    <br>

    <figure><img src="../../../../.gitbook/assets/image (2823).png" alt="Clicking &#x22;Invite&#x22; to send the invitation" width="268"><figcaption></figcaption></figure>

The **Success - Invitation sent** notification is displayed.

<figure><img src="../../../../.gitbook/assets/image (1427).png" alt="&#x22;Success - Invitation sent&#x22; notification"><figcaption></figcaption></figure>

The user will receive an email from the [noreply@patchmypc.com](mailto:noreply@patchmypc.com) mailbox with the subject **You are invited to&#x20;**_**\<company\_name>**_.

{% hint style="info" %}
**Note:**

See [Example Invitation email](../../../technical-references/cloud-email-reference/example-cloud-invitation-email.md) to see an example of the email.
{% endhint %}

The invitation and its details are shown on the **Invitations** tab, which includes any previously created outstanding invitations that are still valid.

<figure><img src="../../../../.gitbook/assets/image (1429).png" alt="“Invitations” tab showing valid, outstanding user invitations"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Invitations are valid for 60 days from the date of issue. If the user does not accept the invitation within this time period, it will expire, and the user will need to be re-invited.

Users should follow the [Accepting an Invitation](invitations/accept-invitation.md) process to onboard to the PMPC Cloud portal.
{% endhint %}

### Users requesting access

When a user from the same company who has not been set up on your company's PMPC Cloud portal tries to sign in, they will see the **Select the Company You Want to Sign In To** screen.

<figure><img src="../../../../.gitbook/assets/image (2080).png" alt="“Select the Company You Want to Sign In To” screen"><figcaption></figcaption></figure>

To join your company, they should click **Request Access** beside your company.

<figure><img src="../../../../.gitbook/assets/image (2081).png" alt="Users should click “Request Access” beside your company to join it"><figcaption></figcaption></figure>

The **Request Access to join&#x20;**_**\<company\_name>**_ popup appears.

<figure><img src="../../../../.gitbook/assets/image-(616).png" alt="&#x22;Request Access to join <company_name>&#x22; popup"><figcaption></figcaption></figure>

The user should enter an optional **Reason for Request** then click **Submit**.

The **Request Access** text changes to **Renotify** and the **Success - Access request sent** notification is shown.

<figure><img src="../../../../.gitbook/assets/image-(617).png" alt="The “Success – Request sent” notification is displayed"><figcaption></figcaption></figure>

Any users with the **Full Admin** role in your PMPC Cloud portal will receive an email containing the user’s details and which company they have requested access to. The email is sent from the [noreply@patchmypc.com](mailto:noreply@patchmypc.com) mailbox with the subject **Access Request&#x20;**_**\<your\_company\_name>**_.

{% hint style="info" %}
**Note**

See [Example Access Request email](../../../technical-references/cloud-email-reference/example-cloud-access-request-email.md) to see an example of the email.
{% endhint %}

{% hint style="warning" %}
**Important**

The user cannot access the PMPC Cloud portal until their request is approved. See [Managing Access Requests](access-requests/) for more details.
{% endhint %}

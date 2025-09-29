# Add a Cloud User

_Applies to: Patch My PC Cloud_

Users can be added to the PMPC Cloud portal by:

* [Invitation from an Administrator](add-a-cloud-user.md#invitation-from-an-administrator)
* [Users requesting access](add-a-cloud-user.md#users-requesting-access)

<blockquote class="wp-block-quote is-note">
<p>Users can also access the portal if they are members of one or more Entra ID Security Groups that have been added to the portal.</p>
<p>If a user has been added directly to the portal using the processes detailed in this article and they are also a member of an Entra ID Security Group that is granted access to the same PMPC Cloud company, they will appear both under the **Users** tab and a member of the relevant Entra ID Security Group(s) when following the [View an Entra ID Group's Membership](using-entra-id-security-groups-in-cloud/view-an-entra-id-groups-membership-in-cloud.md) process.</p>
</blockquote>

### Invitation from an Administrator

To invite a new user to the PMPC Cloud portal:

1. Navigate to **Settings | Users**.
2.  Click **Invite User** in the header.\


    ![](/_images/image-(722).png)
3.  On the **Invite User** screen, enter the user’s details.\


    ![Complete the details of the user you are inviting](/_images/image-(2119).png "Complete the details of the user you are inviting")

<blockquote class="wp-block-quote is-important">
<p>The email address you enter must already have an Entra ID account associated with it. If it does not, that user cannot sign into PMPC Cloud.</p>
</blockquote>

4. Under the **Role** section, click the relevant option for the role you want to assign in the PMPC Cloud portal.

<blockquote class="wp-block-quote is-note">
<p>See [User Roles](cloud-user-roles-reference.md) for details of the available roles and which actions they can perform.</p>
</blockquote>

![Choosing which role to assign this user](/_images/image-(2120).png "Choosing which role to assign this user")

<blockquote class="wp-block-quote is-tip">
<p>Use the tooltips beside each role to gain a quick overview of the role and it's capabilities.</p>
</blockquote>

5.  Click **Invite**.\
    \


    ![Clicking "Invite" to send the invitation](/_images/image-(2122).png "Clicking &#x22;Invite&#x22; to send the invitation")

The **Success - Invitation sent** notification is displayed.

!["Success - Invitation sent" notification](/_images/image-(725).png "&#x22;Success - Invitation sent&#x22; notification")

The user will receive an email from the [noreply@patchmypc.com](mailto:noreply@patchmypc.com) mailbox with the subject **You are invited to&#x20;**_**\<company\_name>**_.

<blockquote class="wp-block-quote is-note">
<p>See [Example Invitation email](../../cloud-reference/cloud-email-reference/example-cloud-invitation-email.md) to see an example of the email.</p>
</blockquote>

The invitation and its details are shown on the **Invitations** tab, which includes any previously created outstanding invitations that are still valid.

!["Invitations" tab showing valid, outstanding user invitations](/_images/image-(728).png "“Invitations” tab showing valid, outstanding user invitations")

<blockquote class="wp-block-quote is-note">
<p>Invitations are valid for 60 days from the date of issue. If the user does not accept the invitation within this time period, it will expire, and the user will need to be re-invited.</p>
<p>Users should follow the [Accepting an Invitation](manage-cloud-invitations/accept-a-cloud-invitation.md) process to onboard to the PMPC Cloud portal.</p>
</blockquote>

### Users requesting access

When a user from the same company who has not been set up on your company's PMPC Cloud portal tries to sign in, they will see the **Select the Company You Want to Sign In To** screen.

!["Select the Company You Want to Sign In To" screen](/_images/image-(1378).png "“Select the Company You Want to Sign In To” screen")

To join your company, they should click **Request Access** beside your company.

![Users should click "Request Access" beside your company to join it](/_images/image-(1379).png "Users should click “Request Access” beside your company to join it")

The **Request Access to join&#x20;**_**\<company\_name>**_ popup appears.

![](/_images/image-(616).png)

The user should enter an optional **Reason for Request** then click **Submit**.&#x20;

The **Request Access** text changes to **Renotify** and the **Success - Access request sent** notification is shown.

![The "Success – Request sent" notification is displayed](/_images/image-(617).png "The “Success – Request sent” notification is displayed")

Any users with the **Full Admin** role in your PMPC Cloud portal will receive an email containing the user’s details and which company they have requested access to. The email is sent from the [noreply@patchmypc.com](mailto:noreply@patchmypc.com) mailbox with the subject **Access Request&#x20;**_**\<your\_company\_name>**_.

<blockquote class="wp-block-quote is-note">
<p>See [Example Access Request email](../../cloud-reference/cloud-email-reference/example-cloud-access-request-email.md) to see an example of the email.</p>
</blockquote>

<blockquote class="wp-block-quote is-important">
<p>The user cannot access the PMPC Cloud portal until their request is approved. See [Managing Access Requests](manage-cloud-access-requests/) for more details.</p>
</blockquote>
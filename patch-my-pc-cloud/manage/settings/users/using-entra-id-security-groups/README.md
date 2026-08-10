# Using Entra ID Security Groups in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Patch My PC (PMPC) Cloud supports the use of Entra ID Security Groups to control who has access to your PMPC Cloud company and which actions they can perform.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Access through nested Entra ID groups is currently not supported.</p>
</blockquote>

Once the Entra ID Security Groups feature has been enabled for your PMPC Cloud Company and provided you have successfully connected it to your Intune tenant, you will see the **Entra ID Groups** tab under the **Users** node.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>For access via Entra ID groups to work, you need to have [enabled the relevant domains](../../company-settings/multiple-domain-support/enable-domain.md) in your PMPC Cloud Company.</p>
</blockquote>

!["Entra ID Groups" tab on the "Users" node](/_images/image-(2957).png "“Entra ID Groups” tab on the “Users” node")

Using Entra ID Security Groups feature of PMPC Cloud allows you to:

* [Add an Entra ID Security Group](add-entra-id-security-group.md)
* [View an Entra ID Security Group's Membership](view-membership-entra-id-security-group.md)
* [Modify an Entra ID Security Group](modify-entra-id-security-group.md)
* [Remove an Entra ID Security Group](remove-entra-id-security-group.md)

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The following actions cannot be performed with PMPC Cloud and need to be performed from within Entra ID:</p>
<p>* Modifying the membership of a group (add or remove).</p>
<p>* Moving users between groups.</p>
<p>* Deleting groups from Entra ID.</p>
<p>Also, when you first set up a PMPC Cloud company, the user creating the company is automatically assigned the **Full Admin with Access Management** role. To avoid access issues (such as this user leaving your company and not passing on their credentials/setting up another user with this role), we recommend you either:</p>
<p>* [Add a second user](../add-user.md) and assign them this role.</p>
<p>* [Add an Entra ID Security Group](add-entra-id-security-group.md) to the portal and assign it the **Full Admin with Access Management** role.</p>
<p>Once you’ve done this, we recommend you use Entra ID Security Groups to manage any additional users who need to have access to your PMPC Cloud company.</p>
</blockquote>
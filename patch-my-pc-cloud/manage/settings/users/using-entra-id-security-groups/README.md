# Using Entra ID Security Groups in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Patch My PC (PMPC) Cloud supports the use of Entra ID Security Groups to control who has access to your PMPC Cloud company and which actions they can perform.

{% hint style="danger" %}
**Important**

Access through nested Entra ID groups is currently not supported.
{% endhint %}

Once the Entra ID Security Groups feature has been enabled for your PMPC Cloud Company and provided you have successfully connected it to your Intune tenant, you will see the **Entra ID Groups** tab under the **Users** node.

{% hint style="danger" %}
**Important**

For access via Entra ID groups to work, you need to have [enabled the relevant domains](../../company-settings/multiple-domain-support/enable-domain.md) in your PMPC Cloud Company.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (2957).png" alt="“Entra ID Groups” tab on the “Users” node"><figcaption></figcaption></figure>

Using Entra ID Security Groups feature of PMPC Cloud allows you to:

* [Add an Entra ID Security Group](add-entra-id-security-group.md)
* [View an Entra ID Security Group's Membership](view-membership-entra-id-security-group.md)
* [Modify an Entra ID Security Group](modify-entra-id-security-group.md)
* [Remove an Entra ID Security Group](remove-entra-id-security-group.md)

{% hint style="info" %}
**Note**

The following actions cannot be performed with PMPC Cloud and need to be performed from within Entra ID:

* Modifying the membership of a group (add or remove).
* Moving users between groups.
* Deleting groups from Entra ID.

Also, when you first set up a PMPC Cloud company, the user creating the company is automatically assigned the **Full Admin with Access Management** role. To avoid access issues (such as this user leaving your company and not passing on their credentials/setting up another user with this role), we recommend you either:

* [Add a second user](../add-user.md) and assign them this role.
* [Add an Entra ID Security Group](add-entra-id-security-group.md) to the portal and assign it the **Full Admin with Access Management** role.

Once you’ve done this, we recommend you use Entra ID Security Groups to manage any additional users who need to have access to your PMPC Cloud company.
{% endhint %}

# Why is the “Add” button unavailable in the Cloud portal?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to add a new Entra ID Security Group to the Patch My PC (PMPC) Cloud portal, but the **Add** button on the Users page is greyed out.

<figure><img src="../../../.gitbook/assets/image (580).png" alt="&#x27;Add&#x27; button greyed out" width="376"><figcaption></figcaption></figure>

### CAUSE

This could be caused by:

* Your PMPC Cloud company is not connected to Intune.
* You have already added ten Entra ID Security Groups to your PMPC Cloud company, which is the maximum we currently support.

### RESOLUTION

Possible ways to resolve this issue are:

* Follow the [Manage Intune tenants](/broken/pages/RoXhXa1jcXhIcPcKJk05) process to check that your PMPC Cloud company is connected to Intune.
* Remove an existing group and replace it with the group you are trying to add.
* Add the users of the new group you are trying to add to another Entra ID Security Group that has already been added to the portal.
* Add the group you are trying to add to another Entra ID Security Group in Entra ID with the same permissions.
* Add the members of the new/existing group(s) as direct users into the portal directly by following the [Add a User](../../manage/settings/users/add-user.md) process.

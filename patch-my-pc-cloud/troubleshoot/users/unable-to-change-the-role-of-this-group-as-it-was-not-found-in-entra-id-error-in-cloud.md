# “Unable to change the role of this group as it was not found in Entra ID” error in Cloud

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to change the role assigned to an Entra ID Security Group in the Patch My PC (PMPC) Cloud portal, but I get the following error:

**Error - Unable to change the role of this group as it was not found in Entra ID**

!["Unable to change the role of this group as it was not found in Entra ID" error](../../../.gitbook/assets/image-\(2994\).png)

### CAUSE

This error is caused if the Entra ID Security Group has been deleted in Entra ID. If you refresh the portal, you will see the **GROUP WAS DELETED ON AZURE** message and you can only delete the group.

!["Group role was deleted on Azure" error](../../../.gitbook/assets/image-\(1050\).png)

### RESOLUTION

To resolve this issue:

1. Delete the existing group from the portal. Just recreating the group in Entra ID won’t work, as the group will have a different Entra ID than the existing one in the portal.
2. Recreate the group in Entra ID with the relevant members.
3. Add the group to the portal.

# "Unable to disconnect this customer as they do not have a user with the Full Admin..." Cloud error

_Applies to: Patch My PC Cloud_

### SYMPTOMS

Why, when I try to disconnect a child company from its parent Managed Service Provider (MSP) Patch My PC (PMPC) Cloud company, do I see the following error:

**Unable to disconnect this customer as they do not have a user with the Full Admin with Access Management role.**

### CAUSE

This message is telling you that in the child company you are trying to disconnect from, there are no users assigned the **Full Admin with Access Management** user role. If we allowed you to proceed with the disconnection, no one would be able to access and administer the child company.

### RESOLUTION

To resolve this issue, ensure at least one user/group is assigned the **Full Admin with Access Management** user role at the child company. Once this exists, you will be able to disconnect the child company.

# Why is the “Add Group” button unavailable on the “Available Groups” page of the Cloud portal?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to add a new Entra ID Security Group to the Patch My PC (PMPC) Cloud portal, but after clicking the **Add Group** button on the **Users** page, the **Add Group** button is greyed out on the **Available Groups** page.

!["Add Group" button unavailable](/_images/image-(1048).png)

### CAUSE

This can occur if:

* You have not selected the checkbox beside at least one group.
* If the number of groups you have selected would take you over the current limit of being allowed to add a total of ten Entra ID Security Groups to your PMPC Cloud company.

### RESOLUTION

To resolve this issue, ensure you:

* Select at least one group.
* Haven’t selected a total of groups that would take you over the current ten-group limit. You may need to rethink how you structure your group membership in Entra ID.
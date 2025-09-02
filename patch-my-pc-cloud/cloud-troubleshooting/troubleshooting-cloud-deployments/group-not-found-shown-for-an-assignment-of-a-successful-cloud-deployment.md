# “Group not found” shown for an Assignment of a successful Cloud deployment

_Applies to: Intune Apps for Cloud_

### SYMPTOMS

I’ve successfully deployed an app using Intune Apps for Cloud (Intune Apps). However, when I look at its properties (by clicking on the deployment, pressing **More Info**, and expanding the **Assignment Type**), why does it show **(Group not found)** beside the assignment?

![](/_images/image-(366 "").png "")

If I edit the deployment and click **Assignments**, I also see the **Group not found. Please remove the assignment** message.

![](/_images/image-(365 "").png "")

### CAUSE

This is because someone has deleted the group used for the assignment from Entra.

### RESOLUTION

To resolve this issue:

1. Recreate and reconfigure the relevant group in Entra.
2. Edit the deployment in the portal.
3. Delete the relevant assignment.
4. Re-add the assignment by browsing to the recreated Entra group.
5. Complete the deployment.

{% hint style="info" %}
**Note**

Even though the group has been recreated in Entra with the same name, it will have a different Object Id so the original assignment has to be deleted and recreated to pick up the new group with the new Object Id.

See the [Edit a Deployment](../../cloud-deployments/manage-cloud-deployments/edit-a-cloud-deployment.md) process for more details.
{% endhint %}

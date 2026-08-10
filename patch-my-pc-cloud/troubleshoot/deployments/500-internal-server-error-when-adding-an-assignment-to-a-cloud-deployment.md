# “500 Internal Server Error” when adding an assignment to a Cloud deployment

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to create an assignment in the Patch My PC (PMPC) Cloud portal that previously worked.

Now, when I try to add an assignment, I get a **500 Internal Server Error**.

!["500 Internal Server Error" when trying to add an assignment](/_images/image-(1466).png "“500 Internal Server Error” when trying to add an assignment")

### CAUSE

The most probable cause of this is either someone has deleted the [Patch My PC Cloud Enterprise App](https://docs.patchmypc.com/patch-my-pc-cloud/troubleshooting/what-happens-if-the-patch-my-pc-cloud-enterprise-app-is-deleted) or a Global Admin has revoked the [Permissions required for Intune Apps](https://docs.patchmypc.com/patch-my-pc-cloud/intune-apps-public-preview/reference/permissions-required-for-intune-apps) from within the Intune admin center.

### RESOLUTION

To resolve this issue, follow the [Reconnecting an Intune tenant](https://docs.patchmypc.com/patch-my-pc-cloud/administration/managing-your-environments/managing-intune-tenants#reconnecting-an-intune-tenant) process, which will prompt you to reconfirm you want to grant the [Permissions required for Intune Apps](https://docs.patchmypc.com/patch-my-pc-cloud/intune-apps-public-preview/reference/permissions-required-for-intune-apps).
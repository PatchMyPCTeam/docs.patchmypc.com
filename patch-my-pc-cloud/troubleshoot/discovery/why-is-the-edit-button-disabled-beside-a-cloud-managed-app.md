# Why is the “Edit” button disabled beside a Cloud Managed App?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I have signed into the Patch My PC (PMPC) Cloud portal and navigated to the **Discovery** node, followed by the **Managed** tab.

I see the list of my managed apps, but why is the **Edit** button beside my app greyed out?

### CAUSE

This can occur for several reasons, including:

* The **Status** of the app is not showing as **Success** (it is in a **In Progress**, **Failed** or **Retrying** state).
* The signed in user does not have permission to edit deployments.
* Your PMPC Cloud portal license has expired.
* The deployment was made using our on-premises Publisher.

### RESOLUTION

To resolve this issue:

1. Check the **Status** of the relevant deployment. If it is showing as **Failed**, follow the [Troubleshooting an Intune Apps Deployment](../deployments/troubleshooting-an-intune-apps-deployment.md) process.
2. Verify the user has not been assigned the **Custom App Admin** user role, as this role cannot edit deployments.
3. Follow the [Managing your License](/broken/pages/8qjfvVWkH0JTJRXsuS6m) process to verify your license is still valid.

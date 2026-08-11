# Why do I see the "Missing Intune permissions" banner in Patch My PC Cloud?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

Why does the **Missing Intune permissions detected. Reconnect Intune to restore full functionality** banner appear in the Patch My PC (PMPC) Cloud Portal?

!['Missing Intune permissions detected. Reconnect Intune to restore full functionality' banner](/_images/image-(4511).png)

### CAUSE

Every hour, PMPC Cloud checks that the [Permissions required for Intune Apps](../../technical-references/cloud-permissions-reference/permissions-required-for-intune-apps.md) are present.

If one or more of these permissions are missing, you will see the banner shown above at the top of the Cloud Portal.

### RESOLUTION

To resolve this issue, click **Reconnect** to [reconnect your Company](../../manage/settings/connections/reconnect-connection.md) to your Intune tenant, which will grant the required permissions in your Intune tenant so that your PMPC Cloud Company functions correctly.
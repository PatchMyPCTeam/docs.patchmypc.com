# Why do I see a Yellow triangle beside my Intune Connection in Patch My PC Cloud?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

Why do I see a yellow triangle beside the Intune connection for my Patch My PC (PMPC) Cloud Company in the **Settings | Connections** page in the Cloud Portal?

![Yellow triangle beside the Intune connection for my Patch My PC (PMPC) Cloud Company in the Cloud Portal](/_images/image-(4513).png "Yellow triangle beside the Intune connection for my Patch My PC (PMPC) Cloud Company in the Cloud Portal")

### CAUSE

This is because one or more of the [Permissions required for Intune Apps](../../technical-references/cloud-permissions-reference/permissions-required-for-intune-apps.md) are missing.

If you hover your mouse over the triangle as shown, the list of required permissions and their status is shown.

### RESOLUTION

To resolve this issue, follow the [reconnect your Company](../../manage/settings/connections/reconnect-connection.md) to your Intune tenant, which will grant the required permissions in your Intune tenant so that your PMPC Cloud Company functions correctly.
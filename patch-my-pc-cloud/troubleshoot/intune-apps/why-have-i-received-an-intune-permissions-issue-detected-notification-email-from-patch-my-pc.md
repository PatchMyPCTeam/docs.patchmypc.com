# Why have I received an "Intune Permissions Issue Detected" notification email from Patch My PC?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I have received an email notification from Patch My PC (PMPC) with the subject **Intune Permissions Issue Detected**

<figure><img src="../../../.gitbook/assets/image (4509).png" alt="&#x27;Intune Permissions Issue Detected&#x27; email" width="488"><figcaption></figcaption></figure>

### CAUSE

If you have email notifications configured for PMPC Cloud and one of the [Permissions required for Intune Apps](../../technical-references/cloud-permissions-reference/permissions-required-for-intune-apps.md) has been revoked, every hour that the issue persists, you will receive this notification warning you we have detected an issue.

### RESOLUTION

Click **Review Connection** to see the **Connections** page, which will let you review your connection and, if needed, [reconnect your Company](../../manage/settings/connections/reconnect-connection.md) to your Intune tenant to grant the relevant permissions.

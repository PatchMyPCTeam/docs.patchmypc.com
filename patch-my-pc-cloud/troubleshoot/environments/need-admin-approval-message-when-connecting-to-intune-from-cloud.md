# “Need admin approval” message when connecting to Intune from Cloud

_Applies to: Intune Apps for Cloud_

### SYMPTOMS

I am trying to onboard to Intune Apps for Cloud (Intune Apps). I’ve signed in and clicked **Connect** to connect my Intune tenant, expecting to see the **Permissions requested** dialog box, but instead, I get the **Need admin approval** dialog box stating:

**Patch My PC LLC needs permission to access resources in your organization that only an admin can grant. Please ask an admin to grant permission to this app before you can use it.**\
<br>

!["Need admin approval" dialog box](../../../.gitbook/assets/image-\(1608\).png)

### CAUSE

This problem occurs because, as the message states, your Entra ID account is not a Global Administrator. As a result, you cannot consent to the PMPC Cloud application on your behalf.

### RESOLUTION

To resolve this issue, ensure you are completing this process using a **Global Administrator** account to create the enterprise app.

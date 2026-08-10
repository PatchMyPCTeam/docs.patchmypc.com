# “Need admin approval” message when onboarding to Cloud

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to onboard to Patch My PC (PMPC) Cloud. I’ve signed in, expecting to see the **Permissions requested** dialog box, but instead, I get the **Need admin approval** dialog box stating:

**Patch My PC LLC needs permission to access resources in your organization that only an admin can grant. Please ask an admin to grant permission to this app before you can use it.**\
<br>

<figure><img src="../../../.gitbook/assets/image (1608).png" alt="“Need admin approval” dialog box"><figcaption></figcaption></figure>

### CAUSE

This problem occurs because, as the message states, your Entra ID account is not a Global Administrator. As a result, you cannot consent to the PMPC Cloud application on your behalf.

### RESOLUTION

To resolve this issue, click **Sign in with that account** next to **Have an admin account?** and sign in with an admin account.

If you don't have a suitable admin account, contact the relevant person in your organization to obtain one or to perform the onboarding for you.

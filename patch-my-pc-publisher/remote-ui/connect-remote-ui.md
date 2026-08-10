# Connect to the Patch My PC Publisher Remote User Interface

_Applies to: Patch My PC Publisher V3.x_

{% hint style="danger" %}
**PRE-RELEASE DOCUMENTATION**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

Once you have [set up](setup.md) Patch My PC (PMPC) Publisher _Remote User Interface (UI)_, simply launch the Settings console.&#x20;

No username or password is required, as when the Settings console connects, Windows authenticates you to the server using your current sign-in (Kerberos, or NTLM as a fallback). The server then checks which Publisher groups you belong to and grants access accordingly.

If your account has not been added to any Publisher groups on the server, the connection still authenticates, but you will not be able to see or change much.

{% hint style="info" %}
**Note**

See [Access and Permissions](technical-references/access-permissions-reference.md) for more information about granting access, and [Show Granted Permissions Shield](../fundamentals/about-interface.md#show-granted-permissions-shield) to confirm which permissions you currently hold.
{% endhint %}

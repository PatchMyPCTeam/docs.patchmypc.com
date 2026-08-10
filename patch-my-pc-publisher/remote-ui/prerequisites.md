# Prerequisites for the Patch My PC Publisher Remote User Interface

_Applies to: Patch My PC Publisher V3.x_

{% hint style="danger" %}
**PRE-RELEASE DOCUMENTATION**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

To use the _Remote User Interface (UI)_ feature of Patch My PC (PMPC) Publisher and run the Settings console remotely against a Publisher server, you need:

* **Network access** from your workstation to the server on the Publisher's management port. The port is chosen by the administrator who enables remote access; ensure any firewall between you and the server allows it.
* **A Windows account that can reach the server.** As sign-in uses Kerberos or NTLM, your workstation must be able to authenticate to the server. Normally this means both are in the same Active Directory domain (or trusted domains).
* **Permission on the server.** Your account (or a domain group you belong to) must be added to the appropriate Publisher group on the server (see [Access and Permissions Reference](technical-references/access-permissions-reference.md) for more information).
* **A trusted server certificate**, for any connection that crosses the network (see [Using a Different Computer](technical-references/using-different-computer.md) for more information). In a domain, a certificate from your internal certificate authority is the easiest option.

# Troubleshoot Patch My PC Publisher Remote User Interface

_Applies to: Patch My PC Publisher V3.x_

{% hint style="danger" %}
**PRE-RELEASE DOCUMENTATION**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

This article contains troubleshooting information for common scenarios related to the Patch My PC (PMPC) Publisher _Remote User Interface (UI)_ feature:

* [Test Connection cannot reach the server](troubleshoot.md#test-connection-cannot-reach-the-server)
* [Test Connection reaches the server, but the certificate is rejected](troubleshoot.md#test-connection-reaches-the-server-but-the-certificate-is-rejected)
* [You can connect, but almost everything is read-only or hidden](troubleshoot.md#you-can-connect-but-almost-everything-is-read-only-or-hidden)
* [You can connect, but the console says it is read-only](troubleshoot.md#you-connect-but-the-console-says-it-is-read-only)

## Test Connection cannot reach the server

**Likely cause and fix:**

Incorrect hostname or port configuration, or the specified port is blocked on the firewall.

Confirm the values entered match those entered in [Enabling external access on the server](setup.md#enabling-external-access-on-the-server) and that the port is open on the firewall between you and the server.

## Test Connection reaches the server, but the certificate is rejected

**Likely cause and fix:**

The certificate name does not match the hostname you entered, or it is not trusted.

Connect using the exact FQDN in the certificate, and verify the requirements and configurations detailed in [Using a Different Computer](technical-references/using-different-computer.md).

## You can connect, but almost everything is read-only or hidden

**Likely cause and fix:**

Your account is not in the right Publisher groups on the server. See [Access and Permissions Reference](technical-references/access-permissions-reference.md) for more information.

## You can connect, but the console says it is read-only

**Likely cause and fix:**

Another administrator already holds the editing session. See [Multiple Administrators](technical-references/multiple-administrators.md) for more information.

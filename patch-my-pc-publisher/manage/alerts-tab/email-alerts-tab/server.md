---
hidden: true
---

# Server section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Server** section on the **Email Alerts** tab of Patch My PC (PMPC) Publisher allows you to configure the settings for the server that will be used by Publisher to send email notifications, based on the "Authentication" method selected.

<figure><img src="../../../../.gitbook/assets/image (1323).png" alt="&#x27;Server&#x27; section" width="563"><figcaption></figcaption></figure>

See the relevant section for the Authentication method you have chosen:

* [Anonymous](server.md#server-configuration-for-anonymous)
* [System account](server.md#server-configuration-for-system-account)
* [Specific user](server.md#server-configuration-for-specific-user)

{% hint style="info" %}
**Note**

When you choose the "OAuth2 (App Auth) authentication method", the **Server** section disappears as it is not relevant to this authentication method.
{% endhint %}

## **Server Configuration for Anonymous**

If you choose the "Anonymous authentication method", configure the settings in the **Server** section as follows:

<table><thead><tr><th width="101.77777099609375" valign="top">Field</th><th valign="top">Configuration</th></tr></thead><tbody><tr><td valign="top">Server</td><td valign="top">Enter the DNS name or IP address of the SMTP server that will relay email messages. This is typically an internal Microsoft Exchange server or an on-premises SMTP relay configured to allow anonymous connections.</td></tr><tr><td valign="top">Port</td><td valign="top">Specify the port used to connect to the SMTP server. Anonymous SMTP relays typically use port 25, though this depends on how the relay is configured.</td></tr><tr><td valign="top">Use TLS</td><td valign="top">Enables Transport Layer Security (TLS) for the SMTP connection. Enable this if your relay requires or supports encrypted connections.</td></tr></tbody></table>

## **Server Configuration for System account**

If you choose the "System account" authentication method", configure the settings in the **Server** section as follows:

<table><thead><tr><th width="101.77777099609375" valign="top">Field</th><th valign="top">Configuration</th></tr></thead><tbody><tr><td valign="top">Server</td><td valign="top">Enter the DNS name or IP address of the SMTP server that will relay email messages. This is typically an on-premises Exchange server or an internal SMTP relay configured to allow integrated Windows authentication.</td></tr><tr><td valign="top">Port</td><td valign="top">Specify the port used to connect to the SMTP server. The appropriate port depends on the relay configuration and support for integrated authentication.</td></tr><tr><td valign="top">Use TLS</td><td valign="top">Enables Transport Layer Security (TLS) for the SMTP connection. This encrypts the connection to the SMTP server but does not affect authentication. Enable this if your relay requires or supports encrypted connections.</td></tr></tbody></table>

## **Server Configuration for Specific user**

If you choose the "Specific user" authentication method", configure the settings in the **Server** section as follows:

<table><thead><tr><th width="101.77777099609375" valign="top">Field</th><th valign="top">Configuration</th></tr></thead><tbody><tr><td valign="top">Server</td><td valign="top">Enter the DNS name or IP address of the SMTP server that will relay email messages. This is typically an internal Microsoft Exchange server or an authenticated SMTP relay.</td></tr><tr><td valign="top">Port</td><td valign="top">Specify the port used to connect to the SMTP server. The appropriate port depends on how the relay is configured and typically supports authenticated SMTP connections.</td></tr><tr><td valign="top">Use TLS</td><td valign="top">Enables Transport Layer Security (TLS) for the SMTP connection. This encrypts the connection to the SMTP server and is required by most authenticated SMTP relays and cloud-based mail services.</td></tr></tbody></table>

















Use the OAuth2 (App Auth) option to send email using OAuth 2.0 instead of a mailbox username and password. OAuth2 authenticates using a Microsoft Entra ID app registration and is the recommended approach for modern cloud email services.

{% hint style="info" %}
**Note**

See [OAuth2 (App Auth) Configuration](authentication/configure-oauth2.md) for detailed guidance on how to configure OAuth 2.0 authentication for email notifications.
{% endhint %}

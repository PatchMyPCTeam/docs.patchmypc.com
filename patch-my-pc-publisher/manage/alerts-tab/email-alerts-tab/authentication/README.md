# Authentication section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Authentication** section on the **Email Alerts** tab of Patch My PC (PMPC) Publisher configures how Publisher signs in to the mail server to be able to send email alerts.

<figure><img src="../../../../../.gitbook/assets/image (1322).png" alt="&#x27;Authentication&#x27; section" width="563"><figcaption></figcaption></figure>

When choosing an authentication method, select the option that aligns with how your mail system accepts SMTP connections.

For internal or on-premises mail servers, [Specific user](./#specific-user) is commonly used when the relay supports authenticated SMTP connections.

For cloud-based email services such as Microsoft 365 (Exchange Online) and Google Workspace, [OAuth2 (App Auth)](./#oauth2-app-auth) is recommended, as modern cloud providers increasingly restrict or deprecate username and password–based SMTP authentication.

Ultimately, the appropriate option depends on the authentication methods supported by your SMTP server.

You can choose from the following authentication methods:

* [Anonymous](./#id-1.-anonymous)
* [System account](./#id-3.-system)
* [Specific user](./#specified-user)
* [OAuth2 (App Auth)](./#id-4.-oauth2-app-auth)

## **Anonymous**

Use the **Anonymous** option only if your SMTP relay explicitly allows unauthenticated sending. Most cloud providers, including Exchange Online, do not support anonymous SMTP. This option typically works only with on-premises SMTP relays configured to accept unauthenticated traffic from trusted internal IP addresses.

{% hint style="info" %}
**Note**

When you select **Anonymous**, the **Login** and **Password** fields do not appear, as no credentials are required for authentication. See "Server Configuration for Anonymous" for details on how you should configure the settings in the **Server** section.
{% endhint %}

## **System account**

Use the **System account** option to authenticate to the SMTP server using the Windows account under which the Publisher service is running.

Choose this option only if your SMTP relay supports integrated Windows authentication using NTLM or Kerberos. This is typically limited to on-premises Microsoft Exchange servers or internal SMTP relays within the same Active Directory domain.

By default, the Publisher service runs under the **local SYSTEM** account.

{% hint style="info" %}
**Note**

When you select **System account**, the **Login** and **Password** fields do not appear, as no credentials are required for authentication. See "Server Configuration for System account" for details on how you should configure the settings in the **Server** section.
{% endhint %}

## **Specific user**

Use the **Specific user** option when your SMTP server requires authentication with a dedicated username and password. This is the most common configuration and is recommended for most environments, including Exchange Online, Google Workspace, and authenticated SMTP relays.

{% hint style="danger" %}
**Important**

Microsoft Exchange Online has deprecated Basic SMTP authentication and does not support username/password–based SMTP authentication by default. For Exchange Online, OAuth2 (App Authentication) is recommended.

Some providers, such as Google Workspace, may still allow authenticated SMTP using a username and password, but this typically requires additional configuration and may be restricted by tenant security policies.
{% endhint %}

If you choose to use the **Specific user** option, configure the settings in the **Specified User** section as follows:

<table><thead><tr><th width="101.77777099609375" valign="top">Field</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">Login</td><td valign="top">Enter the username used to authenticate to the SMTP server. This is often a full email address but may vary depending on your mail provider or relay configuration.</td></tr><tr><td valign="top">Password</td><td valign="top">Enter the password associated with the specified SMTP account.</td></tr></tbody></table>

{% hint style="info" %}
**Note**

See "Server Configuration for Specific user" for details on how you should configure the settings in the **Server** section.
{% endhint %}

### OAuth2 (App Auth)

Use the **OAuth2 (App Auth)** option to send email using OAuth 2.0 instead of a mailbox username and password. OAuth2 authenticates using a Microsoft Entra ID app registration and is the recommended approach for modern cloud email services.

{% hint style="info" %}
**Note**

See [OAuth2 (App Auth) Configuration](configure-oauth2.md) for detailed guidance on how to configure OAuth 2.0 authentication for email notifications.
{% endhint %}


# Email Notification Configuration section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Email Notification Configuration** section of the **Email Alerts** tab in Patch My PC (PMPC) Publisher allows you to configure Publisher to send notifications when specific publishing events occur. These alerts provide timely visibility into publishing activity, including successes, warnings, and failures, without requiring administrators to actively monitor logs.

<figure><img src="../../../../../.gitbook/assets/image (735).png" alt="&#x27;Email Notification Configuration&#x27; section" width="563"><figcaption></figcaption></figure>

Before email alerts can be sent, email settings must be configured. This includes specifying the SMTP server and port or configuring OAuth application details, along with the required authentication settings, sender address, and recipient addresses.

{% hint style="info" %}
**Note**

At the end of a [publishing sync](../../../sync-schedule-tab/), the Publisher sends an email containing details about the sync event.
{% endhint %}

## Send email reports

When the **Send email reports** option is enabled, Publisher sends email alerts and reports based on the configured email settings. When disabled, no email notifications are sent, regardless of the configuration.

## Disable email for manual sync

When **Disable email for manual sync** is enabled, email notifications are sent only for scheduled syncs.

{% hint style="danger" %}
**Important**

Email notifications are not sent when a sync is initiated manually from the [Sync Schedule](../../../sync-schedule-tab/) tab.
{% endhint %}

## Provider

The **Provider** dropdown lets you select from a list of predefined providers (such as Gmail, Outlook, Yahoo, or Exchange Online) to automatically populate the relevant fields on this tab with recommended values for the selected service.

For example, selecting **Exchange Online** from the **Provider** dropdown sets the **Server** to **smtp.office365.com**, **port** to **587**, and enables **Use TLS**.

If **Custom SMTP Provider** is selected, all SMTP settings must be configured manually.

{% hint style="success" %}
**Tip**

You can modify any auto-populated values as required to meet the needs of your environment.
{% endhint %}

## Test Email

After configuring the required email notification settings, click **Test Email** to verify that the message is successfully sent and received by the configured recipient(s).

If the test email fails, the issue is most commonly related to the SMTP or authentication configuration.

{% hint style="info" %}
**Note**

See [Troubleshooting SMTP Email Report Sending When Using Patch My PC](https://patchmypc.com/troubleshooting-smtp-email-sending) for troubleshooting guidance.
{% endhint %}

## **Email Fields**

The following fields control the email message details and recipients.

### **Sender** (_required_)

Enter the email address you want the alerts to come _from_. e.g. `alerts@yourdomain.com`

### **Recipients (**_**required**_**)**

Enter the email address(es) that should _receive_ the alerts. You can enter multiple addresses separated by a semicolon. e.g. `alerts@yourdomain.com; security@yourdomain.com`

### **CC recipients (**_**optional**_**)**

Add any additional recipients if needed. You can enter multiple addresses separated by a semicolon. e.g. `alerts@yourdomain.com; security@yourdomain.com`

### Email subject (_required_)

The default subject of the email is `Report from Patch My PC Publishing Service`. You can change this if required.

### Additional text **(**_**optional**_**)**

Enter any additional text you want included at the top of the email report, such as notes or context for your recipients.

## **Email Authentication**

When choosing an authentication method, select the option that aligns with how your mail system accepts SMTP connections.

For internal or on-premises mail servers, [Specified user](./#specific-user) is commonly used when the relay supports authenticated SMTP connections.

For cloud-based email services such as Microsoft 365 (Exchange Online) and Google Workspace, [OAuth2 (App Auth)](./#oauth2-app-auth) is recommended, as modern cloud providers increasingly restrict or deprecate username and password–based SMTP authentication.

Ultimately, the appropriate option depends on the authentication methods supported by your SMTP server.

You can choose from the following authentication methods:

* [Anonymous](./#id-1.-anonymous)
* [System account](./#id-3.-system)
* [Specific user](./#specified-user)
* [OAuth2 (App Auth)](./#id-4.-oauth2-app-auth)

### **Anonymous**

Use the **Anonymous** option only if your SMTP relay explicitly allows unauthenticated sending. Most cloud providers, including Exchange Online, do not support anonymous SMTP. This option typically works only with on-premises SMTP relays configured to accept unauthenticated traffic from trusted internal IP addresses.

{% hint style="info" %}
**Note**

When **Anonymous** is selected, the **Login** and **Password** fields are disabled, as no credentials are required for authentication.
{% endhint %}

#### **Server Configuration for Anonymous**

If you choose to use the **Anonymous** option, configure the settings in the **Server Configuration** section as follows:

<table><thead><tr><th width="101.77777099609375" valign="top">Field</th><th valign="top">Configuration</th></tr></thead><tbody><tr><td valign="top">Server</td><td valign="top">Enter the DNS name or IP address of the SMTP server that will relay email messages. This is typically an internal Microsoft Exchange server or an on-premises SMTP relay configured to allow anonymous connections.</td></tr><tr><td valign="top">Port</td><td valign="top">Specify the port used to connect to the SMTP server. Anonymous SMTP relays typically use port 25, though this depends on how the relay is configured.</td></tr><tr><td valign="top">Use TLS</td><td valign="top">Enables Transport Layer Security (TLS) for the SMTP connection. Enable this if your relay requires or supports encrypted connections.</td></tr></tbody></table>

### **System account**

Use the **System account** option to authenticate to the SMTP server using the Windows account under which the Publisher service is running.

Choose this option only if your SMTP relay supports integrated Windows authentication using NTLM or Kerberos. This is typically limited to on-premises Microsoft Exchange servers or internal SMTP relays within the same Active Directory domain.

By default, the Publisher service runs under the **local SYSTEM** account.

{% hint style="info" %}
**Note**

When Anonymous is selected, the Login and Password fields are disabled, as no credentials are used for authentication.
{% endhint %}

#### **Server Configuration for System account**

If you choose to use the **System account** option, configure the settings in the **Server Configuration** section as follows:

<table><thead><tr><th width="101.77777099609375" valign="top">Field</th><th valign="top">Configuration</th></tr></thead><tbody><tr><td valign="top">Server</td><td valign="top">Enter the DNS name or IP address of the SMTP server that will relay email messages. This is typically an on-premises Exchange server or an internal SMTP relay configured to allow integrated Windows authentication.</td></tr><tr><td valign="top">Port</td><td valign="top">Specify the port used to connect to the SMTP server. The appropriate port depends on the relay configuration and support for integrated authentication.</td></tr><tr><td valign="top">Use TLS</td><td valign="top">Enables Transport Layer Security (TLS) for the SMTP connection. This encrypts the connection to the SMTP server but does not affect authentication. Enable this if your relay requires or supports encrypted connections.</td></tr></tbody></table>

### **Specific user**

Use the **Specific user** option when your SMTP server requires authentication with a dedicated username and password. This is the most common configuration and is recommended for most environments, including Exchange Online, Google Workspace, and authenticated SMTP relays.

{% hint style="danger" %}
**Important**

Microsoft Exchange Online has deprecated Basic SMTP authentication and does not support username/password–based SMTP authentication by default. For Exchange Online, OAuth2 (App Authentication) is recommended.

Some providers, such as Google Workspace, may still allow authenticated SMTP using a username and password, but this typically requires additional configuration and may be restricted by tenant security policies.
{% endhint %}

#### **Specified User Configuration**

If you choose to use the **Specific user** option, configure the settings in the **Specified User** section as follows:

<table><thead><tr><th width="101.77777099609375" valign="top">Field</th><th valign="top">Configuration</th></tr></thead><tbody><tr><td valign="top">Login</td><td valign="top">Enter the username used to authenticate to the SMTP server. This is often a full email address but may vary depending on your mail provider or relay configuration.</td></tr><tr><td valign="top">Password</td><td valign="top">Enter the password associated with the specified SMTP account.</td></tr></tbody></table>

#### **Server Configuration for Specific user**

If you choose to use the **Specific user** option, configure the settings in the **Server Configuration** section as follows:

<table><thead><tr><th width="101.77777099609375" valign="top">Field</th><th valign="top">Configuration</th></tr></thead><tbody><tr><td valign="top">Server</td><td valign="top">Enter the DNS name or IP address of the SMTP server that will relay email messages. This is typically an internal Microsoft Exchange server or an authenticated SMTP relay.</td></tr><tr><td valign="top">Port</td><td valign="top">Specify the port used to connect to the SMTP server. The appropriate port depends on how the relay is configured and typically supports authenticated SMTP connections.</td></tr><tr><td valign="top">Use TLS</td><td valign="top">Enables Transport Layer Security (TLS) for the SMTP connection. This encrypts the connection to the SMTP server and is required by most authenticated SMTP relays and cloud-based mail services.</td></tr></tbody></table>

### OAuth2 (App Auth)

Use the **OAuth2 (App Auth)** option to send email using OAuth 2.0 instead of a mailbox username and password. OAuth2 authenticates using a Microsoft Entra ID app registration and is the recommended approach for modern cloud email services.

{% hint style="info" %}
**Note**

See [OAuth2 (App Auth) Configuration](configure-oauth2.md) for detailed guidance on how to configure OAuth 2.0 authentication for email notifications.
{% endhint %}

## Save Email Notification Settings

Click **Apply** to save the changes. Once the Email Notification settings are saved, Publisher will automatically send an email at the end of each synchronization when any updates or applications have been published.

{% hint style="info" %}
**Note**

See [Example Email Alerts](../../../../technical-references/example-email-alerts.md) for examples of the alerts sent by Publisher.
{% endhint %}

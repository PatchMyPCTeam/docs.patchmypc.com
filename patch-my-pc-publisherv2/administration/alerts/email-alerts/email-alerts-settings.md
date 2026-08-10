# Email Alerts Settings

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Email Alerts** option allows the Publisher to be configured to send notifications when specific publishing events occur. These alerts provide timely visibility into publishing activity, including successes, warnings, and failures, without requiring administrators to actively monitor logs.

![Email Alerts](../../../../.gitbook/assets/image-\(4237\).png)

Before email alerts can be sent, email settings must be configured. This includes specifying the SMTP server and port or configuring OAuth application details, along with the required authentication settings, sender address, and recipient addresses.

> \*\*Note\*\*
>
> At the end of a \[publishing sync]\(../../sync-schedule.md), the Publisher sends an email containing details about the sync event.

## Send Email Reports

When this option is enabled, the Publisher sends email alerts and reports based on the configured email settings. When disabled, no email notifications are sent, regardless of the configuration.

## Disable Email for Manual Sync

When this option is enabled, email notifications are sent only for scheduled syncs. Email notifications are _not_ sent when a sync is initiated manually from the [Sync Schedule](../../sync-schedule.md#run-publishing-service-sync) tab.

## Provider

Selecting a predefined provider (such as Exchange Online, Gmail, Outlook, or Yahoo) automatically populates the SMTP server address, port, and TLS settings with recommended values for that service.

For example, selecting **Exchange Online** sets the server to **smtp.office365.com**, port **587**, and enables **TLS**.

If Custom SMTP Provider is selected, all SMTP settings must be entered manually.

> \*\*Note\*\*
>
> You can modify any auto-populated values after selecting a provider if your environment requires different settings.

## Test Email

After configuring the Email Notification settings, click Test Email to verify that the message is successfully sent and received by the configured recipient(s).

If the test email fails, the issue is most commonly related to the SMTP or authentication configuration. For troubleshooting guidance, see [Troubleshooting SMTP Email Report Sending When Using Patch My PC](https://patchmypc.com/troubleshooting-smtp-email-sending).

## **Email Fields**

The following fields control the email message details and recipients.

### **Sender**

Enter the email address you want the alerts to come _from_. e.g. `alerts@yourdomain.com`

> This field is Required.

### **Recipients**

Enter the email address(es) that should _receive_ the alerts. You can enter multiple addresses separated by a semicolon. e.g. `alerts@yourdomain.com; security@yourdomain.com`

> This field is Required.

### **CC Recipients**

Add any additional recipients if needed. You can enter multiple addresses separated by a semicolon. e.g. `alerts@yourdomain.com; security@yourdomain.com`

### Email Subject

The default email subject is `Report from Patch My PC Publishing Service`. If you wish to change this, enter your preferred Subject.

### Additional Text

Enter any additional text you want included at the top of the email report, such as notes or context for your recipients.

## **Email Authentication**

When choosing an authentication method, select the option that aligns with how your mail system accepts SMTP connections.

For internal or on-premises mail servers, [Specified User](email-alerts-settings.md#id-2.-specified-user) is commonly used when the relay supports authenticated SMTP connections.

For cloud-based email services such as Microsoft 365 (Exchange Online) and Google Workspace, [OAuth2 (App Authentication)](email-alerts-settings.md#id-4.-oauth2-app-auth) is recommended, as modern cloud providers increasingly restrict or deprecate username and password–based SMTP authentication.

Ultimately, the appropriate option depends on the authentication methods supported by your SMTP server.

You can choose from the following authentication methods:

1. [Anonymous](email-alerts-settings.md#id-1.-anonymous)
2. [Specified User](email-alerts-settings.md#specified-user)
3. [System](email-alerts-settings.md#id-3.-system)
4. [OAuth2 (App Auth)](email-alerts-settings.md#id-4.-oauth2-app-auth)

### **1. Anonymous**

Use this option only if your SMTP relay explicitly allows unauthenticated sending. Most cloud providers, including Exchange Online, do not support anonymous SMTP. This option typically works only with on-premises SMTP relays configured to accept unauthenticated traffic from trusted internal IP addresses.

> \*\*Note\*\*
>
> When Anonymous is selected, the Login and Password fields are disabled, as no credentials are used for authentication.

#### **Server Configuration**

* **SMTP Server**\
  Enter the DNS name or IP address of the SMTP server that will relay email messages. This is typically an internal Microsoft Exchange server or an on-premises SMTP relay configured to allow anonymous connections.
* **Port**\
  Specify the port used to connect to the SMTP server. Anonymous SMTP relays typically use port 25, depending on how the relay is configured.
* **Use TLS**\
  Enables Transport Layer Security (TLS) for the SMTP connection. Enable this if your relay requires or supports encrypted connections.

### **2. Specific User**

Use this option when your SMTP server requires authentication with a dedicated username and password. This is the most common configuration and is recommended for most environments, including Exchange Online, Google Workspace, and authenticated SMTP relays.

> \*\*Important\*\*
>
> Microsoft Exchange Online has deprecated Basic SMTP authentication and does not support username/password–based SMTP authentication by default. For Exchange Online, OAuth2 (App Authentication) is recommended.
>
> Some providers, such as Google Workspace, may still allow authenticated SMTP using a username and password, but this typically requires additional configuration and may be restricted by tenant security policies.

#### **Specified User**

* **Login**\
  Enter the username used to authenticate to the SMTP server. This is often a full email address but may vary depending on your mail provider or relay configuration.
* **Password**\
  Enter the password associated with the specified SMTP account.

#### **Server Configuration**

* **SMTP Server**\
  Enter the DNS name or IP address of the SMTP server that will relay email messages. This is typically an internal Microsoft Exchange server or an authenticated SMTP relay.
* **Port**\
  Specify the port used to connect to the SMTP server. The appropriate port depends on how the relay is configured and typically supports authenticated SMTP connections.
* **Use TLS**\
  Enables Transport Layer Security (TLS) for the SMTP connection. This encrypts the connection to the SMTP server and is required by most authenticated SMTP relays and cloud-based mail services.

### **3. System**

Use this option to authenticate to the SMTP server using the Windows account under which the Publisher service is running.

Choose this option only if your SMTP relay supports integrated Windows authentication using NTLM or Kerberos. This is typically limited to on-premises Microsoft Exchange servers or internal SMTP relays within the same Active Directory domain.

By default, the Publisher service runs under the **local SYSTEM** account.

> \*\*Note\*\*
>
> When Anonymous is selected, the Login and Password fields are disabled, as no credentials are used for authentication.

* **SMTP Server**\
  Enter the DNS name or IP address of the SMTP server that will relay email messages. This is typically an on-premises Exchange server or an internal SMTP relay configured to allow integrated Windows authentication.
* **Port**\
  Specify the port used to connect to the SMTP server. The appropriate port depends on the relay configuration and support for integrated authentication.
* **Use TLS**\
  Enables Transport Layer Security (TLS) for the SMTP connection. This encrypts the connection to the SMTP server but does not affect authentication. Enable this if your relay requires or supports encrypted connections.

### 4. OAuth2 (App Auth)

Use this option to send email using OAuth 2.0 instead of a mailbox username and password. OAuth2 authenticates using a Microsoft Entra ID app registration and is the recommended approach for modern cloud email services.

For detail guidance on how to configure OAuth 2.0 authentication for Email Notifications, see [OAuth2 (App Auth) Configuration](oauth2-app-auth-configuration.md).

## Save Email Notification Settings

Click **Apply** to save the changes made to the Email Notifications form.

Once the Email Notification settings are saved, the Publisher will automatically send an email at the end of each synchronization when any updates or applications have been published.

## Email Content Overview

The email sent at the end of the sync will include the following details for all Published products:

* Update/Application **Title** (Links to release notes)
* **Time** of Publishing
* **Size** of binary
* Update **Classification**
* Update **Severity Level**
* **CVE’s** (Links to CVE-ID on [https://cve.mitre.org/](https://cve.mitre.org/))

In the example below, you can see an email alert where both **WSUS updates and ConfigMgr applications** were published succesfully.

![Email notification for WSUS updates and ConfigMgr applications](../../../../.gitbook/assets/image-\(3878\).png)

For products published to **Intune**, The email will include the following additional information

* Intune Tenant friendly name
* Intune assignments set during Publishing.

![Email notification for Intune applications](../../../../.gitbook/assets/image-\(3879\).png)

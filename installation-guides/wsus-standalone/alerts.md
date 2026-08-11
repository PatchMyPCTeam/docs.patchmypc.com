---
description: >-
  Get notified when there are new updates available to deploy, or when something
  doesn't quite go as expected.
---

# Alerts

_Applies to: On-premises Publisher_

To keep you informed when new updates have been published, we provide three different ways to get notifications in your environment:

* [Email Report](alerts.md#smtp-settings)
* [Teams Webhook](alerts.md#teams-webhook)
* [Slack Webhook](alerts.md#slack-webhook)

<figure><img src="../../.gitbook/assets/image (3706).png" alt=""><figcaption></figcaption></figure>

## Email Report

{% hint style="info" %}
**IMPORTANT**\
Modern authentication is in development for Patch My PC Publisher. At this time, Publisher relies on basic SMTP authentication for sending email reports.

Please refer to [this](https://patchmypc.com/patch-my-pc-smtp-authentication-for-exchange-online) article for more information on how to enable SMTP authentication for a specific mailbox, which will allow Patch My PC Publisher to authenticate and send emails through your Exchange Online environment.
{% endhint %}

You can configure the Publisher to send email notifications whenever new updates or applications are published. Follow the steps below to set up SMTP correctly.

<figure><img src="../../.gitbook/assets/image (3705).png" alt=""><figcaption></figcaption></figure>

**1. Sender** (Required)\
Enter the email address you want the alerts to come _from_. e.g. `alerts@yourdomain.com`

**2. Recipients** (Required)\
Enter the email address(es) that should _receive_ the alerts. You can enter multiple addresses separated by a semicolon. e.g. `alerts@yourdomain.com; security@yourdomain.com`

**3. CC Recipients** (Optional)\
Add any additional recipients if needed.

**4. Server** (Required)\
Enter your mail server address. e.g. `yoursmtpserver.yourdomain.com`

**5. Port** (Required)\
Typically the SMTP server port is 25, 587, or 465 but this can vary depending on the SMTP provider. If you select **Use TLS**, the Publisher will automatically switch the port to 587 (the standard TLS port), but you can change it if your provider requires a different value.

**6. Email Authentication**\
When choosing an authentication method, select the option that aligns with how your mail system accepts SMTP connections. Some environments allow internal relays without credentials, while most cloud providers require authenticated or TLS-secured connections. The right choice depends on whether your SMTP server supports anonymous relay, requires a dedicated username and password, or allows integrated Windows authentication.

* **Anonymous**\
  Use this only if your SMTP relay explicitly allows unauthenticated sending. Most cloud providers (including Exchange Online) **do not** support anonymous SMTP, so this option typically only works with on-premises mail relays configured to accept unauthenticated traffic from trusted internal IPs.
* **Specified User** (Recommended)\
  Use this when your SMTP server requires authentication. Enter a valid username and password for the mailbox or SMTP relay account you want the Publisher to use.\
  This is the recommended option for most environments, including Exchange Online, Gmail, and any authenticated SMTP relay. Enter a username in the **Login** field and password in the **Password** field to be used for SMTP authentication.
* **System**\
  Uses the Windows account running the Patch My PC Publisher service.\
  Choose this only if your SMTP relay supports integrated authentication (NTLM/Kerberos).\
  This is usually limited to on-prem Exchange servers or internal SMTP relays on the same domain. The Publisher will typically be running in the SYSTEM context.

{% hint style="success" %}
**Note:** At the top of the **SMTP Setttings** section, you can choose from the **Common Email Providers** dropdown (Office 365, Outlook.com, Gmail, etc.).

![](<../../.gitbook/assets/image (3707).png>)

Selecting one will auto-populate the server name, port, and TLS settings for that provider. You can still change any field manually afterwards.
{% endhint %}

**7. Change Subject** (Optional)\
The default email subject is `Report from Patch My PC Publishing Service`. If you wish to change this, click **Change subject**, enter your preferred **Subject of the email**, and click **Ok**.

<figure><img src="../../.gitbook/assets/image (3708).png" alt=""><figcaption></figcaption></figure>

Once the settings are complete, you can click the **Test button** to see if the recipient received the test email. If you have any issues sending emails, it’s likely an SMTP configuration error, and you can review our article [**Troubleshooting SMTP Email Report Sending When Using Patch My PC**](https://patchmypc.com/troubleshooting-smtp-email-sending).

**8. Add text to body** (Optional)\
Enter any additional text you want included at the top of the email report, such as notes or context for your recipients.

<figure><img src="../../.gitbook/assets/image (3709).png" alt=""><figcaption></figcaption></figure>

**9.** Click **Apply** to save your changes.

Once the SMTP settings are saved, the Publisher will automatically send an email at the end of each synchronization when any updates or applications have been published. More information on how publishing alerts work for email, please review the following knowledgebase article.

{% embed url="https://patchmypc.com/kb/how-publishing-alerts-work-patch/#h-smtp-settings" %}

If you have issues setting up SMTP emails, check out our troubleshooting guide below.

{% embed url="https://patchmypc.com/troubleshooting-smtp-email-sending" %}
SMTP email troubleshooting
{% endembed %}

## Teams Webhook

The Microsoft Teams webhook is a simple way to get a notification for each application as it is published in yourenvironment. Simply create a new workflow in the Teams channel where you wish to receive notifications, and use that Webhook URL when configuring webhook alerts in the Publisher.

<figure><img src="../../.gitbook/assets/image (3711).png" alt=""><figcaption></figcaption></figure>

Need help creating the webhook in teams? No problem, check out our complete guide to creating a Teams webhook.&#x20;

{% embed url="https://patchmypc.com/kb/how-publishing-alerts-work-patch/#h-how-to-create-a-microsoft-teams-webhook-url" %}

## Slack Webhook

The Slack webhook is another simple way to get a notification for each application as it is published in your environment. Simply create a new webhook in Slack and use that Webhook URL when configuring webhook alerts in the Publisher.

<figure><img src="../../.gitbook/assets/image (1809).png" alt=""><figcaption></figcaption></figure>

Need help creating the webhook for Slack? No problem, check out our complete guide to creating a Slack webhook.&#x20;

{% embed url="https://patchmypc.com/kb/how-publishing-alerts-work-patch/#h-how-to-create-a-slack-webhook-url" %}

# Send email reports in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

When the **Send email reports** option on the **Email Alerts** tab of Patch My PC (PMPC) Publisher is enabled (which it is by default), Publisher sends email alerts and reports based on the configured email settings on this tab.

When disabled, no email notifications are sent, regardless of the configuration.

<figure><img src="../../../../.gitbook/assets/image (1319).png" alt="&#x27;Send email reports&#x27; option" width="563"><figcaption></figcaption></figure>

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

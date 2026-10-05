# Send webhook reports in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

When the **Send webhook reports** option on the **Webhooks** tab of Patch My PC (PMPC) Publisher is enabled, Publisher can send publishing alerts and reports to external messaging systems such as Microsoft Teams workflows and Slack. Webhooks provide near real-time visibility into publishing activity without relying on email notifications.

<figure><img src="../../../../.gitbook/assets/image (1325).png" alt="&#x27;Send webhook reports&#x27; option" width="563"><figcaption></figcaption></figure>

Webhook notifications are commonly used to notify operations, security, or platform teams when publishing events occur.

When webhook notifications are enabled, the Publisher sends HTTP POST messages to the configured webhook endpoints based on publishing events and the selected notification level. Each configured webhook represents a single destination, such as a Teams channel or Slack workspace.

You can configure multiple webhook destinations, and you can independently enable, disable, test, or remove each webhook.

# Webhook Notification Settings in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

**Webhook notifications** allow the Patch My PC (PMPC) Publisher to send publishing alerts and reports to external messaging systems such as Microsoft Teams workflows and Slack. Webhooks provide near real time visibility into publishing activity without relying on email notifications.

Webhook notifications are commonly used to notify operations, security, or platform teams when publishing events occur.

![Webhook Notifications](../../../../.gitbook/assets/image-\(4208\).png)

When webhook notifications are enabled, the Publisher sends HTTP POST messages to the configured webhook endpoints based on publishing events and the selected notification level. Each configured webhook represents a single destination, such as a Teams channel or Slack workspace.

Multiple webhook destinations can be configured, and each webhook can be independently enabled, disabled, tested, or removed.

## Send Webhook Reports

Webhook notifications must be enabled before individual webhooks can be configured.

1. Open the Publisher console and navigate to **Alerts**.
2. Expand **Webhook Notifications**.
3. Select **Send Webhook Reports** to enable webhook notifications.

![Send Webhook Reports](<../../../../.gitbook/assets/image-(31) (1).png>)

## Add a Webhook

Use this option to create a new webhook notification.

1. To add a new webhook notification, click **Add**.

![Add a Webhook Notification](<../../../../.gitbook/assets/image-(32) (1).png>)

2. Continue to [Edit a Webhook](settings.md#edit-a-webhook).

## Edit a Webhook

Use this option to configure a new webhook after clicking Add, or to modify an existing webhook by updating settings such as the webhook URL, notification level, or label.

The **Edit** option opens the webhook configuration dialog. This dialog is used in two scenarios.

* After clicking [Add](settings.md#add-a-webhook) when creating a new webhook.
* When selecting an existing webhook and clicking **Edit**.

![Edit a Webhook](<../../../../.gitbook/assets/image-(33) (1).png>)

In both cases, the same configuration screen is used to define or modify the [webhook configuration](../../../../patch-my-pc-publisherv2/administration/alerts/webhook-notifications/webhook-configuration.md).

## Copy a Webhook

Use this option to create a new webhook configuration based on an existing webhook.

![Copy a Webhook](<../../../../.gitbook/assets/image-(34) (1).png>)

When you select a webhook and click Copy, the [webhook configuration](../../../../patch-my-pc-publisherv2/administration/alerts/webhook-notifications/webhook-configuration.md) dialog opens with settings pre populated from the selected webhook. You must provide a new **Name** and **Webhook URL** before the webhook can be saved.

All other settings are copied from the original webhook, including the message system and notification level. Webhook scope and product selection are also copied, allowing the new webhook to inherit the same filtering and targeting configuration.

## Remove a Webhook

Use this option to delete a webhook.

When you select a webhook and click **Remove**, the webhook is removed from the list and will no longer receive notifications.

![Remove a Webhook](<../../../../.gitbook/assets/image-(35) (1).png>)

> \*\*Important\*\*
>
> Removing a webhook does not display a confirmation dialog. The webhook is permanently deleted after the Publisher settings are saved. If you close and re-open the Publisher without savings the Publisher settings, the deleted webhook is restored.

## Test a Webhook

Use this option to validate an individual webhook configuration by sending a test notification to the selected destination.

Each webhook is tested independently. Only the selected webhook is used when the test is run.

![Test a Webhook](../../../../.gitbook/assets/image-\(36\).png)

The Publisher sends a test HTTP POST message to the webhook URL configured for the selected webhook.

If the test is successful, a confirmation message is displayed indicating that the test webhook notification was sent successfully. The message should also appear in the target system, such as a Microsoft Teams channel or Slack workspace.

![Successful Webhook Test](../../../../.gitbook/assets/image-\(3900\).png)

If the test fails, an error message is displayed. The error typically indicates connectivity issues, an invalid webhook URL, or a response error from the destination service. The webhook must be corrected before notifications will work.

![Failed Webhook Test](../../../../.gitbook/assets/image-\(3899\).png)

# Create a Slack Webhook URL in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

Slack webhooks allow the Patch My PC (PMPC) Publisher to send publishing notifications to a specific Slack channel. Notifications can be sent after each product is processed or as a single summary message at the end of a publishing synchronization, depending on the webhook configuration.

To configure a Slack webhook URL:

1. Navigate to [https://api.slack.com/apps](https://api.slack.com/apps) and and sign in to your Slack account.
2. Select **Create an App** or **Create New App** if you have already created apps previously. Depending on your Slack configuration, you may need to be a workspace owner or have permission to create apps.

![Create an App](../../../../.gitbook/assets/image-\(180\).png)

![Create New App](../../../../.gitbook/assets/image-\(181\).png)

3. Select From scratch.

![From Scratch](../../../../.gitbook/assets/image-\(183\).png)

4. Enter an app name, select the workspace where the app will be created, then select **Create App**.

![Select the Workspace and name the App](../../../../.gitbook/assets/image-\(184\).png)

5. In the app configuration, toggle On **Activate Incoming Webhooks**.

![Activate Incoming Webhooks](../../../../.gitbook/assets/image-\(186\).png)

6. Select Add New Webhook to Workspace.

![Add New Webhook](../../../../.gitbook/assets/image-\(187\).png)

7. Select the Slack channel where you want to receive Publisher notifications, then select **Allow**.

![Allow the app to access Slack](../../../../.gitbook/assets/image-\(188\).png)

8. **Copy** the generated webhook URL.

![Copy the Webhook URL](../../../../.gitbook/assets/image-\(189\).png)

The copied URL can be used when [adding](../../../../patch-my-pc-publisherv2/administration/alerts/webhook-notifications/webhook-notification-settings.md#add-a-webhook) or [editing](../../../../patch-my-pc-publisherv2/administration/alerts/webhook-notifications/webhook-notification-settings.md#edit-a-webhook) a webhook in the Publisher.

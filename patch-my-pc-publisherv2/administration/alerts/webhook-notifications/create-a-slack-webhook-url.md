# Create a Slack Webhook URL

_Applies to: Patch My PC Publisher V2.x_

Slack webhooks allow the Publisher to send publishing notifications to a specific Slack channel. Notifications can be sent after each product is processed or as a single summary message at the end of a publishing synchronization, depending on the webhook configuration.

To configure a Slack webhook URL:

1. Navigate to [https://api.slack.com/apps](https://api.slack.com/apps) and and sign in to your Slack account.
2. Select **Create an App** or **Create New App** if you have already created apps previously. Depending on your Slack configuration, you may need to be a workspace owner or have permission to create apps.

![Create an App](/_images/image-(180).png)

![Create New App](/_images/image-(181).png)

3. Select From scratch.

![From Scratch](/_images/image-(183).png)

4. Enter an app name, select the workspace where the app will be created, then select **Create App**.

![Select the Workspace and name the App](/_images/image-(184).png)

5. In the app configuration, toggle On **Activate Incoming Webhooks**.

![Activate Incoming Webhooks](/_images/image-(186).png)

6. Select Add New Webhook to Workspace.

![Add New Webhook](/_images/image-(187).png)

7. Select the Slack channel where you want to receive Publisher notifications, then select **Allow**.

![Allow the app to access Slack](/_images/image-(188).png)

8. **Copy** the generated webhook URL.

![Copy the Webhook URL](/_images/image-(189).png)

The copied URL can be used when [adding](webhook-notification-settings.md#add-a-webhook) or [editing](webhook-notification-settings.md#edit-a-webhook) a webhook in the Publisher.
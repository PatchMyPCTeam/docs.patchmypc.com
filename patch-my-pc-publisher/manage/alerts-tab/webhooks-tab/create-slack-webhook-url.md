# Create a Slack Webhook URL in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Slack webhooks allow Patch My PC (PMPC) Publisher to send publishing notifications to a specific Slack channel. Notifications can be sent after each product is processed or as a single summary message at the end of a publishing synchronization, depending on the webhook configuration.

To configure a Slack webhook URL:

1. Navigate to [https://api.slack.com/apps](https://api.slack.com/apps) and and sign in to your Slack account.
2. Select **Create an App** or **Create New App** if you have already created apps previously. Depending on your Slack configuration, you may need to be a workspace owner or have permission to create apps.

<figure><img src="../../../../.gitbook/assets/image (180).png" alt="Create an App" width="563"><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (181).png" alt="Create New App" width="563"><figcaption></figcaption></figure>

3. Select From scratch.

<figure><img src="../../../../.gitbook/assets/image (182).png" alt="From Scratch" width="403"><figcaption></figcaption></figure>

4. Enter an app name, select the workspace where the app will be created, then select **Create App**.

<figure><img src="../../../../.gitbook/assets/image (184).png" alt="Select the Workspace and name the App" width="409"><figcaption></figcaption></figure>

5. In the app configuration, toggle On **Activate Incoming Webhooks**.

<figure><img src="../../../../.gitbook/assets/image (185).png" alt="Activate Incoming Webhooks" width="563"><figcaption></figcaption></figure>

6. Select Add New Webhook to Workspace.

<figure><img src="../../../../.gitbook/assets/image (187).png" alt="Add New Webhook" width="439"><figcaption></figcaption></figure>

7. Select the Slack channel where you want to receive Publisher notifications, then select **Allow**.

<figure><img src="../../../../.gitbook/assets/image (188).png" alt="Allow the app to access Slack" width="563"><figcaption></figcaption></figure>

8. **Copy** the generated webhook URL.

<figure><img src="../../../../.gitbook/assets/image (189).png" alt="Copy the Webhook URL" width="563"><figcaption></figcaption></figure>

The copied URL can be used when [adding](../../../../patch-my-pc-publisherv2/administration/alerts/webhook-notifications/webhook-notification-settings.md#add-a-webhook) or [editing](../../../../patch-my-pc-publisherv2/administration/alerts/webhook-notifications/webhook-notification-settings.md#edit-a-webhook) a webhook in the Publisher.

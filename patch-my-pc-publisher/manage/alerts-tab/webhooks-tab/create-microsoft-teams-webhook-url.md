# Create a Microsoft Teams Webhook URL in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

## Create a Workflow

Microsoft Teams webhooks used by the Patch My PC (PMPC) Publisher are created using Teams Workflows. This workflow generates a webhook URL that can be used to send notifications to a specific Teams channel.

To create a webhook URL:

1. Open Microsoft Teams and navigate to the Channel where you want to receive Webhook Notifications.
2. Click the More Options button **…** and select **Workflows**.

<figure><img src="../../../../.gitbook/assets/image (225).png" alt="Teams Workflows" width="524"><figcaption></figcaption></figure>

3. Select **Send webhook alerts to a channel**.

<figure><img src="../../../../.gitbook/assets/image (226).png" alt="Send webhook alerts to a channel" width="429"><figcaption></figcaption></figure>

4. Allow a moment for the template to load, it can take a minute. Optionally, update the **Name** of the workflow so it can be easily distingushed in PowerAutomate. Click **Next.**

<figure><img src="../../../../.gitbook/assets/image (227).png" alt="Name the workflow" width="563"><figcaption></figcaption></figure>

5. Allow a moment for the details tab to load to verify which Team and Channel the webhook URL will be created for and click **Add workflow**.

<figure><img src="../../../../.gitbook/assets/image (228).png" alt="Add the workflow" width="563"><figcaption></figcaption></figure>

6. Click the **copy** icon to copy the webhook URL to your clipboard before click **Done**.

<figure><img src="../../../../.gitbook/assets/image (229).png" alt="Copy the webhook URL" width="563"><figcaption></figcaption></figure>

The copied URL can be used when [adding ](../../../../patch-my-pc-publisherv2/administration/alerts/webhook-notifications/webhook-notification-settings.md#add-a-webhook)or [editing ](../../../../patch-my-pc-publisherv2/administration/alerts/webhook-notifications/webhook-notification-settings.md#edit-a-webhook)a webhook in the Publisher.

## Consideration for Teams Private Channels

Microsoft Teams private channels have stricter permission boundaries than standard channels. Workflows created using Power Automate run as bots by default, and bots are not permitted to post messages to private channels unless explicitly configured.

To allow webhook notifications to be delivered to a private channel, the workflow must be updated to post messages as a user instead of as a bot.

Update the Workflow **Post As** Setting:

1. Navigate to [https://make.powerautomate.com](https://make.powerautomate.com/)
2. Locate the workflow used for Teams notifications targeting the private channel and select **Edit**.

<figure><img src="../../../../.gitbook/assets/image (3910).png" alt="Edit the Workflow" width="563"><figcaption></figcaption></figure>

3. Select the workflow step named **Post card in a chat or channel**
4. Change the **Post As** value from **Bot** to **User**.

<figure><img src="../../../../.gitbook/assets/image (3911).png" alt="Post as User not Bot" width="563"><figcaption></figcaption></figure>

5\. Save the workflow.

After this change, webhook notifications can be successfully delivered to Microsoft Teams private channels.

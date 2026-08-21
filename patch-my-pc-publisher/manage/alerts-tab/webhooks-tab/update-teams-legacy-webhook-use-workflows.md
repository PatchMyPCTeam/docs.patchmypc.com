# Update a Microsoft Teams Legacy Webhook to Use Workflows in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Older Office 365 connectors previously used for Microsoft Teams webhooks are deprecated. Microsoft announced the retirement of these connectors. For more information, see [Retirement of Office 365 connectors within Microsoft Teams on the Microsoft Developer](https://devblogs.microsoft.com/microsoft365dev/retirement-of-office-365-connectors-within-microsoft-teams/) blog.

Microsoft Teams Workflows use the Adaptive Message Card format. Legacy Microsoft Teams webhooks created in earlier versions of the Publisher use the older Message Card format.

It is recommended that any webhook configured in the Patch My PC (PMPC) Publisher using the **MSTeams** message system be updated to use **MSTeamsWorkflow**.

<figure><img src="../../../../.gitbook/assets/image (212).png" alt="MSTeamsWorkflow vs MSTeams Message System" width="509"><figcaption></figcaption></figure>

## Update an Existing Webhook

1. Create a new Microsoft Teams workflow webhook URL by following the steps in [Create a Microsoft Teams Webhook URL](../../../../patch-my-pc-publisherv2/administration/alerts/webhook-notifications/create-a-microsoft-teams-webhook-url.md).
2. In the Publisher, navigate to Alerts and expand Webhook Notifications.
3. Select the existing webhook that uses the Microsoft Teams legacy provider and click Edit.
4. Change the Webhook Provider from **Microsoft Teams (Legacy Webhook)** to **Microsoft Teams Workflow**.

<figure><img src="../../../../.gitbook/assets/image (213).png" alt="Change the Webhook Provider" width="450"><figcaption></figcaption></figure>

1. Replace the existing Webhook URL with the new workflow webhook URL.
2. Click **OK**, then click **Apply** to save the changes.

After completing these steps, the webhook uses the modern Microsoft Teams Workflow model and sends notifications using the Adaptive Message Card format.

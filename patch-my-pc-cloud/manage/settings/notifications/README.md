# Manage Notifications in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Once onboarded to Patch My PC (PMPC) Cloud, you can use the **Notifications** node to configure notifications to be sent from the portal to:

* Microsoft Teams
* Slack
* Email addresses

{% hint style="info" %}
**Note**

If configured and regardless of whether or not the deployment uses Update Rings, we send Slack/webhook notifications whenever:

* A new deployment is created.
* The version of an existing deployment is updated.
* A new Update Ring is created.
* An existing Update Ring is upgraded to a later version
* An admin clicks [Sync Now](../../../deployments/manage-deployments/updates/sync-now.md) to force a deployment to update immediately to the latest version without waiting for the Sync Schedule to run.

Provided you have configured an [email notification](create-email-notification.md), six hours after your [Sync Schedule](../sync-schedule.md) has run, the [Updates Report](../../../technical-references/cloud-email-reference/example-cloud-updates-report-email.md) will be generated and sent to the configured email addresses.

On this report:

* A new deployment appears as **Initial Deployment Created**.
* An existing deployment updated to a newer version appears as **Version Update**.
{% endhint %}

To configure Notifications:

1. Sign in to the portal [https://portal.patchmypc.com/](https://portal.patchmypc.com/).
2. Navigate to **Settings | Notifications**

<figure><img src="../../../../.gitbook/assets/image (298).png" alt="Navigating to &#x27;Settings | Notifications&#x27;" width="563"><figcaption></figcaption></figure>

The **Notifications** page is then displayed, showing any existing Notifications and allowing you to:

* [Add a Notification](add-notification.md)
* [Modify a Notification](modify-notification.md)
* [Delete a Notification](delete-notification.md)

<figure><img src="../../../../.gitbook/assets/image (299).png" alt="&#x27;Notifications&#x27; page" width="563"><figcaption></figcaption></figure>

# Manage Notifications in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Once onboarded to Patch My PC (PMPC) Cloud, you can use the **Notifications** node to configure notifications to be sent from the portal to:

* Microsoft Teams
* Slack
* Email addresses

> \*\*Note\*\*
>
> If configured and regardless of whether or not the deployment uses Update Rings, we send Slack/webhook notifications whenever:
>
> \* A new deployment is created.
>
> \* The version of an existing deployment is updated.
>
> \* A new Update Ring is created.
>
> \* An existing Update Ring is upgraded to a later version
>
> \* An admin clicks \[Sync Now]\(../../../deployments/manage-deployments/updates/sync-now.md) to force a deployment to update immediately to the latest version without waiting for the Sync Schedule to run.
>
> Provided you have configured an \[email notification]\(create-email-notification.md), six hours after your \[Sync Schedule]\(../sync-schedule.md) has run, the \[Updates Report]\(../../../technical-references/cloud-email-reference/example-cloud-updates-report-email.md) will be generated and sent to the configured email addresses.
>
> On this report:
>
> \* A new deployment appears as \*\*Initial Deployment Created\*\*.
>
> \* An existing deployment updated to a newer version appears as \*\*Version Update\*\*.

To configure Notifications:

1. Sign in to the portal [https://portal.patchmypc.com/](https://portal.patchmypc.com/).
2. Navigate to **Settings | Notifications**

![Navigating to 'Settings | Notifications'](../../../../.gitbook/assets/image-\(298\).png)

The **Notifications** page is then displayed, showing any existing Notifications and allowing you to:

* [Add a Notification](add-notification.md)
* [Modify a Notification](modify-notification.md)
* [Delete a Notification](delete-notification.md)

!['Notifications' page](../../../../.gitbook/assets/image-\(299\).png)

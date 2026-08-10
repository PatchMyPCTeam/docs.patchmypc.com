# Create an Email Notification in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

You can create an email notification in Patch My PC (PMPC) Cloud to automatically receive a daily email report with details of all deployments that have been created and updated after the daily sync with our publishing service has been completed.

{% hint style="info" %}
**Note**

We strongly recommend you create at least one email notification so you can easily track what is happening in your environment. See [Example Updates Report Email](../../../technical-references/cloud-email-reference/example-cloud-updates-report-email.md) for an example of the Updates Report email you will receive six hours after the daily sync job has run.
{% endhint %}

To create an email notification:

1. Navigate to **Settings | Notifications**
2. On the **Add Notifications** screen, enter a unique name for this notification in the **Name** field.

<figure><img src="../../../../.gitbook/assets/image (3837).png" alt="&#x27;Add Notifications&#x27; screen" width="563"><figcaption></figcaption></figure>

3. In the **User Email** field, select the relevant administrator’s email address from the dropdown or type their email address.

<figure><img src="../../../../.gitbook/assets/image (3838).png" alt="Selecting the relevant administrator’s email address from the dropdown or type their email address" width="563"><figcaption></figcaption></figure>

The user's email address is added to the **Email** list that will receive the notification.

<figure><img src="../../../../.gitbook/assets/image (3839).png" alt="User&#x27;s email address is added to the email list that will receive the notification" width="563"><figcaption></figcaption></figure>

4. Repeat Step 3 to add any additional email addresses.

{% hint style="success" %}
**Tip**

You can click the small envelope beside the email address (![](<../../../../.gitbook/assets/image (2602).png>)) to send a test notification. See [Testing an Email Notification](technical-references/test-email-notification.md) for more details.
{% endhint %}

{% hint style="info" %}
**Note**

You can add more than one email address. The email address must be in a valid format and can be for an address outside your Intune tenant.

You can also click the trashcan beside an email address to delete it from the list of email addresses to be notified (you may need to scroll down to see the full list).
{% endhint %}

5. Click **Save** on the **Add Notifications** screen to save the notification.

<figure><img src="../../../../.gitbook/assets/image (3840).png" alt="Clicking &#x27;Save&#x27;" width="563"><figcaption></figcaption></figure>

The **Success - Notification created** notification is shown.

<figure><img src="../../../../.gitbook/assets/image (3841).png" alt="&#x27;Success&#x27; notification" width="563"><figcaption></figcaption></figure>

The Cloud Portal auto-refreshes to show the new notification, including abbreviations of the users who will receive the email notification.

<figure><img src="../../../../.gitbook/assets/image (3842).png" alt="Cloud Portal auto-refreshing" width="563"><figcaption></figcaption></figure>

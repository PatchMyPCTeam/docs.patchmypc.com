# What happens if the Patch My PC Cloud Enterprise App is deleted?

_Applies to: Intune Apps for Cloud_

If the **Patch My PC Cloud** Enterprise App is deleted, you will experience the following limitations/issues:

* If you have configured [email notifications](../../manage/settings/notifications/create-email-notification.md), you will receive an email from Patch My PC with the subject **Intune Permissions Issue Detected**.

{% hint style="info" %}
**Note**

See [Why have I received an "Intune Permissions Issue Detected" notification email from Patch My PC?](why-have-i-received-an-intune-permissions-issue-detected-notification-email-from-patch-my-pc.md) for more details.
{% endhint %}

* Only Custom Apps are shown in the App Catalog, but they cannot be deployed.
* The **Deployments** node is missing.

{% hint style="success" %}
**Tip**

You can verify the permissions granted to the **Patch My PC Cloud** Enterprise App by navigating to **Home | Enterprise applications | Patch My PC Cloud | Security | Permissions** in the Microsoft Azure portal.
{% endhint %}

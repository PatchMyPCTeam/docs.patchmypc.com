# Delete Branding in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

{% hint style="danger" %}
**Important**

You cannot delete a branding app unless it has been deployed successfully or failed to deploy.

Also:

* Each branding app must contain at least one localization. You cannot delete all localizations for a branding app.
* Deleting a branding app only removes it from Intune and does not remove any custom logos, files or localizations from your end-user devices. To do this, you need to create an [Uninstall Branding App](uninstall-branding.md).
{% endhint %}

{% hint style="info" %}
**Note**

The process for deleting a branding app is the same, regardless of the type (Classic or Modern (PSADT)).
{% endhint %}

To delete a Branding App:

1. Navigate to **Settings | Branding**

<figure><img src="../../../../.gitbook/assets/image (554).png" alt="Navigating to ‘Settings | Branding’" width="563"><figcaption></figcaption></figure>

2. Click the ellipsis (`⋮`) button beside the relevant Branding App and select **Delete**.

<figure><img src="../../../../.gitbook/assets/image (3751).png" alt="Selecting &#x27;Delete&#x27; from the ellipsis menu" width="563"><figcaption></figcaption></figure>

3. Read the **Are you sure** dialog box, and if you want to continue, click **Yes**.

<figure><img src="../../../../.gitbook/assets/image (3210).png" alt="&#x22;Are you sure&#x22; dialog box" width="287"><figcaption></figcaption></figure>

The **Success - <**_**branding\_app\_name**_**> deleted** notification is shown.

<figure><img src="../../../../.gitbook/assets/image (3752).png" alt="&#x27;Success - <branding_app_name> deleted&#x27; notification" width="563"><figcaption></figcaption></figure>

The **Branding** screen is redisplayed, showing that the Branding App has been deleted.

<figure><img src="../../../../.gitbook/assets/image (3753).png" alt="&#x27;Branding&#x27; screen is redisplayed showing the branding app has been deleted." width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

If you look in the **Events** node, you will see a message stating the Branding App has been deleted.
{% endhint %}

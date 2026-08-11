# Modify/Recreate Branding in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Once you have created a branding app in Patch My PC (PMPC) Cloud, you can modify it.

{% hint style="info" %}
**Note**&#x20;

The process for modifying a branding app is the same, regardless of the type (Classic or Modern (PSADT)).&#x20;
{% endhint %}

To modify a branding app:

1. Navigate to **Settings | Branding**

<figure><img src="../../../../.gitbook/assets/image (536).png" alt="Navigating to ‘Settings | Branding’" width="563"><figcaption></figcaption></figure>

2. Click the ellipsis (`⋮`) button beside the relevant branding app and select the action you want to perform:
   1. [Edit](modify-recreate-branding.md#edit-branding)
   2. [Recreate](modify-recreate-branding.md#recreate-branding)

{% hint style="info" %}
**Note**

See [Delete Branding](delete-branding.md) for details on how to delete a branding app.

You won’t be able to manage a branding app until it has been deployed successfully.

Also, see [Managing Localizations](localizations.md) for details on how to modify the localization used by a branding app.
{% endhint %}

### Edit Branding

Editing a branding app allows you to make any changes as though you were [Adding a Branding App](add-branding.md).

{% hint style="info" %}
**Note**

The process for editing a branding app is the same, regardless of the type (Classic or Modern (PSADT).
{% endhint %}

If you want to reset the logo used by a branding app:

1. Click **Edit** on the ellipsis (`⋮`) menu.

<figure><img src="../../../../.gitbook/assets/image (3743).png" alt="Clicking the ellipsis (⋮) button beside the relevant branding app and selecting the action you want to perform:" width="563"><figcaption></figcaption></figure>

2. In the **Company Logo** area, click **Use Default**.

<figure><img src="../../../../.gitbook/assets/image (538).png" alt="Clicking &#x27;Use Default&#x27; in the &#x27;Company Logo&#x27; area" width="563"><figcaption></figcaption></figure>

The **Branding** page resets just the logo to the default for this branding app.

<figure><img src="../../../../.gitbook/assets/image (539).png" alt="Branding logo reset" width="563"><figcaption></figcaption></figure>

3. If you want to switch branding types, select the relevant option under **Branding Types**

<figure><img src="../../../../.gitbook/assets/image (540).png" alt="Select the relevant option under &#x27;Branding Types&#x27; if you want to change the type" width="563"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

If you switch branding types, you will see the **Are you sure** prompt, asking you to confirm the switch.&#x20;

!['Are you sure' prompt](<../../../../.gitbook/assets/image (541).png>)

Click **Confirm** to continue, but please note that by switching branding types, you will lose any configured localizations and settings configured for this branding app. Once you switch types, you should verify your localizations are configured as detailed in [Manage Localizations in Cloud](localizations.md).
{% endhint %}

4. Make any other required changes.
5. Click **Save** to save your changes to Intune, which will deploy the modified version to all of the resources this branding app is assigned to.

<figure><img src="../../../../.gitbook/assets/image (542).png" alt="Clicking &#x27;Save&#x27; to save your changes" width="563"><figcaption></figcaption></figure>

The **Success - Branding updated** notification is shown.

<figure><img src="../../../../.gitbook/assets/image (3744).png" alt="&#x27;Success - Branding updated&#x27; notification" width="563"><figcaption></figcaption></figure>

Once your branding app has been updated with the default PMPC logo, the **Status** and **Last Updated** fields will be updated to show when this branding app was last updated.

<figure><img src="../../../../.gitbook/assets/image (3745).png" alt="&#x27;Status&#x27; and &#x27;Last Updated&#x27; fields updated to show when this branding app was last updated" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

If you look in the **Events** section, you see a message stating the branding app was updated.
{% endhint %}

5. The branding app will be automatically updated on all of the assigned resources. There is no need for you to [Recreate Branding](modify-recreate-branding.md#recreate-branding) as in previous versions.

### Recreate Branding

The **Recreate** function allows you to delete and recreate a branding app in Intune if you detect an issue with it.

{% hint style="danger" %}
**Important**

You can only recreate branding apps that have either been deployed successfully or failed.
{% endhint %}

{% hint style="info" %}
**Note**

The process for recreating a branding app is the same, regardless of the type (Classic or Modern (PSADT)).
{% endhint %}

To recreate branding:

1. Click **Recreate** on the ellipsis (`⋮`) menu.

<figure><img src="../../../../.gitbook/assets/image (3746).png" alt="Clicking &#x27;Recreate&#x27; on the ellipsis (⋮) menu" width="563"><figcaption></figcaption></figure>

2. On the **Are you sure you want to recreate <**_**branding\_app\_name**_**>** dialog box click **Yes**.

<figure><img src="../../../../.gitbook/assets/image (3205).png" alt="Clicking &#x22;Yes&#x22;" width="287"><figcaption></figcaption></figure>

The **Success - Recreating the branding <**_**branding\_app\_name**_**>** notification is shown.

<figure><img src="../../../../.gitbook/assets/image (3747).png" alt="&#x27;Success - Recreating the branding <branding_app_name>&#x27; notification" width="563"><figcaption></figcaption></figure>

Once the branding app has been recreated, the **Status** and **Last Updated** fields update to show when this branding app was last modified.

<figure><img src="../../../../.gitbook/assets/image (3748).png" alt="&#x27;Status&#x27; and &#x27;Last updated&#x27; fields updated to show when this branding app was last modified" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

If you look in the **Events** node, you see a message stating the branding app was recreated
{% endhint %}

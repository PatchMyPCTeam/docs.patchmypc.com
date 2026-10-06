# All Notifications section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **All Notifications** section on the **Webhooks** tab of Patch My PC (PMPC) Publisher allows you to perform the following actions on webhooks:

* [Test](all-notifications.md#test-button)
* [Copy](all-notifications.md#copy-button)
* [Advanced](all-notifications.md#advanced-button)
* [Remove](all-notifications.md#remove-button)

<figure><img src="../../../../.gitbook/assets/image (1338).png" alt="&#x27;All Notifications&#x27; section" width="528"><figcaption></figcaption></figure>

## Test button

Clicking **Test** sends a test notification for the selected webhook to the configured destination, so you know the webhook has been configured correctly and is working.

### To test a webhook

1. Load Publisher.
2. Navigate to **Alerts | Webhooks**.
3. Click the webhook you want to test, then click **Test**.

<figure><img src="../../../../.gitbook/assets/image (1341).png" alt="Clicking the webhook to test, then clicking &#x27;Test&#x27;." width="563"><figcaption></figcaption></figure>

Publisher sends a test HTTP POST message to the webhook URL configured for the selected webhook.

If the test is successful, the **Webhook Test** popup shows:

**A test webhook notification has been successfully sent**

<figure><img src="../../../../.gitbook/assets/image (1339).png" alt="A test webhook notification has been successfully sent" width="320"><figcaption></figcaption></figure>

The message should also appear in the target system, such as a Microsoft Teams channel or Slack workspace.

If the test fails, the **Webhook Send Error** is displayed with the resulting error, which can be copied to the Windows Clipboard to allow you to investigate the issue. The error typically indicates connectivity issues, an invalid webhook URL, or a response error from the destination service. The webhook must be configured correctly before notifications will work.

<figure><img src="../../../../.gitbook/assets/image (3899).png" alt="Failed Webhook Test" width="427"><figcaption></figcaption></figure>

## Copy button

Clicking **Copy** creates a new webhook based on the configuration of the selected webhook.

### To copy a webhook

1. Load Publisher.
2. Navigate to **Alerts | Webhooks**.
3. Click the existing webhook you want to copy, then click **Copy**.

<figure><img src="../../../../.gitbook/assets/image (1343).png" alt="Clicking the webhook you want to copy, then clicking &#x27;Copy&#x27;." width="563"><figcaption></figcaption></figure>

The existing webhook is copied and selected. The new webhook is appended with **- Copy** at the end of the name so you know you are working on the copy, not the original.

<figure><img src="../../../../.gitbook/assets/image (1345).png" alt="Copy of an existing webhook" width="563"><figcaption></figcaption></figure>

4. Update the **Name** field with a new name.
5. Update the **Webhook URL** field with the new webhook URL for this webhook.

{% hint style="info" %}
**Note**

If you attempt to save the new webhook without updating the **Webhook URL** field, the **Save Failed** dialog appears, telling you that you must update the **Webhook URL** field.

![Save failed](<../../../../.gitbook/assets/image (1346).png>)

All other settings are copied from the original webhook, including the message system and notification level. Webhook scope and product selection are also copied, allowing the new webhook to inherit the same filtering and targeting configuration.
{% endhint %}

6. Make any required changes to the configuration of the new webhook, then click **Apply** to save your changes.

{% hint style="success" %}
**Tip**

See [Add a Webhook](add-webhook.md) for more information on the available options.
{% endhint %}

7. Once you have saved the new webhook, click [Test](all-notifications.md#test-button) to ensure it works.

## Advanced button

Clicking **Advanced** allows you to configure advanced settings for the webhook.

## Remove button

Clicking **Remove** deletes the selected webhook.

### To remove a webhook

1. Load Publisher.
2. Navigate to **Alerts | Webhooks**.
3. Click the webhook you want to remove, then click **Remove**.

<figure><img src="../../../../.gitbook/assets/image (1355).png" alt="Clicking &#x27;Remove&#x27;" width="563"><figcaption></figcaption></figure>

The webhook is deleted from Publisher.

<figure><img src="../../../../.gitbook/assets/image (1359).png" alt="Webhook deleted" width="215"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

Removing a webhook does not display a confirmation dialog. The webhook is permanently deleted after the Publisher settings are saved. If you close and reopen Publisher without clicking **Apply**, the removed webhook will still appear.
{% endhint %}

4. Click **Apply**.

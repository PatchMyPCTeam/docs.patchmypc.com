# Update a Binary Free App

_Applies to: Binary Free Apps for Patch My PC Cloud_

There are two ways to update the version of a Patch My PC (PMPC) Cloud Binary Free App:

* [From the update notification email](update-a-binary-free-app.md#update-a-binary-free-app-from-the-notification-email)
* [From the App Catalog](update-a-binary-free-app.md#update-a-binary-free-app-from-the-app-catalog)

{% hint style="info" %}
**Note**

Regardless of which method you use to update the Binary Free App, once you have updated it, you should [sync any existing deployments of the Binary Free App.](update-a-binary-free-app.md#sync-an-existing-deployment-of-a-binary-free-app-after-updating-it)
{% endhint %}

### Update a Binary Free App from the Notification Email

If you have email notifications enabled for a Binary Free App, whenever we update the version in our App Catalog you will receive an email notification similar to the [Example Binary Free App Update Email](../technical-references/cloud-email-reference/example-binary-free-app-update-email.md).

To update the version of a Binary Free App from the notification email:

1. Within the notification email, click **Update File**.

<figure><img src="../../.gitbook/assets/image-(401).png" alt="Clicking “Add Version” in the notification email" width="452"><figcaption></figcaption></figure>

2. If required, click **Sign In** on the new browser tab prompting you to sign in to your portal.

<figure><img src="../../.gitbook/assets/image-(402).png" alt="Clicking “Sign In” on the new browser tab prompting you to sign in to your portal." width="563"><figcaption></figcaption></figure>

3. Select the relevant account if you are already signed in or enter your credentials.\
   \
   The portal opens on the **“<**_**app\_name**_**>” Upload** file screen.

<figure><img src="../../.gitbook/assets/image (1105).png" alt="Portal opening on the “”<app_name>” Upload file” screen." width="563"><figcaption></figcaption></figure>

4. On the **Upload File Installer** screen, either:
   1. Click **Select Application File** and browse to the location containing the app’s installer.
   2. Drag and drop the installer file onto this page.

{% hint style="success" %}
**Tip**

We suggest you use the download link at the bottom of the page to ensure you download the latest version of the app from the vendor’s official website.
{% endhint %}

<figure><img src="../../.gitbook/assets/image-(404).png" alt="Clicking “Select Application File”" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If you select either the wrong file or the wrong version of the file, the [Unable to verify the file you are trying to upload. Please ensure you have uploaded the correct file](../troubleshoot/binary-free-apps/unable-to-verify-the-file-you-are-trying-to-upload-error-in-binary-free-apps.md) error will be displayed.

This is because we validate the hash of the installer to ensure you are uploading the correct file compared to the version information we have stored in our App Catalog.

If you really need to deploy an older version of the app, deploy it as a Custom App by using the [Create a Custom App](../custom-apps/create-a-custom-app/) process.
{% endhint %}

The hash for the file is calculated as the file is uploaded to your portal.

<figure><img src="../../.gitbook/assets/image-(405).png" alt="Calculating the hash for the file as its uploaded to your portal" width="563"><figcaption></figcaption></figure>

The portal also shows **File Up to Date** and the **Success – File Successfully Uploaded** notification once:

* The file has been uploaded successfully.
* The calculated hash matches that stored in our App Catalog.

<figure><img src="../../.gitbook/assets/image-(406).png" alt="“Success – File Successfully Uploaded” notification" width="563"><figcaption></figcaption></figure>

You can now click **Back** or navigate to another area of the portal.

### Update a Binary Free App from the App Catalog

Whenever a new version of a Binary Free App is available in the App Catalog and we don’t have the latest installer file, the upload (![](../../.gitbook/assets/image-\(407\).png)) icon appears beside the app.

<figure><img src="../../.gitbook/assets/image-(408).png" alt="“Upload” icon showing a new version of an app needs to be uploaded" width="563"><figcaption></figcaption></figure>

To update a Binary Free App from the App Catalog:

1. Click the upload (![](../../.gitbook/assets/image-\(407\).png)) icon.
2. On the app’s properties screen, click **Manage Files**.

<figure><img src="../../.gitbook/assets/image-(409).png" alt="Clicking “Manage Files”" width="563"><figcaption></figcaption></figure>

3. Continue from Step 8 of the [Upload the app installer](deploy-a-binary-free-app.md#upload-the-app-installer) section of the [Create a Binary Free App](deploy-a-binary-free-app.md) process to upload the latest version.

### Sync an Existing Deployment of a Binary Free App after Updating it

Once you have updated a Binary Free App, you can either:

* Wait for the next Sync Schedule to run as detailed in [Manage the Sync Schedule in Cloud](../manage/settings/sync-schedule.md).
* Manually initiate a sync as detailed in [Sync Now" Cloud feature](../deployments/manage-deployments/updates/sync-now.md).

# Deploy a Binary Free App

_Applies to: Binary Free Apps for Patch My PC Cloud_

There are two stages to deploying a Patch My PC (PMPC) Cloud Binary Free App:

* [Upload the app installer](deploy-a-binary-free-app.md#upload-the-app-installer)
* [Deploy the Binary Free app](deploy-a-binary-free-app.md#deploy-the-binary-free-app)

### Upload the app installer

To upload the app installer for the Binary Free App:

1. Download the relevant version of the software from the vendor for the app you wish to deploy.
2. Login to our portal.
3.  Search for the app in the **App Catalog**.\


    ![Searching for the app in the App Catalog](/_images/image-(443).png "Searching for the app in the App Catalog")


4.  Click the app to open its properties.\


    ![Clicking the app to open its properties](/_images/image-(444).png "Clicking the app to open its properties")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Notice that both the **Deploy** and **Edit Deployment** options are unavailable as this is a Binary Free App that requires you to upload the installer.</p>
</blockquote>

5.  Click **Manage Files**.\


    ![Clicking "Manage Files"](/_images/image-(445).png "Clicking “Manage Files”")
6.  On the **“<**_**app\_name**_**>” Upload file** screen, click **Add App File**.\


    ![Clicking "Add App File"](/_images/image-(446).png "Clicking “Add App File”")


7.  On the **General Information** tab, configure the required options for the app, then click **Next**.\


    ![Configuring any required options for the app, then clicking "Next"](/_images/image-(447).png "Configuring any required options for the app, then clicking “Next”")


8.  On the **Upload File Installer** tab, either:\
    \
    a. Click **Select Application File** and browse to the location containing the app’s installer.

    b. Drag and drop the installer file onto this page.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>We suggest you use the download link at the bottom of the page to ensure you download the latest version of the app from the vendor’s official website.</p>
</blockquote>

![Clicking "Select Application File"](/_images/image-(448).png "Clicking “Select Application File”")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you select either the wrong file or the wrong version of the file, the [Unable to verify the file you are trying to upload. Please ensure you have uploaded the correct file](../cloud-troubleshooting/troubleshooting-binary-free-apps/unable-to-verify-the-file-you-are-trying-to-upload-error-in-binary-free-apps.md) error will be displayed.</p>
<p>This is because we validate the hash of the installer to ensure you are uploading the correct file compared to the version information we have stored in our App Catalog.</p>
<p>If you really need to deploy an older version of the app, deploy it as a Custom App by using the [Create a Custom App](../custom-apps/create-a-custom-app/)  process.</p>
</blockquote>

The hash for the file is calculated as the file is uploaded to your portal.

![Calculating the hash for the file as its uploaded to your portal.](/_images/image-(2049).png "Calculating the hash for the file as its uploaded to your portal.")

The portal also shows **File Up to Date** and the **Success – File Successfully Uploaded** notification once:

* The file has been uploaded successfully.
*   The calculated hash matches that stored in our App Catalog.\


    !["Success – File Successfully Uploaded" notification](/_images/image-(2050).png "“Success – File Successfully Uploaded” notification")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>By default, whenever a new version of a Binary Free App is released, we update the version in our App Catalog, which will trigger an update notification to be sent to all users configured in your portal.</p>
<p>See the [Manage New Version Notifications for a Binary Free App](manage-new-version-notifications-for-a-binary-free-app.md) process to change this.</p>
</blockquote>

### Deploy the Binary Free app

Once the app installer for the Binary Free App has been successfully uploaded, follow the [Deploy an App](../cloud-deployments/deploying-an-app-using-cloud/) process to deploy the app.
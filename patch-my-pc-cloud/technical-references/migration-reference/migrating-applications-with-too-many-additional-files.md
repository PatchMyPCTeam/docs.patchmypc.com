# Migrating applications with too many additional files

Applications that contain more than 1,000 files cannot currently be migrated using the [Migration](../../migration/) feature due to technical limitations.

We are actively working to improve this experience. In the meantime, you can use the workaround below to successfully migrate these applications.

<figure><img src="../../../.gitbook/assets/image (4293).png" alt=""><figcaption></figcaption></figure>

**Workaround**

1. **Create a Copy of the Application**

In the **ConfigMgr Console**, create a copy of the application:

* Right-click the application
* Select **Copy**

Optionally, rename the Deployment Type to clearly indicate that it is the copied version. This name will be visible in the Cloud Portal.

<figure><img src="../../../.gitbook/assets/image (4294).png" alt=""><figcaption></figcaption></figure>

2. **Create a copy of the Source Content**

Navigate to the application’s source content and create a duplicate of the folder.

<figure><img src="../../../.gitbook/assets/image (4292).png" alt=""><figcaption></figcaption></figure>

3. **Zip files to reduce the file count**

In the copied content folder:

* Compress (zip) additional files
* Keep only the primary installer unzipped

{% hint style="info" %}
**NOTES**

* Do not zip the primary installer.
* If using PSADT, do not zip:
  * The PSADT modules
  * The primary installer referenced in the toolkit

This ensures the installer can still be scanned and hashed, which is required for catalog matching.
{% endhint %}

Example:

<figure><img src="../../../.gitbook/assets/image (4295).png" alt=""><figcaption></figcaption></figure>

4. **Update the Deployment Type's content**

In the copied application:

* Edit and update the Content path in the Deployment Type to point to the copied content folder
* Once done, save your changes, right-click on your Deployment Type, and update the content to create a new revision of the app

5. **Refresh Migration Data**

From the Cloud Portal, [Refresh the Migration Data](../../migration/refresh-migration-data.md).

Once the refresh is complete, the application should now be available for migration.

<figure><img src="../../../.gitbook/assets/image (4297).png" alt=""><figcaption></figcaption></figure>

6. **Add Pre-Script During Migration**

When migrating the application, add [this](https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Install/Pre-Install/Extract%20Zip) as a **pre-script** to extract the zipped files before installation.

{% hint style="info" %}
If you already have a pre-script configured, update it to include both:

* The extraction logic for the zipped files (should be first)
* Your existing script logic (after the extraction logic)

Make sure both sets of actions are combined into a single script so they run together during deployment.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (4298).png" alt=""><figcaption></figcaption></figure>

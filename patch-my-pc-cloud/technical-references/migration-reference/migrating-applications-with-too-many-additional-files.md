# Migrating applications with too many additional files

Applications that contain more than 1,000 files cannot currently be migrated using the [Migration](../../migration/) feature due to technical limitations.

We are actively working to improve this experience. In the meantime, you can use the workaround below to successfully migrate these applications.

![](/_images/image-(4293).png)

**Workaround**

1. **Create a Copy of the Application**

In the **ConfigMgr Console**, create a copy of the application:

* Right-click the application
* Select **Copy**

Optionally, rename the Deployment Type to clearly indicate that it is the copied version. This name will be visible in the Cloud Portal.

![](/_images/image-(4294).png)

2. **Create a copy of the Source Content**

Navigate to the application’s source content and create a duplicate of the folder.

![](/_images/image-(4292).png)

3. **Zip files to reduce the file count**

In the copied content folder:

* Compress (zip) additional files
* Keep only the primary installer unzipped

<blockquote class="wp-block-quote">
<p>**NOTES**</p>
<p>* Do not zip the primary installer.&#x20;</p>
<p>* If using PSADT, do not zip:</p>
<p>* The PSADT modules</p>
<p>* The primary installer referenced in the toolkit</p>
<p>This ensures the installer can still be scanned and hashed, which is required for catalog matching.</p>
</blockquote>

Example:

![](/_images/image-(4296).png)

4. **Update the Deployment Type's content**

In the copied application:

* Edit and update the Content path in the Deployment Type to point to the copied content folder
* Once done, save your changes, right-click on your Deployment Type, and update the content to create a new revision of the app

5. **Refresh Migration Data**

From the Cloud Portal, [Refresh the Migration Data](../../migration/refresh-migration-data.md).

Once the refresh is complete, the application should now be available for migration.

![](/_images/image-(4297).png)

6. **Add Pre-Script During Migration**

When migrating the application, add [this](https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Install/Pre-Install/Extract%20Zip) as a **pre-script** to extract the zipped files before installation.

<blockquote class="wp-block-quote">
<p>If you already have a pre-script configured, update it to include both:</p>
<p>* The extraction logic for the zipped files (should be first)&#x20;</p>
<p>* Your existing script logic (after the extraction logic)</p>
<p>Make sure both sets of actions are combined into a single script so they run together during deployment.</p>
</blockquote>

![](/_images/image-(4298).png)
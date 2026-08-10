# Publish the App Migrated from ConfigMgr in Intune as a Patch My PC Custom App

_Applies to: Patch My PC Cloud_

Configuration Manager (ConfigMgr) applications that can be migrated to Patch My PC (PMPC) Cloud and deployed as one of our Custom Apps have a **Match Type** of **Custom App**.

Once you click **Migrate** to migrate a ConfigMgr application to a PMPC Custom App, the Custom Apps Deployment Wizard starts, and you can follow [Create a Custom App](../../custom-apps/create-a-custom-app/), but please note the following:

* As a double-check, verify that the information on each tab is correct before clicking **Next**.
* On the **General Information** tab, ensure the **Version** and **Apps & Features Name** fields are completed. These are required to complete the deployment wizard and are also important if you choose to switch from custom detection rules carried over from ConfigMgr to the PMPC detection rule on the **Detection Rules** tab.
* On the **Configurations** tab, under the **Install Parameters** tool/section, check that the **Additional Argument** field is correct and includes any required additional arguments/command line options. If the application's primary installer file is a .MSI, we automatically extract it and populate the **Conflicting processes** field on this tab.
* On the **Assignments** tab, you can click **ConfigMgr Assignment List** to see a list of the current assignments in ConfigMgr, so you can then review this and set these up in Intune accordingly.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you don’t want to deploy this app now, click **Install App** under **App Without Assignments** on the **Assignments** tab, then click **Migrate** to create the app in Intune only. When you are ready to assign the app, you can [edit the deployment](../../deployments/manage-deployments/edit.md) and add the required assignment.</p>
</blockquote>

* On the **Detection Rules** tab, you can either continue with the **Use Custom** option, i.e. what we detected in ConfigMgr, or select the **Patch My PC Default (Recommended)** option instead.

When you click **Migrate**, the **Deployment Created, Migration Pending** notification is shown.

![Application migration status](/_images/image-(3678).png "Application migration status")

The **Status** field also updates to **In Progress** whilst the deployment is created, with any required content zipped (e.g., the primary installer file and any extra files) and sent to Azure Blob Storage.

You can also monitor the deployment progress by clicking the **Deployments** node and watching for the deployment status to change to **Success**.

![Deployment created for migrated application](/_images/image-(3679).png "Deployment created for migrated application")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>To see the migrated app in Intune, within the Microsoft Intune admin center navigate to:</p>
<p>**Home | Apps | Windows | Windows | Windows Apps | <**_**app\_name**_**>**</p>
</blockquote>

![Migrated application as seen in the Intune admin center](/_images/image-(3680).png "Migrated application as seen in the Intune admin center")
# Publish the App Migrated from ConfigMgr in Intune as a Patch My PC Catalog App

_Applies to: Patch My PC Cloud_

When migrating a Configuration Manager (ConfigMgr) application to a Patch My PC (PMPC) Catalog App, the deployment wizard starts, and you can follow [Deploying an App using Cloud](../../deployments/deploy-app/), but please note the following:

* Verify that the information on each tab is correct before clicking **Next**.
* On the **Configurations** tab, under the **Install Parameters** tool/section, check that the **Additional Argument** field is correct and includes any required additional arguments/command line options.
* On the **Assignments** tab, you can click **ConfigMgr Assignment List** to see a list of the current assignments in ConfigMgr, so you can then review this and set these up in Intune accordingly.

{% hint style="danger" %}
**Important**

We do not match ConfigMgr assignments to Entra ID groups. You need to manually configure your assignments during app deployment.
{% endhint %}

Once you have added your assignments, click **Migrate** and the **Deployment Created, Migration Pending** notification is shown.

<figure><img src="../../../.gitbook/assets/image (605).png" alt="Application migration status" width="563"><figcaption></figcaption></figure>

The **Status** field also updates to **In Progress** whilst the deployment is created, with any required content (such as extra files) being zipped and sent to Azure Blob Storage.

You can also monitor deployment progress by clicking the **Deployments** node and watching for the deployment **Status** to change to **Success**.

<figure><img src="../../../.gitbook/assets/image (3677).png" alt="Deployment created for migrated application" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

To see the migrated app in Intune, within the Microsoft Intune admin center navigate to:

**Home | Apps | Windows | Windows | Windows Apps | <**_**app\_name**_**>**
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (608).png" alt="Migrated application as seen in the Intune admin center" width="563"><figcaption></figcaption></figure>

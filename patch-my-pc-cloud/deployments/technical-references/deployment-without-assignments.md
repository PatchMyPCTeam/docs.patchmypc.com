# Create a Deployment without Assignments in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Some large organizations want to be able to create deployments in Intune Apps for Patch My PC (PMPC) Cloud without any assignments.

{% hint style="info" %}
**Note**

See [Understand Patch My PC Cloud Assignments](understand-assignments.md) for more details about assignments and how they work in PMPC Cloud.
{% endhint %}

Then, their local IT organization adds and manages the assignments to the relevant deployments to meet their needs by using Intune admin center.

To create a deployment with no assignments:

1. Follow the [Deploy an App](../deploy-app/) process until you reach the[ Assignments](../deploy-app/assignments-tab.md) tab where you can add an assignment.\
   \
   When you click **Add Assignment**, you will see the **App Without Assignment** sub-menu containing the following two items:

* **Install App -** Allows the Intune admin to add **Required**, **Available**, or **Uninstall** assignments from within the Intune admin center.
* **Update Only App -** Allows the Intune admin to add only an **Update Only** assignment from within the Intune admin center if the **Installer Type** is **.msp**.

<figure><img src="../../../.gitbook/assets/image (1060).png" alt="&#x27;App Without Assignment&#x27; sub-menu" width="223"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If you are deploying a Microsoft patch file (**.msp**), only the **Update Only App** option is shown under the **App Without Assignment** section as **.msp** files cannot be used to install an app, only update it.
{% endhint %}

{% hint style="success" %}
**Tip**

You can also [Add a Template](../../manage/settings/deployment-templates/add-template.md) with the **App Without Assignments** options configured. Then when you create the deployment, simply click **Apply Template** and select the relevant template to have its settings applied to this deployment.
{% endhint %}

2. Select the relevant option.

<figure><img src="../../../.gitbook/assets/image (3185).png" alt="Selecting the required option" width="563"><figcaption></figcaption></figure>

3. Uncheck the **Copy-Forward** checkbox if required.\
   \
   This checkbox is checked by default, which means that whenever we update the app, we remove all assignments from the previous version and add them to the new version.\
   \
   If the **Copy-Forward** checkbox is unchecked, we keep all assignments from the previous version.

{% hint style="info" %}
**Note**

The **Copy-Forward** checkbox also affects the behavior of assignments when you [recreate a deployment](../manage-deployments/recreate.md):

* If the **Copy-Forward** checkbox is checked, any existing assignments will be copied.
* If the **Copy-Forward** checkbox is unchecked, any existing assignments will be deleted.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3186).png" alt="&#x27;Copy-Forward&#x27; checkbox" width="563"><figcaption></figcaption></figure>

4. Click **Deploy** and wait for the deployment to complete successfully.

<figure><img src="../../../.gitbook/assets/image (3187).png" alt="Clicking &#x27;Deploy&#x27;" width="563"><figcaption></figcaption></figure>

Once the deployment has successfully completed, if you look in the Intune admin center you will see that the app has been created without any assignments.

<figure><img src="../../../.gitbook/assets/image (1064).png" alt="App created with no assignments" width="563"><figcaption></figcaption></figure>

Your local IT teams can now follow the [Assign apps to groups with Microsoft Intune](https://learn.microsoft.com/en-us/mem/intune/apps/apps-deploy) process to add the relevant assignments for this app.

{% hint style="info" %}
**Note**

If you checked the **Copy-Forward** checkbox, the next time the Sync Schedule detects a new version, the assignments are copied forward to the new version. The old version of the app will be removed immediately once the new version has been created and the assignments moved over to it.

Also, a deployment without assignments can be edited and managed in the same way as a regular deployment. See the [Manage Updates](../manage-deployments/updates/) and [Manage Deployments](../manage-deployments/) sections for more details.
{% endhint %}

{% hint style="danger" %}
**Important**

The current release of this feature has the following restrictions:

* A deployment cannot contain both regular assignment types and no assignment types.
* If you edit a deployment with no assignments, you cannot add a regular assignment type.
* If you have a regular deployment with update rings enabled, you cannot edit that deployment, disable update rings, remove all the assignments and then add a new no assignment type.
{% endhint %}

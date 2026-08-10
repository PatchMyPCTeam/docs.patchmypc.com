# Create a Deployment without Assignments in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Some large organizations want to be able to create deployments in Intune Apps for Patch My PC (PMPC) Cloud without any assignments.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Understand Patch My PC Cloud Assignments](understand-assignments.md) for more details about assignments and how they work in PMPC Cloud.</p>
</blockquote>

Then, their local IT organization adds and manages the assignments to the relevant deployments to meet their needs by using Intune admin center.

To create a deployment with no assignments:

1. Follow the [Deploy an App](../deploy-app/) process until you reach the[ Assignments](../deploy-app/assignments-tab.md) tab where you can add an assignment.\
   \
   When you click **Add Assignment**, you will see the **App Without Assignment** sub-menu containing the following two items:

* **Install App -** Allows the Intune admin to add **Required**, **Available**, or **Uninstall** assignments from within the Intune admin center.
* **Update Only App -** Allows the Intune admin to add only an **Update Only** assignment from within the Intune admin center if the **Installer Type** is **.msp**.

!['App Without Assignment' sub-menu](/_images/image-(1060).png "&#x27;App Without Assignment&#x27; sub-menu")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you are deploying a Microsoft patch file (**.msp**), only the **Update Only App** option is shown under the **App Without Assignment** section as **.msp** files cannot be used to install an app, only update it.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can also [Add a Template](../../manage/settings/deployment-templates/add-template.md) with the **App Without Assignments** options configured. Then when you create the deployment, simply click **Apply Template** and select the relevant template to have its settings applied to this deployment.</p>
</blockquote>

2. Select the relevant option.

![Selecting the required option](/_images/image-(3185).png "Selecting the required option")

3. Uncheck the **Copy-Forward** checkbox if required.\
   \
   This checkbox is checked by default, which means that whenever we update the app, we remove all assignments from the previous version and add them to the new version.\
   \
   If the **Copy-Forward** checkbox is unchecked, we keep all assignments from the previous version.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The **Copy-Forward** checkbox also affects the behavior of assignments when you [recreate a deployment](../manage-deployments/recreate.md):</p>
<p>* If the **Copy-Forward** checkbox is checked, any existing assignments will be copied.</p>
<p>* If the **Copy-Forward** checkbox is unchecked, any existing assignments will be deleted.</p>
</blockquote>

!['Copy-Forward' checkbox](/_images/image-(3186).png "&#x27;Copy-Forward&#x27; checkbox")

4. Click **Deploy** and wait for the deployment to complete successfully.

![Clicking 'Deploy'](/_images/image-(3187).png "Clicking &#x27;Deploy&#x27;")

Once the deployment has successfully completed, if you look in the Intune admin center you will see that the app has been created without any assignments.

![App created with no assignments](/_images/image-(1064).png "App created with no assignments")

Your local IT teams can now follow the [Assign apps to groups with Microsoft Intune](https://learn.microsoft.com/en-us/mem/intune/apps/apps-deploy) process to add the relevant assignments for this app.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you checked the **Copy-Forward** checkbox, the next time the Sync Schedule detects a new version, the assignments are copied forward to the new version. The old version of the app will be removed immediately once the new version has been created and the assignments moved over to it.</p>
<p>Also, a deployment without assignments can be edited and managed in the same way as a regular deployment. See the [Manage Updates](../manage-deployments/updates/) and [Manage Deployments](../manage-deployments/) sections for more details.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>The current release of this feature has the following restrictions:</p>
<p>* A deployment cannot contain both regular assignment types and no assignment types.</p>
<p>* If you edit a deployment with no assignments, you cannot add a regular assignment type.</p>
<p>* If you have a regular deployment with update rings enabled, you cannot edit that deployment, disable update rings, remove all the assignments and then add a new no assignment type.</p>
</blockquote>
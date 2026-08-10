# Recreate a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

Using Patch My PC (PMPC) Cloud, you can delete software from Intune and recreate it to retrigger the deployment on the targeted resources.

To recreate a deployment:

1.  From the **Deployments** page, click the ellipsis (**⋮**) beside the relevant deployment you want to recreate and click **Recreate**.<br>

    ![Clicking the ellipsis beside a deployment and selecting "Recreate"](/_images/image-(2715).png "Clicking the ellipsis beside a deployment and selecting “Recreate”")
2.  On the **Are you sure you want to recreate <**_**deployment\_name**_**>** dialog box, click **Yes**.<br>

    ![](/_images/image-(2383).png)

    \
    The **Status** of the deployment changes to **In Progress** and the **Recreating the deployment&#x20;**_**\<deployment\_name>**_**&#x20;has started** message is displayed.<br>

    ![Change to deployment status and message stating the recreation process has started](/_images/image-(2384).png "Change to deployment status and message stating the recreation process has started")

    \
    Once the deployment has been recreated, the portal auto-refreshes and the **Status** changes to **Success**.<br>

    ![Portal auto-refreshes to show the deployment has been successfully recreated](/_images/image-(2385).png "Portal auto-refreshes to show the deployment has been successfully recreated")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can also click **Recreate** on the property page of a deployment to recreate it.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If the deployment you are recreating has [Update Rings](../update-rings/) enabled, clicking **Recreate** will result in duplicate versions of the apps being created in Intune. Any existing assignments will be automatically moved from the old version to the new, recreated version.</p>
<p>Also, if the deployment you are recreating has [App Dependencies](../deploy-app/configurations-tab/additional-tools/dependencies.md), clicking **Recreate** creates a new app, creates any dependencies, deletes the dependencies for the old app, and finally deletes the old app from Intune.</p>
</blockquote>
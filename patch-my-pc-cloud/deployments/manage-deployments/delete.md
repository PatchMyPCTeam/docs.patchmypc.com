# Delete a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

To delete a deployment in Patch My PC (PMPC) Cloud:

1.  From the **Deployments** page, click the ellipsis (**⋮**) beside the relevant deployment you want to delete and click **Delete**.<br>

    ![Clicking the ellipsis beside a deployment and selecting "Delete"](/_images/image-(2386).png "Clicking the ellipsis beside a deployment and selecting “Delete”")


2.  On the **Are you sure you want to delete <**_**deployment\_name**_**>** dialog box, click **Yes**.<br>

    ![](/_images/image-(1571).png)



<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If the deployment you are deleting is for an app that another app is dependent on, the **Are you sure** dialog box will state which app has a dependency on this deployment and warn you that proceeding will delete this dependency, which could break the app dependent on this one.</p>
<p>!["Are you sure" prompt if other deployments have dependencies on this one](/_images/image-(2978 "\"Are you sure\" prompt if other deployments have dependencies on this one").png>)</p>
</blockquote>

The deployment is deleted and the **Success - Deployment&#x20;**_**\<deployment\_name>**_**&#x20;deleted** notification is displayed.

<blockquote class="wp-block-quote">
<p>**Warning**</p>
<p>Deleting a deployment will also delete the:</p>
<p>* latest and all old unassigned versions of this deployment if a [Retention Policy](../deploy-app/configurations-tab/additional-tools/retention-policy.md) has been configured.</p>
<p>* packaged win32 app from Intune.</p>
</blockquote>

![](/_images/image-(2387).png)

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can also click **Delete** on the property page of a deployment to delete it.</p>
</blockquote>
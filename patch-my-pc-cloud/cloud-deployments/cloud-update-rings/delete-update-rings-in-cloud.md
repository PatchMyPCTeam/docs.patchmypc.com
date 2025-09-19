# Delete Update Rings in Cloud

_Applies to: Patch My PC Cloud_

For a Patch My PC (PMPC) Cloud deployment with Update Rings enabled, you can either:

* [Delete all Update Rings](delete-update-rings-in-cloud.md#delete-all-update-rings)
* [Delete a Single Update Ring](delete-update-rings-in-cloud.md#delete-a-single-update-ring)

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>All deletion tasks for Update Rings are performed from the **Assignments** tab of the respective deployment.</p>
</blockquote>

### Delete all Update Rings

To delete all Update Rings for a deployment:

1. [Edit](../manage-cloud-deployments/edit-a-cloud-deployment.md) the relevant deployment and navigate to the **Assignments** tab.
2.  If you want to delete a single Update Ring, use the [Delete a Single Update Ring](delete-update-rings-in-cloud.md#delete-a-single-update-ring) process.\
    \
    To delete all Update Rings for this deployment, click **Remove all Rings**.\


    ![Clicking "Remove all Rings"](/_images/image-(2061Remove-all-Rings "Clicking \"Remove all Rings\"").png "Clicking “Remove all Rings”")


3.  On the **Move Assignments or Delete** dialog box, click **Move** to remove the Update Rings but keep all the existing assignments.\
    \


    ![Clicking "Move" to remove the Update Rings but keep all the existing assignments](/_images/image-(2062Move "Clicking \"Move\" to remove the Update Rings but keep all the existing assignments").png "Clicking “Move” to remove the Update Rings but keep all the existing assignments")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Clicking **Delete** will delete any existing assignments but not the deployment itself.</p>
<p>![Clicking "Delete" will delete any existing assignments, not the deployment itself.](/_images/image-(2064 "Clicking \"Delete\" will delete any existing assignments, not the deployment itself.").png>)\</p>
</blockquote>

The Update Rings are removed and any existing assignments are kept.

![Update Rings are removed and any existing assignments are kept](/_images/image-(2065 "Update Rings are removed and any existing assignments are kept").png "Update Rings are removed and any existing assignments are kept")

4.  Click **Save** to save your changes.\
    \


    ![Clicking "Save" to save changes](/_images/image-(2066Save "Clicking \"Save\" to save changes").png "Clicking “Save” to save changes")

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>As removing all Update Rings disables Update Ring functionality for this deployment (which could result in unintended results), the **"**_**\<deployment\_name>**_**" Deployment Summary** is shown detailing the impact of your proposed change.\</p>
<p>\</p>
<p>For example, this version of the app will be deployed immediately to all of the following assignments without any of the delays enforced by using Update Rings.</p>
<p>!["Deployment Summary" showing the impact of deleting all Update Rings ](/_images/image-(2067 "\"Deployment Summary\" showing the impact of deleting all Update Rings ").png>)</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If the existing deployment had different versions applied to different assignments, we use the version that was applied to the lowest delay ring before the deployment was edited.</p>
</blockquote>

5.  Click **Cancel** to return to the **Assignments** tab to make any required changes, or click **Confirm** to save your changes.\
    \
    The **Deployments** node is displayed along with the **Success – Edited <**_**deployment\_name**_**>** notification.\
    \


    !["Deployment Summary" showing the impact of delete all Update Rings](/_images/image-(2068Deployment-Summary "\"Deployment Summary\" showing the impact of delete all Update Rings").png "“Deployment Summary” showing the impact of delete all Update Rings")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you edit the deployment and click **More Info**, you will see the tabs representing the Update Rings are no longer present.</p>
</blockquote>

### Delete a Single Update Ring

To delete a Single Update Ring:

1. Navigate to the **Assignments** page of the deployment.
2. Click the red **X** beside the Update Ring you want to delete.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Deleting an Update Ring also deletes any assignments controlled by that ring. If you want to keep the assignment, drag and drop it to another ring before you delete the ring.</p>
</blockquote>

![Clicking the read "X" to delete a specific Update Ring](/_images/image-(2069X "Clicking the read \"X\" to delete a specific Update Ring").png "Clicking the read “X” to delete a specific Update Ring")

The ring and any assignments it contains are deleted.

![Update Ring deleted](/_images/image-(2070 "Update Ring deleted").png "Update Ring deleted")

3.  Click **Save** to save your changes.\
    \


    ![Clicking "Save" to save changes](/_images/image-(2071Save "Clicking \"Save\" to save changes").png "Clicking “Save” to save changes")

    \
    As you’ve removed an Update Ring and it’s assignments, the **"<**_**deployment\_name**_**>" Deployment Summary** is shown detailing the impact of your proposed change.\
    \
    For example, by deleting the **7-Zip Pilot +7 Days** ring, this app will not be deployed to the **03 - Patching - Production - All - 7 Days** Entra ID group.\
    \


    !["Deployment Summary" showing the impact of deleting this Update Rings](/_images/image-(2072Deployment-Summary "\"Deployment Summary\" showing the impact of deleting this Update Rings").png "“Deployment Summary” showing the impact of deleting this Update Rings")
4.  Click **Cancel** to return to the **Assignments** tab to make any required changes, or click **Confirm** to save your changes.\
    \
    The **Deployments** node is displayed along with the **Success – Edited <**_**deployment\_name**_**>** notification.\


    !["Deployment Summary" showing the impact of delete all Update Rings](/_images/image-(2073Deployment-Summary "\"Deployment Summary\" showing the impact of delete all Update Rings").png "“Deployment Summary” showing the impact of delete all Update Rings")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you edit the deployment and click **More Info**, you will see the tab representing the deleted Update Ring is no longer present.</p>
</blockquote>
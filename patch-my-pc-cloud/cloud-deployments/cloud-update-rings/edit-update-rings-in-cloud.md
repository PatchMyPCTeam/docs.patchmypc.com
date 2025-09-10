# Edit Update Rings in Cloud

_Applies to: Patch My PC Cloud_

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If a Patch My PC (PMPC) Cloud deployment is created with [Delayed Update Rings](how-cloud-update-rings-are-created.md#delayed-update-rings), you cannot edit it until all of the rings have been created. If you attempt to edit a deployment with incomplete  Update Rings you will see the [Error - Editing is not allowed until all rings are created after the configured delay](../../cloud-troubleshooting/troubleshooting-cloud-update-rings/error-editing-is-not-allowed-until-all-rings-are-created-after-the-configured-delay-cloud-error.md) message.</p>
<p>Also, if you make any changes to Return Codes for a deployment where Update Rings are enabled, these changes are only applied to the latest ring (newest version).</p>
</blockquote>

To edit the Update Rings configuration for a deployment:

1.  Navigate to the **Deployments** node.\


    ![Navigating to the “Deployments” node](/_images/image-(434 "Navigating to the “Deployments” node").png "Navigating to the “Deployments” node")


2. Click the relevant deployment whose Update Ring configuration you want to edit.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Click the filter button (![](/_images/image-(2513).png>)) and select the **Enabled** option under the **Update Rings** section, followed by **Apply Filters** to see just those deployments that have update Rings configured.&#x20;</p>
</blockquote>

![Clicking the relevant deployment you want to edit](/_images/image-(2060 "Clicking the relevant deployment you want to edit").png "Clicking the relevant deployment you want to edit")

3.  Click **Edit**.\


    ![Clicking “More Info”](/_images/image-(436 "Clicking “More Info”").png "Clicking “More Info”")


4.  Click the **Assignments** tab.\


    ![Clicking the “Assignments” tab](/_images/image-(437 "Clicking the “Assignments” tab").png "Clicking the “Assignments” tab")


5. Make any required changes, for example:&#x20;
   1. Move Assignments between rings using drag and drop
   2. Rename rings by clicking the pencil icon beside the relevant ring
   3. Modify the delay for a ring by clicking the minus (**-**) or plus (**+**)
   4. Add a ring by clicking **Add Update Rings**
   5. Delete a ring by clicking the red x after the delay.
6.  Click **Save** to save your changes.\


    ![Clicking “Save”](/_images/image-(438 "Clicking “Save”").png "Clicking “Save”")

    \
    If you make any changes that affect how the Update Rings will work, you will see the **“<**_**app\_name**_**>” Deployment Summary** asking you to either confirm or cancel your changes.\
    \
    For example, reducing the delay for **Corel All Users** ring from **3** days to **2** results in the following.\


    ![Example “Deployment Summary” showing the effects of the edit](/_images/image-(439 "Example “Deployment Summary” showing the effects of the edit").png "Example “Deployment Summary” showing the effects of the edit")


7.  Either click **Cancel** to return to the **Assignments** tab and make any required changes or click **Confirm** to save your changes.\
    \
    The **Deployments** node is redisplayed along with the **Success – Edited <**_**deployment\_name**_**>** notification.\


    ![](/_images/image-(440).png "")
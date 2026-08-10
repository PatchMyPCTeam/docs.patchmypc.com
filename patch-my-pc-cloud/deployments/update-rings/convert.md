# Convert an existing Patch My PC Cloud Deployment to use Update Rings

_Applies to: Patch My PC Cloud_

If you have already successfully deployed an app using Patch My PC (PMPC) Cloud, you can convert that deployment to use Update Rings.

To convert an existing deployment to use Update Rings:

1. [Edit the deployment](../manage-deployments/edit.md) and navigate to the **Assignments** tab.

![Navigating to the "Assignments" tab](/_images/image-(1151).png "Navigating to the “Assignments” tab")

Any existing assignments for the deployment are shown.

![Existing assignments](/_images/image-(1152).png "Existing assignments")

2. Click **Enable Update Rings**.

![Clicking "Enable Update Rings"](/_images/image-(1153).png "Clicking “Enable Update Rings”")

3. On the **Move Assignments or Delete** dialog box, click **Move** to create the Update Rings and move any existing assignments to the first Update Ring.

![Clicking "Move" to move any existing assignments to the first Update Ring.](/_images/image-(1154).png "Clicking “Move” to move any existing assignments to the first Update Ring.")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Clicking **Delete** will delete any existing assignments, not the deployment itself. It will also create the default two Update Rings with default settings.</p>
</blockquote>

Any existing assignments are moved into the first Update Ring.

![Any existing assignments are moved into the first Update Ring.](/_images/image-(2748).png "Any existing assignments are moved into the first Update Ring.")

4. Continue from Step 3 of the [Create Update Rings](create.md) process to configure your Update Rings. For example, adding additional assignments, moving assignments between rings, etc.
5. Once you have completed reconfiguring the deployment, click **Save**.

![Clicking "Save" to save changes](/_images/image-(1156).png "Clicking “Save” to save changes")

<blockquote class="wp-block-quote">
<p>**Warning**</p>
<p>When you convert an existing deployment to use Update Rings, the rings will be created with the **Immediate** option, i.e. immediately. As this is the expected behavior, it cannot be changed.</p>
</blockquote>
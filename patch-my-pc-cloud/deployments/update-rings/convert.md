# Convert an existing Patch My PC Cloud Deployment to use Update Rings

_Applies to: Patch My PC Cloud_

If you have already successfully deployed an app using Patch My PC (PMPC) Cloud, you can convert that deployment to use Update Rings.

To convert an existing deployment to use Update Rings:

1. [Edit the deployment](../manage-deployments/edit.md) and navigate to the **Assignments** tab.

![Navigating to the "Assignments" tab](../../../.gitbook/assets/image-\(1151\).png)

Any existing assignments for the deployment are shown.

![Existing assignments](../../../.gitbook/assets/image-\(1152\).png)

2. Click **Enable Update Rings**.

![Clicking "Enable Update Rings"](../../../.gitbook/assets/image-\(1153\).png)

3. On the **Move Assignments or Delete** dialog box, click **Move** to create the Update Rings and move any existing assignments to the first Update Ring.

![Clicking "Move" to move any existing assignments to the first Update Ring.](../../../.gitbook/assets/image-\(1154\).png)

> \*\*Note\*\*
>
> Clicking \*\*Delete\*\* will delete any existing assignments, not the deployment itself. It will also create the default two Update Rings with default settings.

Any existing assignments are moved into the first Update Ring.

![Any existing assignments are moved into the first Update Ring.](../../../.gitbook/assets/image-\(2748\).png)

4. Continue from Step 3 of the [Create Update Rings](create.md) process to configure your Update Rings. For example, adding additional assignments, moving assignments between rings, etc.
5. Once you have completed reconfiguring the deployment, click **Save**.

![Clicking "Save" to save changes](../../../.gitbook/assets/image-\(1156\).png)

> \*\*Warning\*\*
>
> When you convert an existing deployment to use Update Rings, the rings will be created with the \*\*Immediate\*\* option, i.e. immediately. As this is the expected behavior, it cannot be changed.

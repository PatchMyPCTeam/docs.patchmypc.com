# Create Update Rings in Cloud

_Applies to: Patch My PC Cloud_

To create Update Rings for a new Deployment in Patch My PC (PMPC) Cloud:

1. If you are unfamiliar with creating a deployment, follow the [Deploy an App](../deploying-an-app-using-cloud/) process until Step 7.
2.  On the **Assignments** page, click **Enable Update Rings**.\


    ![Clicking "Enable Update Rings](/_images/image-(2110Enable-Update-Rings "Clicking \"Enable Update Rings").png "Clicking “Enable Update Rings")
3. From the **Update ring start time** dropdown, choose how you want your Update Rings to handle the start times for their assignments:\
   • [Delayed](how-cloud-update-rings-are-created.md#delayed)\
   • [Immediate](how-cloud-update-rings-are-created.md#immediate)

![Choosing the Update Ring start time](/_images/image-(2582 "Choosing the Update Ring start time").png "Choosing the Update Ring start time")

By default, two Update Rings are created with a two-day delay between them.

![Default rings and their settings](/_images/image-(2583 "Default rings and their settings").png "Default rings and their settings")

4. If you do not want to add additional Update Rings, go to step 7.\
   \
   To add an additional Update Ring, click **Add Update Ring**.

![Clicking "Add Update Ring"](/_images/image-(2584Add-Update-Ring "Clicking \"Add Update Ring\"").png "Clicking “Add Update Ring”")

5. On the **Add Update Ring** dialog box, enter the name for the new ring in the **Name** field and click **Save**.

!["Add Update Ring" dialog box](/_images/image-(2187Add-Update-Ring "\"Add Update Ring\" dialog box").png "“Add Update Ring” dialog box")

A new ring is added.

![New ring added](/_images/image-(2585 "New ring added").png "New ring added")

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Whenever you add a new Update Ring, it is created with a default delay of **0** days, i.e. the deployment will be installed immediately on any targeted users/devices.</p>
<p>If you already have another ring with a default delay of 0 days, you will see the **Two rings cannot have the same delay value** message besides the second ring with the duplicate delay.</p>
<p>You should adjust the delays on your Update Rings to avoid duplicates.</p>
<p>Also, if your [Sync Schedule](../../cloud-administration/manage-the-sync-schedule-in-cloud.md) is configured for anything other than **Daily**, this will affect the delay you can configure between rings. For example, assuming you have your Sync Schedule configured for **Monthly**, when you add a new ring you will not be able to configure a delay between rings of less than 30 days as shown below.</p>
</blockquote>

6. Repeat step 4 to add any additional Update Rings.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You can add up to a maximum of 10 Update Rings per deployment.</p>
</blockquote>

7. If you do not want to change the names of any of the rings, go to Step 10.\
   \
   If you want to change the name of any of the rings, click the pencil icon (![pencil icon](/_images/image-(2039 "pencil icon").png>)) beside the relevant ring.

![Clicking the pencil icon beside the relevant ring to rename](/_images/image-(2591 "Clicking the pencil icon beside the relevant ring to rename").png "Clicking the pencil icon beside the relevant ring to rename")

8. Enter the ring's name in the **Name** field of the **Edit Update Ring** dialog box, then click **Save**.

![Entering the ring's name in the "Name" field of the "Edit Update Ring" dialog box and clicking "Save"](/_images/image-(2041Name "Entering the ring's name in the \"Name\" field of the \"Edit Update Ring\" dialog box and clicking \"Save\"").png "Entering the ring&#x27;s name in the “Name” field of the “Edit Update Ring” dialog box and clicking “Save”")

The updated name appears.

![Updated ring name](/_images/image-(2592 "Updated ring name").png "Updated ring name")

9. Change the name of any other rings.
10. If you do not want to change the delay for any of the rings, go to Step 11.\
    \
    If you want to change the delay for a ring, click the plus (**+**) or minus (**-**) sign beside the relevant rings.

![Clicking plus or minus beside the relevant rings](/_images/image-(2593 "Clicking plus or minus beside the relevant rings").png "Clicking plus or minus beside the relevant rings")

11. Click **Add Assignment** and add the relevant assignments for each ring, configuring the settings for each assignment as required.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See the [Assignments](../deploying-an-app-using-cloud/cloud-assignments-deployment-tab.md) section of the [Deploy an App](../deploying-an-app-using-cloud/) process for more information.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can drag assignments between Update Rings by clicking the double ellipsis (![](/_images/image-(2044).png)) beside the relevant assignment and dragging and dropping it to the relevant Update Ring.</p>
</blockquote>

![Assignments added and configured for each Update Ring](/_images/image-(2594 "Assignments added and configured for each Update Ring").png "Assignments added and configured for each Update Ring")

12. Click **Deploy**.

![Clicking "Deploy"](/_images/image-(2595Deploy "Clicking \"Deploy\"").png "Clicking “Deploy”")

The **“<**_**deployment\_name**_**>” Deployment Summary** dialog box appears, summarizing what you are deploying, to which groups, and when.

!["Deployment Summary"](/_images/image-(2135Deployment-Summary "\"Deployment Summary\"").png "“Deployment Summary”")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If your [Sync Schedule](../../cloud-administration/manage-the-sync-schedule-in-cloud.md) is set to anything other than **Daily**, the UI will warn you that some rings may not be evaluated as expected.&#x20;</p>
<p>![](/_images/image-(2138).png>)</p>
<p>This is why we recommend you set your [Sync Schedule](../../cloud-administration/manage-the-sync-schedule-in-cloud.md) to **Daily** if you plan to use Update Rings.</p>
</blockquote>

13. Either click :\
    \
    a. **Cancel** to return to the **Assignments** tab to make any changes (after which you need to click **Deploy**).\
    \
    b. Click **Confirm** to continue.

![Clicking "Confirm"](/_images/image-(2140Confirm "Clicking \"Confirm\"").png "Clicking &#x22;Confirm&#x22;")

When you click **Confirm**, the **Deployments** node appears showing the deployment as **In Progress** and the **Success – Created <**_**deployment\_name**_**>** notification.

![](/_images/image-(2142).png "")
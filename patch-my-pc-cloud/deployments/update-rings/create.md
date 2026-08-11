# Create Update Rings in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

To create Update Rings for a new Deployment in Patch My PC (PMPC) Cloud:

1. If you are unfamiliar with creating a deployment, follow the [Deploy an App](../deploy-app/) process until Step 7.
2.  On the **Assignments** page, click **Enable Update Rings**.<br>

    ![Clicking "Enable Update Rings](/_images/image-(2812).png)
3. From the **Update ring start time** dropdown, choose how you want your Update Rings to handle the start times for their assignments:\
   • [Delayed](update-ring-types.md#delayed)\
   • [Immediate](update-ring-types.md#immediate)

![Choosing the Update Ring start time](/_images/image-(3284).png)

By default, two Update Rings are created with a two-day delay between them.

![Default rings and their settings](/_images/image-(3285).png)

4. If you do not want to add additional Update Rings, go to step 7.\
   \
   To add an additional Update Ring, click **Add Update Ring**.

![Clicking "Add Update Ring"](/_images/image-(3286).png)

5. On the **Add Update Ring** dialog box, enter the name for the new ring in the **Name** field and click **Save**.

!["Add Update Ring" dialog box](/_images/image-(2889).png)

A new ring is added.

![New ring added](/_images/image-(3287).png)

> \*\*Important\*\*
>
> Whenever you add a new Update Ring, it is created with a default delay of \*\*0\*\* days, i.e. the deployment will be installed immediately on any targeted users/devices.
>
> If you already have another ring with a default delay of 0 days, you will see the \*\*Two rings cannot have the same delay value\*\* message besides the second ring with the duplicate delay.
>
> You should adjust the delays on your Update Rings to avoid duplicates.
>
> Also, if your \[Sync Schedule]\(../../manage/settings/sync-schedule.md) is configured for anything other than \*\*Daily\*\*, this will affect the delay you can configure between rings. For example, assuming you have your Sync Schedule configured for \*\*Monthly\*\*, when you add a new ring you will not be able to configure a delay between rings of less than 30 days as shown below.

6. Repeat step 4 to add any additional Update Rings.

> \*\*Note\*\*
>
> You can add up to a maximum of 10 Update Rings per deployment.

7. If you do not want to change the names of any of the rings, go to Step 10.\
   \
   If you want to change the name of any of the rings, click the pencil icon (!\[pencil icon]\(/\_images/image-(2741 "pencil icon").png>)) beside the relevant ring.

![Clicking the pencil icon beside the relevant ring to rename](/_images/image-(3293).png)

8. Enter the ring's name in the **Name** field of the **Edit Update Ring** dialog box, then click **Save**.

![Entering the ring's name in the "Name" field of the "Edit Update Ring" dialog box and clicking "Save"](/_images/image-(2743).png)

The updated name appears.

![Updated ring name](/_images/image-(3294).png)

9. Change the name of any other rings.
10. If you do not want to change the delay for any of the rings, go to Step 11.\
    \
    If you want to change the delay for a ring, click the plus (**+**) or minus (**-**) sign beside the relevant rings.

![Clicking plus or minus beside the relevant rings](/_images/image-(3295).png)

11. Click **Add Assignment** and add the relevant assignments for each ring, configuring the settings for each assignment as required.

> \*\*Note\*\*
>
> See the \[Assignments]\(../deploy-app/assignments-tab.md) section of the \[Deploy an App]\(../deploy-app/) process for more information.

> \*\*Tip\*\*
>
> You can drag assignments between Update Rings by clicking the double ellipsis (!\[]\(/\_images/image-(2746).png)) beside the relevant assignment and dragging and dropping it to the relevant Update Ring.

![Assignments added and configured for each Update Ring](/_images/image-(3296).png)

12. Click **Deploy**.

![Clicking "Deploy"](/_images/image-(3297).png)

The **“<**_**deployment\_name**_**>” Deployment Summary** dialog box appears, summarizing what you are deploying, to which groups, and when.

!["Deployment Summary"](/_images/image-(2837).png)

> \*\*Note\*\*
>
> If your \[Sync Schedule]\(../../manage/settings/sync-schedule.md) is set to anything other than \*\*Daily\*\*, the UI will warn you that some rings may not be evaluated as expected.
>
> !\[]\(/\_images/image-(2840).png>)
>
> This is why we recommend you set your \[Sync Schedule]\(../../manage/settings/sync-schedule.md) to \*\*Daily\*\* if you plan to use Update Rings.

13. Either click :\
    \
    a. **Cancel** to return to the **Assignments** tab to make any changes (after which you need to click **Deploy**).\
    \
    b. Click **Confirm** to continue.

![Clicking "Confirm"](/_images/image-(2842).png)

When you click **Confirm**, the **Deployments** node appears showing the deployment as **In Progress** and the **Success – Created <**_**deployment\_name**_**>** notification.

![](/_images/image-(2844).png)
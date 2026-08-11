# Create Update Rings in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

To create Update Rings for a new Deployment in Patch My PC (PMPC) Cloud:

1. If you are unfamiliar with creating a deployment, follow the [Deploy an App](../deploy-app/) process until Step 7.
2.  On the **Assignments** page, click **Enable Update Rings**.<br>

    <figure><img src="../../../.gitbook/assets/image (2812).png" alt="Clicking “Enable Update Rings" width="563"><figcaption></figcaption></figure>
3. From the **Update ring start time** dropdown, choose how you want your Update Rings to handle the start times for their assignments:\
   • [Delayed](update-ring-types.md#delayed)\
   • [Immediate](update-ring-types.md#immediate)

<figure><img src="../../../.gitbook/assets/image (3284).png" alt="Choosing the Update Ring start time " width="563"><figcaption></figcaption></figure>

By default, two Update Rings are created with a two-day delay between them.

<figure><img src="../../../.gitbook/assets/image (3285).png" alt="Default rings and their settings" width="563"><figcaption></figcaption></figure>

4. If you do not want to add additional Update Rings, go to step 7.\
   \
   To add an additional Update Ring, click **Add Update Ring**.

<figure><img src="../../../.gitbook/assets/image (3286).png" alt="Clicking “Add Update Ring”" width="563"><figcaption></figcaption></figure>

5. On the **Add Update Ring** dialog box, enter the name for the new ring in the **Name** field and click **Save**.

<figure><img src="../../../.gitbook/assets/image (2889).png" alt="“Add Update Ring” dialog box" width="336"><figcaption></figcaption></figure>

A new ring is added.

<figure><img src="../../../.gitbook/assets/image (3287).png" alt="New ring added" width="563"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

Whenever you add a new Update Ring, it is created with a default delay of **0** days, i.e. the deployment will be installed immediately on any targeted users/devices.

If you already have another ring with a default delay of 0 days, you will see the **Two rings cannot have the same delay value** message besides the second ring with the duplicate delay.

You should adjust the delays on your Update Rings to avoid duplicates.

Also, if your [Sync Schedule](../../manage/settings/sync-schedule.md) is configured for anything other than **Daily**, this will affect the delay you can configure between rings. For example, assuming you have your Sync Schedule configured for **Monthly**, when you add a new ring you will not be able to configure a delay between rings of less than 30 days as shown below.
{% endhint %}

6. Repeat step 4 to add any additional Update Rings.

{% hint style="info" %}
**Note**

You can add up to a maximum of 10 Update Rings per deployment.
{% endhint %}

7. If you do not want to change the names of any of the rings, go to Step 10.\
   \
   If you want to change the name of any of the rings, click the pencil icon (![pencil icon](<../../../.gitbook/assets/image (2741).png>)) beside the relevant ring.

<figure><img src="../../../.gitbook/assets/image (3293).png" alt="Clicking the pencil icon beside the relevant ring to rename" width="563"><figcaption></figcaption></figure>

8. Enter the ring's name in the **Name** field of the **Edit Update Ring** dialog box, then click **Save**.

<figure><img src="../../../.gitbook/assets/image (2743).png" alt="Entering the ring&#x27;s name in the “Name” field of the “Edit Update Ring” dialog box and clicking “Save”" width="336"><figcaption></figcaption></figure>

The updated name appears.

<figure><img src="../../../.gitbook/assets/image (3294).png" alt="Updated ring name" width="563"><figcaption></figcaption></figure>

9. Change the name of any other rings.
10. If you do not want to change the delay for any of the rings, go to Step 11.\
    \
    If you want to change the delay for a ring, click the plus (**+**) or minus (**-**) sign beside the relevant rings.

<figure><img src="../../../.gitbook/assets/image (3295).png" alt="Clicking plus or minus beside the relevant rings" width="563"><figcaption></figcaption></figure>

11. Click **Add Assignment** and add the relevant assignments for each ring, configuring the settings for each assignment as required.

{% hint style="info" %}
**Note**

See the [Assignments](../deploy-app/assignments-tab.md) section of the [Deploy an App](../deploy-app/) process for more information.
{% endhint %}

{% hint style="success" %}
**Tip**

You can drag assignments between Update Rings by clicking the double ellipsis (<img src="../../../.gitbook/assets/image (2746).png" alt="double ellipsis" data-size="line">) beside the relevant assignment and dragging and dropping it to the relevant Update Ring.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3296).png" alt="Assignments added and configured for each Update Ring" width="563"><figcaption></figcaption></figure>

12. Click **Deploy**.

<figure><img src="../../../.gitbook/assets/image (3297).png" alt="Clicking “Deploy”" width="563"><figcaption></figcaption></figure>

The **“<**_**deployment\_name**_**>” Deployment Summary** dialog box appears, summarizing what you are deploying, to which groups, and when.

<figure><img src="../../../.gitbook/assets/image (2837).png" alt="“Deployment Summary”"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If your [Sync Schedule](../../manage/settings/sync-schedule.md) is set to anything other than **Daily**, the UI will warn you that some rings may not be evaluated as expected.&#x20;

![](<../../../.gitbook/assets/image (2840).png>)

This is why we recommend you set your [Sync Schedule](../../manage/settings/sync-schedule.md) to **Daily** if you plan to use Update Rings.
{% endhint %}

13. Either click :\
    \
    a. **Cancel** to return to the **Assignments** tab to make any changes (after which you need to click **Deploy**).\
    \
    b. Click **Confirm** to continue.

<figure><img src="../../../.gitbook/assets/image (2842).png" alt="Clicking &#x22;Confirm&#x22;"><figcaption></figcaption></figure>

When you click **Confirm**, the **Deployments** node appears showing the deployment as **In Progress** and the **Success – Created <**_**deployment\_name**_**>** notification.

<figure><img src="../../../.gitbook/assets/image (2844).png" alt="“Deployments” node appearing showing the deployment as “In Progress” and the “Success – Created <deployment_name>” notification. "><figcaption></figcaption></figure>

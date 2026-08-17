# Delete an Update Ring in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

For a Patch My PC (PMPC) Cloud deployment with Update Rings enabled, you can either:

* [Delete all Update Rings](delete.md#delete-all-update-rings)
* [Delete a Single Update Ring](delete.md#delete-a-single-update-ring)

{% hint style="info" %}
**Note**

All deletion tasks for Update Rings are performed from the **Assignments** tab of the respective deployment.
{% endhint %}

## Delete all Update Rings

To delete all Update Rings for a deployment:

1. [Edit](../manage-deployments/edit.md) the relevant deployment and navigate to the **Assignments** tab.
2.  If you want to delete a single Update Ring, use the [Delete a Single Update Ring](delete.md#delete-a-single-update-ring) process.\
    \
    To delete all Update Rings for this deployment, click **Remove all Rings**.<br>

    <figure><img src="../../../.gitbook/assets/image (2763).png" alt="Clicking “Remove all Rings”"><figcaption></figcaption></figure>
3.  On the **Move Assignments or Delete** dialog box, click **Move** to remove the Update Rings but keep all the existing assignments.\
    <br>

    <figure><img src="../../../.gitbook/assets/image (1154).png" alt="Clicking “Move” to remove the Update Rings but keep all the existing assignments" width="300"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Clicking **Delete** will delete any existing assignments but not the deployment itself.

![Clicking “Delete” will delete any existing assignments, not the deployment itself.](<../../../.gitbook/assets/image (2765).png>)<br>
{% endhint %}

The Update Rings are removed and any existing assignments are kept.

<figure><img src="../../../.gitbook/assets/image (2767).png" alt="Update Rings are removed and any existing assignments are kept"><figcaption></figcaption></figure>

4.  Click **Save** to save your changes.\
    <br>

    <figure><img src="../../../.gitbook/assets/image (2768).png" alt="Clicking “Save” to save changes"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

As removing all Update Rings disables Update Ring functionality for this deployment (which could result in unintended results), the **"**_**\<deployment\_name>**_**" Deployment Summary** is shown detailing the impact of your proposed change.\
\
For example, this version of the app will be deployed immediately to all of the following assignments without any of the delays enforced by using Update Rings.

<img src="../../../.gitbook/assets/image (2769).png" alt="“Deployment Summary” showing the impact of deleting all Update Rings" data-size="original">
{% endhint %}

{% hint style="info" %}
**Note**

If the existing deployment had different versions applied to different assignments, we use the version that was applied to the lowest delay ring before the deployment was edited.
{% endhint %}

5.  Click **Cancel** to return to the **Assignments** tab to make any required changes, or click **Confirm** to save your changes.\
    \
    The **Deployments** node is displayed along with the **Success – Edited <**_**deployment\_name**_**>** notification.<br>

    <figure><img src="../../../.gitbook/assets/image (2770).png" alt="“Deployment Summary” showing the impact of delete all Update Rings"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

If you edit the deployment and click **More Info**, you will see the tabs representing the Update Rings are no longer present.
{% endhint %}

## Delete a Single Update Ring

To delete a Single Update Ring:

1. Navigate to the **Assignments** page of the deployment.
2. Click the red **X** beside the Update Ring you want to delete.

{% hint style="info" %}
**Note**

Deleting an Update Ring also deletes any assignments controlled by that ring. If you want to keep the assignment, drag and drop it to another ring before you delete the ring.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (2771).png" alt="Clicking the read “X” to delete a specific Update Ring"><figcaption></figcaption></figure>

The ring and any assignments it contains are deleted.

<figure><img src="../../../.gitbook/assets/image (2772).png" alt="Update Ring deleted"><figcaption></figcaption></figure>

3.  Click **Save** to save your changes.\
    <br>

    <figure><img src="../../../.gitbook/assets/image (2773).png" alt="Clicking “Save” to save changes"><figcaption></figcaption></figure>

    \
    As you’ve removed an Update Ring and it’s assignments, the **"<**_**deployment\_name**_**>" Deployment Summary** is shown detailing the impact of your proposed change.\
    \
    For example, by deleting the **7-Zip Pilot +7 Days** ring, this app will not be deployed to the **03 - Patching - Production - All - 7 Days** Entra ID group.\
    <br>

    <figure><img src="../../../.gitbook/assets/image (2774).png" alt="“Deployment Summary” showing the impact of deleting this Update Rings"><figcaption></figcaption></figure>
4.  Click **Cancel** to return to the **Assignments** tab to make any required changes, or click **Confirm** to save your changes.\
    \
    The **Deployments** node is displayed along with the **Success – Edited <**_**deployment\_name**_**>** notification.<br>

    <figure><img src="../../../.gitbook/assets/image (2775).png" alt="“Deployment Summary” showing the impact of delete all Update Rings"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

If you edit the deployment and click **More Info**, you will see the tab representing the deleted Update Ring is no longer present.
{% endhint %}

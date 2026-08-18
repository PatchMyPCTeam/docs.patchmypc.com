# Bulk Actions for Patch My PC Cloud Deployments

_Applies to: Patch My PC (PMPC) Cloud_

{% hint style="danger" %}
**Public Preview**

This documentation is for a pre-release feature still under development and therefore incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

The _Bulk Actions_ functionality of Patch My PC (PMPC) Cloud allows you to select multiple deployments to perform a management action on, versus having to repeat the same action on each deployment individually.

To use _Bulk Actions_:

{% stepper %}
{% step %}
### **Navigate to Deployments**

Navigate to the **Deployments** node of the Cloud Portal.
{% endstep %}

{% step %}
### Either select all or a subset

Either select all or [select a subset](bulk-actions.md#select-a-subset)

Click the select all checkbox in the top-left corner to select all of the deployments on the current page.

<figure><img src="../../../.gitbook/assets/image (364).png" alt="Clicking the select all checkbox" width="563"><figcaption></figcaption></figure>

All deployments on the current page are now selected (unchecking the select all checkbox unchecks all deployments on the current page).

{% hint style="danger" %}
**Important**

The select all option does not work with deployments with a **Status** of **In Progress.** You also cannot manually select a deployment that is **In Progress**.
{% endhint %}

{% hint style="success" %}
**Tip**

If your list of deployments spans multiple pages, you can navigate to the next page and click the select all checkbox to select all deployments on that page as well. You can repeat this process to select all of your deployments.
{% endhint %}
{% endstep %}

{% step %}
### Select a subset

To select a subset of deployments, click the checkbox beside all of the deployments you wish to perform an action on.

<figure><img src="../../../.gitbook/assets/image (406).png" alt="Clicking the checkbox beside the required deployments" width="563"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Perform the required bulk action

Notice that regardless of which option you use, the number of selected deployments appears beside the **Search** box, along with the bulk actions toolbar of actions you can perform on the selected deployments.

<figure><img src="../../../.gitbook/assets/image (545).png" alt="Number of selected deployments and bulk actions toolbar" width="563"><figcaption></figcaption></figure>

At this point, you can perform the following actions on all of the selected deployments:

* [Resume paused deployments](bulk-actions.md#resume-paused-deployments)
* [Pause deployments from updating](bulk-actions.md#pause-deployments-from-updating)
* [Recreate selected deployments](bulk-actions.md#recreate-selected-deployments)
* [Sync selected deployments now](bulk-actions.md#sync-selected-deployments-now)
* [Delete the selected deployments](bulk-actions.md#delete-selected-deployments)
{% endstep %}
{% endstepper %}

## Resume paused deployments

If the _Pause Updates_ feature of PMPC Cloud has been configured for an app that has since been updated, and you want to bring the app up to date to the latest version, you need to disable pause updates by resuming updates to the deployment.

{% hint style="info" %}
**Note**

You can only resume updates for deployments that have already been paused.
{% endhint %}

When you click the Resume Updates button (![Resume Updates button](<../../../.gitbook/assets/image (554).png>)), the **Resume Updates Deployments** dialog appears, warning you that you are about to resume updates for the number of deployments you selected, and that new versions of the apps within these deployments will be deployed according to the configuration of each individual deployment.

{% hint style="info" %}
**Note**

If you select a deployment that has not already been paused along with a deployment(s) that has, only the paused deployment is resumed.
{% endhint %}

Click **Confirm** to continue.

<figure><img src="../../../.gitbook/assets/image (563).png" alt="‘Resume Updates’" width="410"><figcaption></figcaption></figure>

&#x20;The **Resume Updates in Progress** dialog is shown for each deployment as it is resumed.

<figure><img src="../../../.gitbook/assets/image (564).png" alt="‘Resume Updates in Progress’ dialog" width="440"><figcaption></figcaption></figure>

Once all of the deployments have been resumed, the **Resume Updates Completed** dialog is shown, which you can close by clicking **Close**.

<figure><img src="../../../.gitbook/assets/image (566).png" alt="‘Resume Updates Completed’ dialog" width="411"><figcaption></figcaption></figure>

The **Deployments** home page updates to show that the deployment(s) is no longer paused (the **UPDATES PAUSED** text has been removed for the selected deployments).

<figure><img src="../../../.gitbook/assets/image (567).png" alt="Resumed deployment" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See [Resume Updates](updates/resume-updates.md) for more information on resuming updates to a paused deployment.
{% endhint %}

## Pause deployments from updating

The _Pause Updates_ feature (disabled by default) of PMPC Cloud allows you to prevent an app that’s previously been successfully deployed from being updated whenever a new version is released.

When you click the Pause Updates button (!['Pause Updates' button](<../../../.gitbook/assets/image (568).png>)), the **Pause Deployments** dialog appears, warning you that you are pausing updates for the number of deployments you selected, and that the apps deployed using these deployments will no longer receive automatic updates.

Click **Confirm** to continue.

<figure><img src="../../../.gitbook/assets/image (576).png" alt="‘Pause Deployments’" width="408"><figcaption></figcaption></figure>

The **Pause in Progress** dialog is shown for each deployment as it is paused.

<figure><img src="../../../.gitbook/assets/image (577).png" alt="‘Pause in Progress’ dialog" width="413"><figcaption></figcaption></figure>

Once all of the deployments have been paused, the **Pause Completed** dialog is shown, which you can close by clicking **Close**.

<figure><img src="../../../.gitbook/assets/image (579).png" alt="‘Pause Completed’ dialog" width="413"><figcaption></figcaption></figure>

The **Deployments** home page updates to show **UPDATES PAUSED** for the selected deployments.

<figure><img src="../../../.gitbook/assets/image (606).png" alt="‘UPDATES PAUSED’ status" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See [Pause Updates](updates/pause.md) for more information on pausing updates to a deployment.
{% endhint %}

## Recreate selected deployments

Recreating a deployment in PMPC Cloud deletes the software from Intune and recreates it, which retriggers the deployment on the targeted resources.

When you click the Recreate button (![Recreate button](<../../../.gitbook/assets/image (709).png>)), the **Recreate Deployments** dialog appears, warning you that you are about to recreate the selected deployments using their selected configuration, which will replace the existing deployments whilst maintaining their settings and assignments.

Click **Confirm** to continue.

<figure><img src="/broken/files/ukDUk6N4W4hfwJNgZpyt" alt="‘Recreate Deployments’" width="415"><figcaption></figcaption></figure>

The **Recreate in Progress** dialog is shown for each deployment as it is recreated.

<figure><img src="/broken/files/KIlITpydDPSCwIXS9cre" alt="‘Recreate in Progress’ dialog" width="440"><figcaption></figcaption></figure>

Once all of the deployments have been recreated, the **Recreate Completed** dialog is shown, which you can close by clicking **Close**.

<figure><img src="/broken/files/W92e0XzsOGBqSSkXuyNs" alt="‘Recreate Completed’ dialog" width="413"><figcaption></figcaption></figure>

The **Deployments** home page updates to show first the deployment with an **In Progress** status whilst it is being recreated,followed by a **Success** status once it has been recreated successfully.

<figure><img src="../../../.gitbook/assets/image (609).png" alt="Deployment recreated successfully" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See [Recreate a Deployment](recreate.md) for more information on recreating a deployment.
{% endhint %}

{% hint style="danger" %}
**Important**

Since you can only recreate 20 deployments at a time, selecting more than 20 causes the **Recreate** button to become unavailable, as the tooltip explains.
{% endhint %}

## Sync selected deployments now

The _Sync Now_ feature of PMPC Cloud forces an immediate update of an app rather than waiting for the next occurrence of your Sync Schedule (this is typically used after updates to a deployment have been resumed).

When you click the Sync Now button (!['Sync Now' button](<../../../.gitbook/assets/image (612).png>)), the **Update Deployments** dialog appears, warning you that you are about to update the version for the selected deployments, which will be updated to the latest version.

Click **Confirm** to continue.

<figure><img src="../../../.gitbook/assets/image (613).png" alt="‘Update Deployments’" width="402"><figcaption></figcaption></figure>

The **Update in Progress** dialog is shown for each deployment as it is updated.

<figure><img src="../../../.gitbook/assets/image (648).png" alt="‘Update in Progress’ dialog" width="440"><figcaption></figcaption></figure>

Once all of the deployments have been updated, the **Update Completed** dialog is shown, which you can close by clicking **Close**.

<figure><img src="../../../.gitbook/assets/image (672).png" alt="‘Update Completed’ dialog" width="410"><figcaption></figcaption></figure>

The **Deployments** home page is redisplayed.

<figure><img src="../../../.gitbook/assets/image (673).png" alt="Deployments home page" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See [Sync Now](updates/sync-now.md) for more information on syncing deployments.
{% endhint %}

## Delete selected deployments

Deleting a deployment from PMPC Cloud deletes the packaged win32 app from Intune.

{% hint style="danger" %}
**Important**

Deleting a deployment does not trigger the uninstall of the software on the targeted resources. If you want to uninstall the software that the deleted deployment deployed, you will need to create a new deployment with the relevant uninstall assignments to do this.

Also, since you can only delete 20 deployments at a time, selecting more than 20 causes the **Delete** button to be unavailable, as the tooltip explains.
{% endhint %}

Select the deployment(s) you want to delete and click the **Delete** button.

<figure><img src="../../../.gitbook/assets/image (674).png" alt="Selecting the deployment(s) you want to delete and clicking the &#x27;Delete&#x27; button" width="563"><figcaption></figcaption></figure>

The **Delete Deployments** dialog appears, warning you that you are going to permanently delete the selected deployments.

Click **Confirm** to continue.

<figure><img src="../../../.gitbook/assets/image (703).png" alt="‘Delete Deployments’" width="408"><figcaption></figcaption></figure>

The **Delete in Progress** dialog is shown for each deployment as it is deleted.

<figure><img src="../../../.gitbook/assets/image (704).png" alt="‘Delete in Progress’ dialog" width="440"><figcaption></figcaption></figure>

Once all of the deployments have been deleted, the **Delete Completed** dialog is shown, which you can close by clicking **Close**.

<figure><img src="../../../.gitbook/assets/image (705).png" alt="‘Delete Completed’ dialog" width="440"><figcaption></figcaption></figure>

The **Deployments** home page updates to show the deployments have been deleted

<figure><img src="../../../.gitbook/assets/image (706).png" alt="‘Deployments’ home page showing deployments have been deleted" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See [Delete a Deployment](delete.md) for more information on deleting a deployment.
{% endhint %}

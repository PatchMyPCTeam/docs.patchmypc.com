---
hidden: true
noIndex: true
---

# Bulk Actions for Patch My PC Cloud Deployments

_Applies to: Patch My PC (PMPC) Cloud_

{% hint style="danger" %}
**Public Preview**

This documentation is for a pre-release feature still under development and therefore incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

The _Bulk Actions_ functionality of Patch My PC (PMPC) Cloud allows you to select multiple deployments to perform a management action on, versus having to repeat the same action on each deployment individually.

To select more than one deployment:

1. Navigate to the **Deployments** node of the Cloud Portal.
2. On the **Deployments** home page, either:
   1. Click the select all checkbox in the top-left corner to select all of the deployments on the current page.

<figure><img src="../../../.gitbook/assets/image (364).png" alt="Clicking the select all checkbox" width="563"><figcaption></figcaption></figure>

_<mark style="color:$danger;">**@GitBook Support - I want the following text aligned with the "Click the select" text in point a.**</mark>_

All deployments on the current page are now selected (unchecking the select all checkbox unchecks all deployments on the current page).

_<mark style="color:$danger;">**@GitBook Support - I want the "Tip" aligned with the "Click the select" text in point a.**</mark>_

{% hint style="success" %}
**Tip**

If your list of deployments spans multiple pages, you can navigate to the next page and click the select all checkbox to select all deployments on that page as well. You can repeat this process to select all of your deployments.
{% endhint %}

_<mark style="color:$danger;">**@GitBook Support - I want the following to carry on the numbering (i.e. "b." and to be aligned correctly with point a. - no other comments for you from this point onwards**</mark>_

b. Click the checkbox beside all of the deployments you wish to perform an action on.

<figure><img src="../../../.gitbook/assets/image (406).png" alt="Clicking the checkbox beside the required deployments" width="563"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

The select all option does not work with deployments with a Status of In Progress. You also cannot manually select a deployment that is In Progress.
{% endhint %}

Notice that regardless of which option you use, the number of selected deployments appears beside the **Search** box, along with the bulk actions toolbar of actions you can perform on the selected deployments.

<figure><img src="../../../.gitbook/assets/image (545).png" alt="Number of selected deployments and bulk actions toolbar" width="563"><figcaption></figcaption></figure>

At this point, you can perform the following actions on all of the selected deployments:

* [Resume paused deployments](bulk-actions.md#resume-paused-deployments)
* [Pause deployments from updating](bulk-actions.md#pause-deployments-from-updating)
* [Recreate selected deployments](bulk-actions.md#recreate-selected-deployments)
* [Sync selected deployments now](bulk-actions.md#sync-selected-deployments-now)
* [Delete the selected deployments](bulk-actions.md#delete-selected-deployments)

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

When you click the Pause Updates button (!['Pause Updates' button](<../../../.gitbook/assets/image (568).png>)), the Pause Deployments dialog appears, warning you that you are pausing updates for the number of deployments you selected, and that the apps deployed using these deployments will no longer receive automatic updates.

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







## Sync selected deployments now







## Delete selected deployments




















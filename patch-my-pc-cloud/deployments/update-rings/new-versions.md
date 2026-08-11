# How Patch My PC Cloud Update Rings Handle New Versions

_Applies to: Patch My PC Cloud_

Let’s assume you want to deploy an app in a controlled manner using Patch My PC (PMPC) Cloud.

First, you want to deploy the software to a pilot group containing a few users who want to test the software.

Then, a couple of days later, once you are happy the app functions correctly, you want to deploy it to a different group containing more users.

You could:

1. Create a single deployment targeted to the pilot users group.
2. Two days later, either:
   1. Modify the deployment targeted to the pilot users group to add the other group containing more users.
   2. Create a new deployment targeted to the other group containing more users.

This approach is admin intensive and relies on the admin remembering to create the deployment two days later to ensure the other group containing more users gets the app.

Alternatively, you can create a single deployment and enable Update Rings with:

* One ring assigned to the pilot users group.
* A separate ring assigned to the other group containing more users, but with a two-day delay to allow the pilot users to perform testing.

How Update Rings behave depends on which Update ring Start Time you chose at the time of creating the rings:

* [Delayed](new-versions.md#how-delayed-update-rings-handle-new-versions)
* [Immediate](new-versions.md#how-immediate-update-rings-handle-new-versions)

## How Delayed Update Rings Handle New Versions

For this example, we will assume you want to deploy version 2019.1 of dBase:

* &#x20;Initially to the **dBase Pilot Users** group.
* Two days later, you want to deploy the software to the **dBase All Users** group.

This is how you would configure this deployment in the PMPC Cloud portal to use **Delayed** update Rings.

<figure><img src="../../../.gitbook/assets/image (2901).png" alt="Configuring a phased deployment using Delayed Update Rings in PMPC Cloud"><figcaption></figcaption></figure>

In this scenario, when you deploy the app the **Deployments** node is displayed along with the **Success – Created <**_**app\_name**_**>** notification.

<figure><img src="../../../.gitbook/assets/image (2902).png" alt="“Deployments” node is displayed along with the “Success – Created <app_name> notification"><figcaption></figcaption></figure>

Once the deployment has been completed successfully, if you look in the Microsoft Intune admin center under **All apps** and search for the app, you will see that version **2019.1** has been successfully deployed.

<figure><img src="../../../.gitbook/assets/image (2903).png" alt="Version 2019.1 successfully deployed"><figcaption></figcaption></figure>

If you click the app and navigate to **Manage | Properties**, then scroll down to the **Assignments** section, as you are using delayed update rings you will only see the assignments for the first Update Ring has been created and applied to this version.

<figure><img src="../../../.gitbook/assets/image (2904).png" alt="Only the assignment for the first update rings has been created and applied to this version."><figcaption></figcaption></figure>

If you click on the deployment in the portal, then click **More Info**, then click **Ring 2**, you will see that this ring is scheduled to be created two days after the deployment was created.

<figure><img src="../../../.gitbook/assets/image (2905).png" alt="Ring 2 scheduled to be created two days after the deployment was created"><figcaption></figcaption></figure>

Two days after the deployment was created and after the next Sync Schedule runs, the second update ring will be created and the assignment added for the **dBase All Users** group to install the software to all of the members of this group.

<figure><img src="../../../.gitbook/assets/image (2906).png" alt="Second Update Ring has been created, which has added the assignment to the “dBase All Users” group."><figcaption></figcaption></figure>

You can now edit the deployment if required, as all of the rings have been created.

If you also look at the deployment's properties, you will see that the second ring has been created successfully and assigned to the **dBase All Users** group.

<figure><img src="../../../.gitbook/assets/image (2907).png" alt="Properties of the deployment showing the second Update Ring has been created and assigned to the “dBase All Users” group."><figcaption></figcaption></figure>

As the following table shows, the software is installed immediately for any users in the **dBase Pilot Users** group.

Any users in the **dBase All Users** group will not have the software installed until two days later.

<table><thead><tr><th width="92">Day</th><th width="197">Group</th><th>Software installed?</th></tr></thead><tbody><tr><td>0</td><td>dBase Pilot Users<br>dBase All Users</td><td>Yes<br>No</td></tr><tr><td>1</td><td>dBase Pilot Users<br>dBase All Users</td><td>Yes<br>No</td></tr><tr><td>2</td><td>dBase Pilot Users<br>dBase All Users</td><td>Yes<br>Yes</td></tr></tbody></table>

### New Version Released

Now, let’s assume a new version (2019.2) gets released.

In this scenario, you can:

* Wait until the overnight sync runs to pick up the new version.
* Run the [Sync Now](../manage-deployments/updates/sync-now.md) process to update just this deployment immediately.

{% hint style="info" %}
**Note**

This is one of the many reasons why we recommend configuring your [Sync Schedule](../../manage/settings/sync-schedule.md) to **Daily** if you are using Update Rings.

We also use the release date of the new version to validate if it is the right time to update the assignments to upgrade rings to later versions.
{% endhint %}

Once the deployment has been updated, you can now edit it as all of the rings have now been created. If you look at the deployment’s properties, you will see that for the **Ring 1**, version **2019.2** has now been assigned to the **dBase Pilot Users** group.

<figure><img src="../../../.gitbook/assets/image (2908).png" alt="Version 2019.2 targeted to the “dBase Pilot Users” Update Ring."><figcaption></figcaption></figure>

But if you click on **Ring 2**, you will see that version **2019.1** is still assigned to the **dBase All Users** group.

<figure><img src="../../../.gitbook/assets/image (2909).png" alt="“Ring 2” is still assigned version 2019.1 and assigned to the “dBase All Users” group"><figcaption></figcaption></figure>

If you check in the Intune admin center, you will now see both the existing app (version 2019.1) and the new version we have just deployed (version 2019.2).

<figure><img src="../../../.gitbook/assets/image (2910).png" alt="Intune admin center shows both the existing app (version 2019.1) and the new version we have just deployed (version 2019.2)."><figcaption></figcaption></figure>

If you check the assignments for the original deployment (version 2019.1), you will see it is now only assigned to the **dBase All Users** group.

<figure><img src="../../../.gitbook/assets/image (2911).png" alt="Updated assignment for the original version (2019.1)"><figcaption></figcaption></figure>

Whereas, if you check the assignments for the new deployment (version 2019.2), you will see it is only assigned for now to the **dBase Pilot Users** group.

<figure><img src="../../../.gitbook/assets/image (2912).png" alt="Assignments for the new deployment (version 2019.2) is only assigned for now to the dBase Pilot Users group."><figcaption></figcaption></figure>

Two days after the new version of the app is released and after the next Sync Schedule runs, the assignment for the **dBase All Users** group will be automatically moved from the version 2019.1 deployment to the 2019.2 deployment, automatically upgrading the members of the **dBase All Users** group to version 2019.2.

The old version of the app (2019.1), will remain, but will no longer show as **Yes** under the **Assigned** column in the Intune admin center. At the next sync, the old version of the app will be deleted.

<figure><img src="../../../.gitbook/assets/image (2913).png" alt="Assignments for the old version (2019.1) no longer has any assignments"><figcaption></figcaption></figure>

This update process is summarized in the following table:

<table><thead><tr><th width="88">Day*</th><th>Group</th><th>Current version</th><th>Upgraded?</th><th>Installed version</th></tr></thead><tbody><tr><td>0</td><td>dBase Pilot Users<br>dBase All Users</td><td>2019.1<br>2019.1</td><td>Yes<br>No</td><td>2019.2<br>2019.1</td></tr><tr><td>1</td><td>dBase Pilot Users<br>dBase All Users</td><td>2019.2<br>2019.1</td><td>No**<br>No</td><td>2019.2<br>2019.1</td></tr><tr><td>2</td><td>dBase Pilot Users<br>dBase All Users</td><td>2019.2<br>2019.1</td><td>No**<br>Yes</td><td>2019.2<br>2019.1</td></tr></tbody></table>

\* Number of days after the new version of the app is released

\*\* Any new users/devices added to the group will receive the version applicable to the group.

## How Immediate Update Rings Handle New Versions

For this example, we will assume you want to deploy version 2024.1 of PaintShop Pro:

* Initially to the **Corel Pilot Users** group.
* Two days later, you want to deploy the software to the **Corel All Users** group.

This is how you would configure this deployment in the PMPC Cloud portal to use **Immediate** Update Rings.

<figure><img src="../../../.gitbook/assets/image (2914).png" alt="Configuring a phased deployment using Immediate Update Rings in PMPC Cloud"><figcaption></figcaption></figure>

When you deploy the software, you see the **Deployment Summary** of how the deployment will be handled.

<figure><img src="../../../.gitbook/assets/image (2915).png" alt="Deployment summary summarizing how the deployment will be handled"><figcaption></figcaption></figure>

Once the deployment has completed successfully, if you look in the Microsoft Intune admin center under **All apps** and search for the app, you will see that version **2024.1** has been successfully deployed.

<figure><img src="../../../.gitbook/assets/image (2916).png" alt="Version 2024.1 successfully deployed"><figcaption></figcaption></figure>

If you then click the app and navigate to **Manage | Properties**, then scroll down to the **Assignments** section, you will see all of the assignments for each of the Update Rings have been created and applied to this version.

<figure><img src="../../../.gitbook/assets/image (2917).png" alt="All assignments for each of the Update Rings created and applied to this version."><figcaption></figcaption></figure>

As the following table shows, when using Immediate Rings, the software is installed immediately for any users in any of the groups assigned to any of the update rings.

| Day | Group                                       | Software installed? |
| --- | ------------------------------------------- | ------------------- |
| 0   | <p>Corel Pilot Users<br>Corel All Users</p> | <p>Yes<br>Yes</p>   |
| 1   | <p>Corel Pilot Users<br>Corel All Users</p> | <p>Yes<br>Yes</p>   |
| 2   | <p>Corel Pilot Users<br>Corel All Users</p> | <p>Yes<br>Yes</p>   |

It is only when a [new version](new-versions.md#new-version-released-1) of the targeted software gets released (current plus one or n+1), do the assignments from the previous version get moved to the latest version and Update Rings start to function as configured.

### New Version Released

Now, let’s assume a new version (2024.2) gets released.

In this scenario, you can:

* Wait until the overnight sync runs to pick up the new version.
* Run the [Sync Now](../manage-deployments/updates/sync-now.md) process to update just this deployment immediately.

{% hint style="info" %}
**Note**

This is one of the many reasons why we recommend configuring your [Sync Schedule](../../manage/settings/sync-schedule.md) to **Daily** if you are using Update Rings.

We also use the release date of the new version to validate if it is the right time to update the assignments to upgrade rings to later versions.
{% endhint %}

Once the deployment has been updated, if you look at its properties, you will see that for the **Ring 1**, version **2024.2** has now been assigned to the **Corel Pilot Users** group.

<figure><img src="../../../.gitbook/assets/image (2918).png" alt="Version 2024.2 targeted to the “Corel Pilot Users” Update Ring."><figcaption></figcaption></figure>

But if you click on **Ring 2**, you will see that version **2024.1** is still assigned to the **Corel All Users** group.

<figure><img src="../../../.gitbook/assets/image (2919).png" alt="“Ring 2” is still assigned version 2024.1 and assigned to the “Corel All Users” group"><figcaption></figcaption></figure>

If you check in the Intune admin center, you will now see both the existing app (version 2024.1) and the new version we have just deployed (version 2024.2).

<figure><img src="../../../.gitbook/assets/image (2920).png" alt="Intune admin center shows both the existing app (version 2024.1) and the new version we have just deployed (version 2024.2)."><figcaption></figcaption></figure>

If you check the assignments for the original deployment (version 2024.1), you will see it is now only assigned to the **Corel All Users** group.

<figure><img src="../../../.gitbook/assets/image (2898).png" alt="Updated assignment for the original version (2024.1)"><figcaption></figcaption></figure>

Whereas, if you check the assignments for the new deployment (version 2024.2), you will see it is only assigned for now to the **Corel Pilot Users** group.

<figure><img src="../../../.gitbook/assets/image (2899).png" alt="Assignments for the new deployment (version 2024.2) is only assigned for now to the Corel Pilot Users group"><figcaption></figcaption></figure>

Two days after the new version of the app is released, the assignment for the **Corel All Users** group will be automatically moved from the version 2024.1 deployment to the 2024.2 deployment, automatically upgrading the members of the **Corel All Users** group to version 2024.2.

The old version of the app (2024.1), will remain, but will no longer show as **Yes** under the **Assigned** column in the Intune admin center. At the next sync, the old version of the app will be deleted.

<figure><img src="../../../.gitbook/assets/image (2900).png" alt="Assignments for the old version (2024.1) no longer has any assignments"><figcaption></figcaption></figure>

This update process is summarized in the following table:

<table><thead><tr><th width="89">Day*</th><th>Group</th><th>Current version</th><th>Upgraded?</th><th>Installed version</th></tr></thead><tbody><tr><td>0</td><td>Corel Pilot Users<br>Corel All Users</td><td>2024.1<br>2024.1</td><td>Yes<br>No</td><td>2024.2<br>2024.1</td></tr><tr><td>1</td><td>Corel Pilot Users<br>Corel All Users</td><td>2024.2<br>2024.1</td><td>No**<br>No</td><td>2024.2<br>2024.1</td></tr><tr><td>2</td><td>Corel Pilot Users<br>Corel All Users</td><td>2024.2<br>2024.1</td><td>No**<br>Yes</td><td>2024.2<br>2024.2</td></tr></tbody></table>

\* Number of days after the new version of the app is released

\*\* Any new users/devices added to the group will receive the version applicable to the group.

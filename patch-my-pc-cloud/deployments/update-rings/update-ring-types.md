# Update Ring Types in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

In Patch My PC (PMPC) Cloud, there are two different types of _Update Rings,_ both of which depend on the start time of the relevant deployment and how you have your Sync Schedule configured:

* [Delayed Update Rings](update-ring-types.md#delayed-update-rings)
* [Immediate Update Rings](update-ring-types.md#immediate-update-rings)

{% hint style="info" %}
**Note**

Only once the configured start time has passed will the assignments under an Update Ring be created in Intune for the corresponding Win32 app.
{% endhint %}

## Delayed Update Rings

The _Delayed_ option works as follows:

1. The first Update Ring is created immediately, and the software is deployed to the assigned test users/devices (usually known as a _pilot group)._
2. After waiting the configured number of days from when the deployment was created (to allow testing to be performed), the next Update Ring is created, and the software is deployed to the assigned users/devices (usually a bigger group/all assigned users/devices).
3. Step 2 is repeated until all Update Rings have been created and the software has been deployed to all users/devices requiring it.

### Advantages

The advantage of the delayed option is:

* As the next ring (and therefore the next set of assignments) has not been created, if the software causes an issue that is detected in the first ring, the issue cannot propagate to other rings as they haven’t been created.
* Your full Update Ring workflow is followed, starting with the current version.
* Useful when you want every version to follow the same controlled rollout.

### Disadvantages

The disadvantages of the delayed option are:

* The deployment will be in a scheduled state until at least one version has passed through all rings.
* Your Sync Schedule configuration can impact both when the initial rings are created and when the Sync Schedule runs, which will update your rings and their assignments, including promoting a new version to your relevant rings.
* You cannot edit a deployment that uses delayed Update Rings until all of the rings have been created. If you try, you will see the [Error - Editing is not allowed until all rings are created after the configured delay.](../../troubleshoot/update-rings/error-editing-is-not-allowed-until-all-rings-are-created-after-the-configured-delay-cloud-error.md)
* If you need to change anything, you must delete and recreate the deployment.

## Immediate Update Rings

The _Immediate_ options works as follows:

1. All Update Rings are created immediately with their relevant delays and assignments.
2. Assignments from all of the Update Rings will be applied to the version of the app you created the deployment with.
3. Update Rings will not begin to work until the next version (current plus one or n+1) of the software is released. At this point, the assignments from the previous version are moved to the latest version and Update Rings start to function as configured.

### Advantages

The advantages of the immediate option are:

* All rings are created and configured once.
* The deployment can be edited and adjusted as required.
* You can make configuration changes at any time.
* Helpful for first-time deployments where version _n_ needs to reach all devices right away, while future updates follow the phased rollout.

### Disadvantages

The disadvantages of the immediate option are:

* If the software in one ring causes an issue, if the admin forgets to pause the deployment or remove any additional rings, the issue could be spread to the next ring, even if a delay between rings is configured.
* All assignments from all Update Rings are applied to the same version of the application that the deployment was created with. However, this is only true for the initial creation of the Update Rings. All other functionality of Update Rings will continue to work as normal in any new app versions.

{% hint style="danger" %}
**Important**

You need to consider the following when working with Update Rings:

* You cannot mix standard deployments (that don’t use Update Rings) and Update Rings in a single deployment.
* [How the Sync Schedule Affects Update Rings](sync-schedule.md) for more information on how your configuration of the Sync Schedule will affect how Update Rings behave.
* [How Update Rings Handle New Versions](new-versions.md) for more information about how update rings handle new versions, including worked examples.
{% endhint %}

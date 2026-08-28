# Trigger a Software Update Point Sync section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Trigger a Software Update Point Sync** section of the **WSUS Options** tab in Patch My PC (PMPC) Publisher is where you configure the SMS Provider connection, which the Publisher uses to communicate with ConfigMgr. This connection enables the Publisher to trigger Software Update Point (SUP) synchronizations and ultimately serves as the foundation for all Publisher interactions with ConfigMgr.

<figure><img src="../../../../.gitbook/assets/image (783).png" alt="&#x27;Trigger a Software Update Point Sync&#x27; section" width="563"><figcaption></figcaption></figure>

This section also allows you to manually initiate a SUP sync, which is the process by which ConfigMgr retrieves update metadata from WSUS (and ultimately Microsoft Update), making newly published first and third-party updates visible and actionable in the ConfigMgr console.

## Perform Delta Synchronization

Clicking the **Perform Delta Synchronization** button triggers a _delta sync_ that only retrieves the changes from WSUS that have occurred since the last successful synchronization.

This includes newly added updates and updates that have been revised or removed. Updates that were previously synchronized and have not changed are not re-evaluated.

Because of this limited scope, delta syncs are faster and place less load on WSUS, SQL, and the ConfigMgr Site Server. For this reason, most synchronizations in ConfigMgr (both manual and scheduled) run as delta syncs.

The key characteristics of delta synchronization are:

* Only new or changed update metadata is synchronized.
* The entire update catalog is not reprocessed.
* Faster and less resource-intensive.
* Commonly sufficient after publishing or enabling third-party updates.

{% hint style="danger" %}
**Important**

It’s important to note that a delta synchronization does not repair updates that may have been damaged or deleted during previous synchronizations.
{% endhint %}

## Perform Full Synchronization

Clicking the **Perform Full Synchronization** button forces ConfigMgr to perform a _full sync_, i.e. to synchronize the entire update catalog from WSUS, filtered by the SUP site components product and classifications configuration.&#x20;

At the end of a full sync, the ConfigMgr database reflects the complete and current state of the WSUS catalog.

Full syncs are more resource-intensive and take longer to complete, especially in environments with large update catalogs. Because of this, they are not typically used for routine operations.

The key characteristics of a full synchronization are:

* The entire update catalog is re-evaluated.
* Updates that were damaged or deleted in previous synchronizations can be repaired.
* More time-consuming and resource-intensive.
* Intended for troubleshooting or recovery scenarios.

{% hint style="info" %}
**Note**

ConfigMgr typically escalates to a _full sync_ when required. This occurs when configuration changes are detected that cannot be processed incrementally.

Examples include:

* Switching to a different default SUP.
* Changes to Product and Classification selection in the SUP site component properties.
* Modifications to supersedence settings or the supersedence window.

In addition, ConfigMgr periodically performs a full sync at a fixed interval (every 7 days by default).&#x20;

See [About Synchronizing the Software Update Point](https://learn.microsoft.com/en-us/intune/configmgr/develop/sum/about-synchronizing-the-software-update-point) for more information on SUP synchronization.
{% endhint %}

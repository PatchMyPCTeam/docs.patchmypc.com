# Trigger a SUP Sync

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Trigger a Software Update Point Sync** section is where you configure the SMS Provider connection, which the Publisher uses to communicate with ConfigMgr. This connection enables the Publisher to trigger SUP synchronizations and ultimately serves as the foundation for all the Publisher interactions with ConfigMgr.

This section also allows you to manually initiate a SUP sync. A SUP sync is the process by which ConfigMgr retrieves update metadata from WSUS (and ultimately Microsoft Update), making newly published first and third-party updates visible and actionable in the ConfigMgr console.

![Trigger a SUP sync](/_images/image-(4105).png "Trigger a SUP sync")

## Perform Delta Synchronization

A **delta sync** retrieves from WSUS only changes that have occurred since the last successful synchronization. This includes newly added updates and updates that have been revised or removed. Updates that were previously synchronized and have not changed are not re-evaluated.

Because of this limited scope, delta syncs are faster and place less load on WSUS, SQL, and the site server. For this reason, most synchronizations in ConfigMgr, both manual and scheduled, run as delta syncs.

Key characteristics of delta synchronization:

* Synchronizes only new or changed update metadata.
* Does not reprocess the entire update catalog.
* Faster and less resource-intensive.
* Commonly sufficient after publishing or enabling third-party updates.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>It’s important to note that a delta synchronization does not repair updates that may have been damaged or deleted during previous synchronizations.</p>
</blockquote>

## Perform Full Synchronization

A **full sync** forces ConfigMgr to synchronize the entire update catalog from WSUS, filtered by the SUP site components product and classifications configuration. At the end of a full sync, the ConfigMgr database reflects the complete and current state of the WSUS catalog.

Full syncs are more resource-intensive and take longer to complete, especially in environments with large update catalogs. Because of this, they are not typically used for routine operations.

Key characteristics of full synchronization:

* Re-evaluates the entire update catalog.
* Can repair updates that were damaged or deleted in previous synchronizations.
* More time-consuming and resource-intensive.
* Intended for troubleshooting or recovery scenarios.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>ConfigMgr will typically escalate to a **full sync** when it's required. This occurs when configuration changes are detected that cannot be processed incrementally.</p>
<p>Examples include:</p>
<p>* Switching to a different default Software Update Point.</p>
<p>* Changes to Product and Classification selection in the SUP site component properties.</p>
<p>* Modifications to supersedence settings or the supersedence window.</p>
<p>In addition, ConfigMgr periodically performs a full sync on a fixed interval (every 7 days by default). More information on SUP synchronization can be found at <a href="https://learn.microsoft.com/en-us/intune/configmgr/develop/sum/about-synchronizing-the-software-update-point">https://learn.microsoft.com/en-us/intune/configmgr/develop/sum/about-synchronizing-the-software-update-point</a></p>
</blockquote>

## Configure SMS Provider Connection

The **SMS Provider** is the interface that enables all interactions with ConfigMgr, including actions performed in the ConfigMgr console and through supported APIs. The Publisher also relies on the SMS Provider to perform operations such as triggering SUP synchronizations, creating and modifying applications, and distributing content.

The SMS Provider configuration is shared across the Publisher. When you configure the SMS Provider from **Updates > Options**, the same settings are automatically used in other areas of the product, including **ConfigMgr Apps > Options** and the **Sync Schedule** tab.

For information on how to configure the SMS Provider connection, see [Configure the SMS Provider Connection](../../../publisher-reference/configure-the-sms-provider-connection.md).
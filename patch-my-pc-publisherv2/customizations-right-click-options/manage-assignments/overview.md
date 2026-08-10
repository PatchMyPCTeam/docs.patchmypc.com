# Overview

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_
\
_Available on tab: Intune Apps, Intune Updates_

## Overview

The **Manage Assignments** option allows you to control which Intune assignments the Publisher creates and maintains for Intune applications and Intune updates.

![Manage Assignments](/_images/image-(4022).png "Manage Assignments")

When selected, the **Manage Application Assignments** form opens. From this form, you can add new assignments, remove existing assignments, and control whether the Publisher should override manual assignment changes made directly in Intune.

![Manage Application Assignments Form](/_images/image-(4023).png "Manage Application Assignments Form")

Assignments are grouped by intent so you can clearly see which Entra ID groups receive the application automatically (Required), which groups can install it from the Company Portal (Available), and which groups are targeted for remova(Uninstall).

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>All changes made in this window are applied during the **next** Publisher [synchronization](../../administration/sync-schedule.md). Changes are not applied immediately to Win32 apps that already exist in Intune.</p>
<p>If you want to make changes to assignments for applications and updates that have already been published to Intune, use the [Intune Application Manager](../../administration/intune-apps-updates/form-controls/intune-application-manager.md) instead.</p>
</blockquote>

## Required for Enrolled Devices

Assignments listed under **Required for Enrolled Devices** are automatically installed on targeted devices based on the configured availability and deadline settings. These assignments are typically used for mandatory applications or updates that must be installed to remain compliant.

Each row represents a targeted Entra ID group and displays the assignment configuration, including mode, user notification behavior, Delivery Optimization priority, filter usage, availability time, deadline, and restart grace period.

## Available for Enrolled Devices

Assignments listed under **Available for Enrolled Devices** make the application visible in the Company Portal for the targeted user or device groups, but do not _require_ installation. Users can choose when or whether to install the app.

These assignments share many of the same configuration options as Required assignments, such as notification behavior and Delivery Optimization priority, but do not support deadlines.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>When an Available assignment targets a **device based Entra ID group**, only the **primary user of the device** will see the application in the Company Portal. Other users who sign in to the same device will not see the app listed.</p>
</blockquote>

## Uninstall for Enrolled Devices

Assignments listed under **Uninstall for Enrolled Devices** automatically remove the application from devices in the targeted groups. This intent is commonly used for decommissioning applications or removing software from specific populations.

Only uninstall relevant settings are shown, such as notification behavior and restart handling.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Uninstall assignments are **version specific** and only apply to the exact application version that is deployed. An Uninstall assignment will not remove earlier or later versions of the same product.</p>
<p>For example, if an Uninstall assignment is configured for Google Chrome version 100.2, it will not uninstall version 100.1.</p>
<p>To successfully uninstall a specific version, that exact version must be installed on the device. If the device is running an earlier version, deploy the corresponding update for the target version first. Once the device reports the matching version, the Uninstall assignment becomes applicable and the removal will proceed as expected.</p>
</blockquote>
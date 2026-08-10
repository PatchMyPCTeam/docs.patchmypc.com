# Overview of Manage Assignments in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: Intune Apps, Intune Updates_

The **Manage Assignments** right-click option in Patch My PC (PMPC) Publisher allows you to control which Intune assignments the Publisher creates and maintains for Intune applications and Intune updates.

When selected, the **Manage Application Assignments** form opens.

!['Manage Application Assignments' form](../../../../.gitbook/assets/image-\(4766\).png)

From this form, you can add new assignments, remove existing assignments, and control whether Publisher should override manual assignment changes made directly in Intune.

Assignments are grouped by tab so you can clearly see which Entra ID groups receive the application automatically (**Required**), which groups can install it from the Company Portal (**Available**), and which groups are targeted for removal (**Uninstall**).

> \*\*Important\*\*
>
> All changes made in this window are applied during the next Publisher \[synchronization]\(../../../manage/sync-schedule-tab/). Changes are not applied immediately to Win32 apps that already exist in Intune.
>
> If you want to make changes to assignments for applications and updates that have already been published to Intune, use the \[Intune Manager]\(../../../manage/intune-tabs/intune-manager.md) instead.

## Required for enrolled devices

Assignments listed under the **Required for enrolled devices** section of the **Required Assignments** tab are automatically installed on targeted devices based on the configured availability and deadline settings. These assignments are typically used for mandatory applications or updates that must be installed to remain compliant.

Each row represents a targeted Entra ID group and displays the assignment configuration, including mode, user notification behavior, Delivery Optimization priority, filter usage, availability time, deadline, and restart grace period.

## Available for enrolled devices

Assignments listed under the **Available for enrolled devices** section of the **Available Assignments** tab make the application visible in the Company Portal for the targeted user or device groups, but do not _require_ installation. Users can choose when or whether to install the app.

These assignments share many of the same configuration options as Required assignments, such as notification behavior and Delivery Optimization priority, but do not support deadlines.

> \*\*Note\*\*
>
> When an \*\*Available\*\* assignment targets a device-based Entra ID group, only the device's primary user will see the application in the Company Portal. Other users who sign in to the same device will not see the app listed.

## Uninstall for enrolled devices

Assignments listed under the **Uninstall for enrolled devices** section of the **Uninstall Assignments** tab automatically remove the application from devices in the targeted groups. This intent is commonly used for decommissioning applications or removing software from specific populations.

Only uninstall relevant settings are shown, such as notification behavior and restart handling.

> \*\*Important\*\*
>
> Uninstall assignments are version-specific and only apply to the exact application version that is deployed. An Uninstall assignment will not remove earlier or later versions of the same product.
>
> For example, if an Uninstall assignment is configured for Google Chrome version 100.2, it will not uninstall version 100.1.
>
> To successfully uninstall a specific version, that exact version must be installed on the device. If the device is running an earlier version, deploy the corresponding update for the target version first. Once the device reports the matching version, the Uninstall assignment becomes applicable, and the removal will proceed as expected.

# Assignment Options

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: Intune Apps, Intune Updates_

## Overview

Assignment Options allow you to configure how an Intune assignment behaves for applications and updates managed by the Publisher.

![Assignment Options](/_images/image-(4028).png)

These options are available only after an assignment has been added. Any changes made here are saved in the Publisher configuration and are applied to the Intune application or update during the next Publisher synchronization.

> \*\*Important\*\*
>
> All changes made in this window are applied during the next Publisher \[synchronization]\(../../administration/sync-schedule.md). Changes are not applied immediately.
>
> If you want to make changes to assignments for applications and updates that have already been published to Intune, use the \[Intune Application Manager]\(../../administration/intune-apps-updates/form-controls/intune-application-manager.md) instead.

## Mode

Mode determines whether a group is included or excluded for the assignment.

![Assignment Mode](/_images/image-(4029).png)

* When set to **Include**, Intune applies the assignment to users or devices in the selected Entra group.
* When set to **Exclude**, Intune explicitly excludes the group even if it is part of a broader included group.

Exclusions always take precedence over inclusions. This allows precise targeting for pilot groups, testing scenarios, or exception handling.

The example indicates how Include and Exclude modes work together within the same assignment intent. In the Available for enrolled devices section, the **All Users** group is set to **Include**. This makes the application available in the Company Portal for all targeted users. A second assignment targets the **LAPS Admins** Entra and is set to **Exclude**. This explicitly prevents members of that group from seeing or installing the application, even though they are part of the broader **All Users** group.

> \*\*Note\*\*
>
> The \*\*Exclude\*\* mode is not selectable for the built in \*\*All Users\*\* and \*\*All Devices\*\* targets.

## Notification

Notification controls whether toast notifications are shown to the user when the Intune Management Extension installs or uninstalls the application or update.

![Assignment Notification](/_images/image-(4030).png)

* When set to **Show all**, all installation and restart related notifications are displayed.
* When set to **Show restarts only**, only notifications related to required restarts are displayed.
* When set to **Hide all**, all toast notifications are suppressed.

**Example**

The example above demonstrates how different Notification settings can be applied per assignment to control user facing toast notifications during application installation or uninstallation. In this scenario, multiple Entra groups are targeted with different notification behaviors.

The **LAPS Admins group** is configured with **Show all**. Users in this group receive all installation and restart related notifications when the app is installed or updated.

The **AOVPN Users group** is configured with **Hide all**. Users in this group do not see any toast notifications related to the installation or restart process.

The **Autopilot Admins** group is configured with **Show restarts only**. Users only receive notifications related to required restarts, while installation progress notifications are suppressed.

> \*\*Note\*\*
>
> Notifications in this context are delivered as Windows toast notifications and are controlled by the Intune Management Extension during application install or uninstall.
>
> These notifications are not related to and should not be confused with \[Manage Conflicting Processes]\(../manage-conflicting-processes/) notifications, which are a separate feature and serve a different purpose.

## DO Priority

Delivery Optimization priority controls how quickly application content is downloaded after the Intune Management Extension evaluates the assignment.

![Assignment DO Priority](/_images/image-(118).png)

• When set to **Foreground**, Intune prioritizes the download and processes the application content immediately. This is commonly used for Autopilot scenarios or time sensitive deployments where faster installation is required.

• When set to **Background**, Windows downloads the content with normal priority and may defer the download based on network conditions and device activity. This is recommended for most Intune Updates where immediate installation is not critical.

**Example**

The example above shows 2 available assignments that use different Delivery Optimization priorities.

**Foreground** is configured for the **LAPS Admins** group. This prioritizes the download and processes the application content immediately.

**Background** is configured for the **AOVPN Users** group. This allows Windows to download the content with normal priority based on network conditions and device activity.

> \*\*Note\*\*
>
> For most Intune Updates, \*\*Background\*\* is recommended because installations are usually not time critical.
>
> \\
>
> For applications deployed during \*\*Autopilot\*\*, \*\*Foreground\*\* is recommended to reduce onboarding delays.

## Filter Mode and Filter (Name)

Filters allow you to refine assignment targeting using Intune device filters based on attributes such as operating system version, device model, enrollment type, or join type.

![Assignment Intune Filters](/_images/image-(119).png)

This enables advanced targeting scenarios such as excluding virtual machines, targeting corporate devices only, or limiting deployment to specific OS builds.

**Filter Mode**

* When set to **None**, no filter is applied and the Filter selection option is disabled (set to n/a).
* When set to **Include**, the assignment applies only to devices that match the **Filter**.
* When set to **Exclude**, the assignment applies to all targeted devices except those that match the **Filter**.

**Filter Name**\
Filter Name selects the Intune device filter to apply to the assignment. Only one filter can be selected per assignment.

**Example**\
The example above shows how Filter Mode and Filter (Name) can be used to further refine assignment targeting beyond Entra group membership.

For the **LAPS Admins** group, Filter Mode is set to **None**. No Intune filter is applied, so the assignment targets all devices in the group without additional filtering.

For the **AOVPN Users** group, Filter Mode is set to **Include** with the **Cloud PCs** filter. The assignment applies only to devices in the group that match the Cloud PCs filter criteria.

For the **Autopilot Admins** group, Filter Mode is set to **Exclude** with the **Windows 10** filter. The assignment applies to the group except for devices that match the Windows 10 filter.

### Filter Selection

The Filter Selection form is used to choose an existing Intune device filter to apply to an assignment when Filter Mode is set to Include or Exclude.

![Filter Selection](/_images/image-(121).png)

This form lists all Intune device filters available in your tenant and allows you to search, review, and select the appropriate filter. Only one filter can be selected per assignment.

### Steps to Select a Filter

1. Set Filter Mode to Include or Exclude on the assignment.
2. Select the n/a value in the Filter column to open the Filter Selection form.
3. Use Search or Refresh to locate the required filter.
4. Select the filter from the list.
5. Select OK to apply the filter.

### Filter Validation

When configuring assignments, the Publisher validates that a filter is selected whenever Filter Mode is set to Include or Exclude.

If Filter Mode is set to Include or Exclude and the Filter column remains set to **n/a**, a validation error is triggered. This indicates that a filter mode has been selected but no Intune device filter has been assigned.

![Filter Validation](/_images/image-(120).png)

In this state, the assignment configuration cannot be saved. A validation warning is displayed at the bottom of the form, and details are shown indicating that the assignment is missing a required filter selection.

## Availability and Deadline

The Available Time and Deadline Time form dynamically changes based on the assignment intent. Only the options supported by Intune for that intent are displayed. This ensures that invalid or unsupported configurations cannot be set.

![Availability and Deadline Options](/_images/image-(125).png)

* **Required for enrolled devices** assignments show both **Availability** and Installation **Deadline**. Availability controls when content is downloaded. Deadline controls when installation is enforced.
* **Available for enrolled devices** assignments show **Availability** only. Deadlines are not supported. Availability controls when the app appears in the Company Portal and when users can start installation.
* **Uninstall for enrolled devices** assignments show Installation **Deadline** only. Availability is not used for uninstall intent. Deadline controls when the uninstall is enforced.

### Available Time

Available Time controls when an Intune application or update becomes available to devices for a specific assignment.

![Assignment Available Time](/_images/image-(122).png)

* For **Required for enrolled devices** assignments, content download begins at the available time.
* For **Available for enrolled devices** assignments, the application becomes visible in the Company Portal at the available time.

If no custom availability is configured, the default behavior is **As soon as possible**, which makes the assignment available as soon as policy is received.

> \*\*Important\*\*
>
> Intune has a known issue when multiple \*\*Required\*\* assignments exist for the same application and different availability times are configured.
>
> If one assignment uses \*\*As soon as possible\*\* and another assignment uses a future availability time, the Intune Management Extension may delay content download and installation until the later availability time is reached.
>
> This behavior is documented in a Patch My PC blog at [https://patchmypc.com/blog/intune-asap-assignments-bug/](https://patchmypc.com/blog/intune-asap-assignments-bug/).
>
> A recommended workaround is to configure availability as \*\*Publishing date plus 0 days\*\*. This sets the availability to the application publish time, which is already in the past when the device evaluates the assignment. As a result, Intune processes the assignment immediately and avoids delays caused by mixed availability configurations.

Available Time is configured per assignment by selecting the value in the **Available Time** column. This opens the **Edit Availability** dialog.

![Availability Configuration](/_images/image-(127).png)

You can configure availability relative to the publishing date or set a specific date and time. Availability can be evaluated using UTC or the device local time zone.

1. Open the Manage Application Assignments window.
2. Locate the assignment you want to modify.
3. Select the value in the **Available Time** column.
4. Click **Application availability**.
5. Select **Publishing date plus** or **Specific date and time**.
6. Configure the **number of days and time**, or select a **specific date**.
7. Choose **UTC** or **Device time** **zone** as required.
8. Click **OK** to save the configuration.

The updated availability setting is shown in the **Available Time** column and is applied during the next Publisher [synchronization](../../administration/sync-schedule.md).

#### Availability Time Processing Behavior

Availability time should be treated as an **earliest eligible time**, not a guaranteed execution time.

When a device receives policy, the Intune Management Extension processes assignments through the Global Resource Scheduler (GRS). Assignment evaluation is not continuous. Instead, a background processing cycle runs periodically, every 8 hours.

Because of this behavior, even if you configure a specific date and time for availability, the assignment may not be processed at that exact time. As long as the device is powered on, the assignment can be actioned any time from the configured availability onward, up to several hours later.

This is a limitation of the Intune Management Extension scheduling model and not a limitation of the Publisher configuration.

When setting a specific availability time, plan for a possible delay window and avoid assuming precise execution at the configured minute.

### Deadline

Deadline controls when installation or removal is enforced for an assignment.

![Assignment Deadline](/_images/image-(116).png)

Deadlines are supported only for **Required for enrolled devices** and **Uninstall for enrolled devices** assignments. Deadlines are not supported for **Available for enrolled devices** assignments.

* For **Required for enrolled devices assignments**, installation is enforced when the deadline is reached.
* For **Uninstall for enrolled devices assignments**, removal of the application is enforced when the deadline is reached.

If **no deadline is configured**, enforcement still occurs, but it happens after the **Available Time** is reached. In this case, installation or uninstall is processed based on availability and policy evaluation scheduling timing rather than a fixed enforcement deadline.

> \*\*Important\*\*
>
> When multiple \*\*Required\*\* assignments exist for the same application and devices belong to more than one assignment, Intune determines applicability based on availability first. If availability processing is delayed due to a known bug, deadline enforcement is also delayed because the assignment is not considered applicable until availability is reached.
>
> In scenarios where one assignment uses \*\*As soon as possible\*\* and another uses a future availability time, Intune may defer both content download and subsequent deadline enforcement until the later availability time is reached.
>
> This behavior is an Intune platform limitation and is documented in the Patch My PC blog [https://patchmypc.com/blog/intune-asap-assignments-bug/](https://patchmypc.com/blog/intune-asap-assignments-bug/).
>
> To ensure predictable deadline enforcement, avoid mixing \*\*As soon as possible\*\* with future availability times. A recommended approach is to configure availability as \*\*Publishing date plus 0 days\*\*, which sets availability to the publish time and allows both availability processing and deadline enforcement to occur as expected.

A Deadline is configured per assignment by selecting the value in the Deadline column. This opens the Edit Availability dialog.

![Deadline Configuration](/_images/image-(117).png)

You can configure the deadline relative to the publishing date or set a specific date and time. Deadline evaluation can be performed using UTC or the device local time zone.

1. Open the Manage Application Assignments window.
2. Locate the Required or Uninstall assignment you want to modify.
3. Select the value in the **Deadline** column.
4. Enable **Installation deadline**.
5. Select **Publishing date plus** or **Specific date and time**.
6. Configure the **number of days and time**, or select a **specific date**.
7. Choose **UTC** or **Device time zone** as required.
8. Click **OK** to save the configuration.

The updated deadline setting is shown in the Deadline column and is applied during the next Publisher synchronization.

#### Deadline Processing Behavior

A Deadline should be treated as the earliest enforcement time, not a guaranteed execution time.

After the deadline is reached, the Intune Management Extension evaluates enforcement through the Global Resource Scheduler. Enforcement checks are not continuous. Instead, a background processing cycle runs periodically, every 8 hours.

Because of this behavior, even if you configure a specific date and time for a deadline, installation or uninstall enforcement may not occur at that exact time. As long as the device is powered on, enforcement can occur any time after the configured deadline, up to several hours later.

This is a limitation of the Intune Management Extension scheduling model and not a limitation of the Publisher configuration.

When setting a specific deadline, plan for a possible enforcement delay window and avoid assuming precise execution at the configured minute.

## Restart Grace Period

The **Restart Grace Period** controls how long a device can delay a required reboot after an application install or uninstall is enforced.

![Restart Settings / Grace Period](/_images/image-(4031).png)

During a configured grace period, the user can continue working before a reboot, indicated by the Win32 app, becomes mandatory.

![Restart Grace Period Configuration](/_images/image-(4032).png)

You can configure the Restart grace period settings by selecting the **Grace Period** value in the assignment row.

1. Open the Manage Application Assignments window.
2. Locate the assignment you want to modify.
3. Select the value in the Grace Period column.
4. Enable **Configure restart grace period**.
5. Configure the **Grace period** (minutes).
6. Configure the **Restart countdown** (minutes).
7. Optionally enable **Allow snooze** and set the **snooze duration**.
8. Click **OK** to save the configuration.

The updated restart grace period settings are applied during the next Publisher synchronization.

> \*\*Note\*\*
>
> For a deeper explanation of how Intune processes restart grace periods, notification behavior, countdown timing, and enforcement nuances, review the Patch My PC blog at [https://patchmypc.com/blog/intune-s-restart-grace-period/](https://patchmypc.com/blog/intune-s-restart-grace-period/).

### Restart Grace Period Behavior

When a restart is required, the Intune Management Extension displays Windows toast notifications informing the user that a restart is pending.

As the grace period progresses, Intune escalates the user experience. This includes toast notifications and a restart countdown dialog that appears shortly before enforcement. The **Restart countdown** setting controls how long before enforcement the countdown dialog is shown. The default value is **15 minutes**, giving the user a final opportunity to save work.

If **Allow snooze** is enabled, users can temporarily delay the reboot. The **Snooze duration** determines how long the reboot is postponed before notifications resume.

### Installer Dependency

The restart grace period is enforced only when the installer explicitly signals that a reboot is required.

If the installer does not return a reboot required exit code, Intune does not enforce a restart, even if a restart grace period is configured. In this scenario, no reboot countdown or enforcement occurs.

This behavior ensures that restart enforcement is predictable and based on the installer’s actual reboot requirement, with the Intune Management Extension honoring that signal.
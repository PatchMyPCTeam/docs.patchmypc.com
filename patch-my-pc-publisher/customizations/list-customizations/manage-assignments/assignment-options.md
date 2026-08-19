# Assignment Options in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: Intune Apps, Intune Updates_

_Assignment Options_ in Patch My PC (PMPC) Publisher allow you to configure how an Intune assignment behaves for applications and updates managed by Publisher.

After using the [Manage Assignments](add-remove-assignment.md) right-click option to [add an assignment](add-remove-assignment.md#steps-to-add-an-assignment), you can edit various assignment settings.

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><a href="assignment-options.md#mode">Mode</a></td><td valign="top"><a href="assignment-options.md#notification">Notification</a></td><td valign="top"><a href="assignment-options.md#do-priority">DO Priority</a></td></tr><tr><td valign="top"><a href="assignment-options.md#filter-mode-and-filter-name">Filter Mode and Filter (Name)</a></td><td valign="top"><a href="assignment-options.md#available-time">Available Time</a></td><td valign="top"><a href="assignment-options.md#deadline">Deadline</a></td></tr><tr><td valign="top"><a href="assignment-options.md#grace-period">Grace Period</a></td><td valign="top"></td><td valign="top"></td></tr></tbody></table>

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1).png" alt="Application Assignments" width="563"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

All changes made in this window are applied during the next Publisher [Synchronization](../../../manage/sync-schedule-tab/). Changes are not applied immediately to Win32 apps that already exist in Intune.

If you want to make changes to assignments for applications and updates that have already been published to Intune, use the [Intune Manager](../../../manage/intune-tabs/intune-manager.md) instead.
{% endhint %}

## Mode

The value defined in the **Mode** field determines whether a group is included or excluded for the assignment.

<table><thead><tr><th width="102.22222900390625" valign="top">Setting</th><th valign="top">When set to this Intune...</th></tr></thead><tbody><tr><td valign="top">Include</td><td valign="top">Applies the assignment to users or devices in the selected Entra ID group.</td></tr><tr><td valign="top">Exclude</td><td valign="top">Explicitly excludes the group even if it is part of a broader included group.</td></tr></tbody></table>

Exclusions always take precedence over inclusions. This allows precise targeting for pilot groups, testing scenarios, or exception handling.

### Mode Example

The example below shows how Include and Exclude modes work together within the same assignment intent. In the **Available for enrolled devices** section, the **All Users** group is set to **Include**. This makes the application available in the Company Portal for all targeted users.

A second assignment targets the **Corel Pilot Users** Entra ID group and is set to **Exclude**. This explicitly prevents members of that group from seeing or installing the application, even though they are part of the broader **All Users** group.

<figure><img src="../../../../.gitbook/assets/image (4827).png" alt="Mode example" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

**Exclude** mode is not selectable for the built-in **All Users** and **All Devices** targets.
{% endhint %}

## Notification

The value defined in the **Notification** field controls whether toast notifications are shown to the user when the Intune Management Extension installs or uninstalls the application or update.

<table><thead><tr><th width="168.888916015625" valign="top">Setting</th><th valign="top">When set to this...</th></tr></thead><tbody><tr><td valign="top">Show all</td><td valign="top">All installation and restart-related notifications are displayed.</td></tr><tr><td valign="top">Show restarts only</td><td valign="top">Only notifications related to required restarts are displayed.</td></tr><tr><td valign="top">Hide all</td><td valign="top">All toast notifications are suppressed.</td></tr></tbody></table>

### Notification Example

The following example demonstrates how different Notification settings can be applied per assignment to control user-facing toast notifications during application installation or uninstallation.

<figure><img src="../../../../.gitbook/assets/image (4815).png" alt="Notification Example" width="563"><figcaption></figcaption></figure>

In this scenario, multiple Entra ID groups are targeted with different notification behaviors.

* The **Corel Pilot Users** group is configured with **Show all**. Users in this group receive all installation and restart-related notifications when the app is installed or updated.
* The **dBase All Users** group is configured with **Show restarts only**. Users only receive notifications related to required restarts, while installation progress notifications are suppressed.
* The **Corel All Users** group is configured with **Hide all**. Users in this group do not see any toast notifications related to the installation or restart process.

{% hint style="info" %}
**Note**

Notifications in this context are delivered as Windows toast notifications and are controlled by the Intune Management Extension during application install or uninstall.

These notifications are not related to and should not be confused with [Manage Conflicting Processes](../manage-conflicting-processes/) notifications, which are a separate feature and serve a different purpose.
{% endhint %}

## DO Priority

The value defined in the **DO Priority** field controls how quickly Delivery Optimization downloads application content after the Intune Management Extension evaluates the assignment.

<table><thead><tr><th width="120" valign="top">Setting</th><th valign="top">When set to this...</th></tr></thead><tbody><tr><td valign="top">Foreground</td><td valign="top">Intune prioritizes the download and processes the application content immediately. This is commonly used for Autopilot scenarios or time-sensitive deployments where faster installation is required.</td></tr><tr><td valign="top">Background</td><td valign="top">Windows downloads the content with normal priority and may defer the download based on network conditions and device activity. This is recommended for most Intune Updates where immediate installation is not critical.</td></tr></tbody></table>

### DO Priority Example

The example below shows two available assignments that use different Delivery Optimization priorities:

* **Foreground** is configured for the **Corel Pilot Users** group. This prioritizes the download and processes the application content immediately.
* **Background** is configured for the **Corel All Users** group. This allows Windows to download the content with normal priority based on network conditions and device activity.

<figure><img src="../../../../.gitbook/assets/image (4816).png" alt="DO Priority Example" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

For most Intune Updates, **Background** is recommended because installations are usually not time-critical. For applications deployed during Autopilot, **Foreground** is recommended to reduce onboarding delays.
{% endhint %}

## Filter Mode and Filter (Name)

Filters allow you to refine assignment targeting using Intune device filters based on attributes such as operating system version, device model, enrollment type, or join type.

This enables advanced targeting scenarios such as excluding virtual machines, targeting corporate devices only, or limiting deployment to specific OS builds.

The value defined in the **Filter Mode** field selects the Intune device filter (selected in the **Filter** field) to apply to the assignment. Only one filter can be selected per assignment.

<table><thead><tr><th width="104.44439697265625" valign="top">Setting</th><th valign="top">When set to this...</th></tr></thead><tbody><tr><td valign="top">None</td><td valign="top">No filter is applied and the Filter selection option is disabled (set to <strong>n/a</strong>).</td></tr><tr><td valign="top">Include</td><td valign="top">The assignment applies only to devices that match the <a href="assignment-options.md#select-filter">selected filter</a> in the <strong>Filter</strong> field.</td></tr><tr><td valign="top">Exclude</td><td valign="top">The assignment applies to all targeted devices except those that match the <a href="assignment-options.md#select-filter">selected filter</a> in the <strong>Filter</strong> field.</td></tr></tbody></table>

### Filter Name Example

The following example shows how **Filter Mode** and **Filter** (Name) can be used to further refine assignment targeting beyond Entra group membership:

* For the **Corel Pilot Users** group, **Filter Mode** is set to **None**. No Intune filter is applied, so the assignment targets all devices in the group without additional filtering.
* For the **Corel All Users** group, **Filter Mode** is set to **Include** with the **Microsoft Devices** filter. The assignment applies only to devices in the group that match the **Microsoft Devices** filter criteria.
* For the **dBase All Users** group, **Filter Mode** is set to **Exclude** with the **Dell Devices** filter. The assignment applies to the group except for devices that match the **Dell Devices** filter.

<figure><img src="../../../../.gitbook/assets/image (4817).png" alt="Filter Name Example" width="563"><figcaption></figcaption></figure>

### Select Filter

Whenever [Filter Mode](assignment-options.md#filter-mode-and-filter-name) is set to either **Include** or **Exclude**, the default **n/a** entry becomes a hyperlink. When you click this link, the **Select Filter** dialog opens, showing all of the Intune device filters available in your tenant (which you can search and filter) and select the appropriate filter. Only one filter can be selected per assignment.

<figure><img src="../../../../.gitbook/assets/image (2) (1).png" alt="&#x27;Select Filter&#x27; dialog" width="563"><figcaption></figcaption></figure>

### Steps to Select a Filter

To select a Filter:

1. Set **Filter Mode** to **Include** or **Exclude** on the assignment.
2. Click the **n/a** value in the **Filter** column to open the **Select Filter** dialog.
3. Use **Search** or **Refresh** to locate the required filter and select it from the list.
4. Click **OK** to apply the filter.

### Filter Validation

When configuring assignments, Publisher validates that a filter is selected whenever **Filter Mode** is set to **Include** or **Exclude**.

If **Filter Mode** is set to **Include** or **Exclude** and the **Filter** column remains set to **n/a**, a validation error is triggered. This indicates that a filter mode has been selected, but no Intune device filter has been assigned.

In the example below:

1. **Filter Mode** has been set to **Exclude** for the **dBase All Users** assignment, but no filter has been configured in the **Filter** field.
2. The **Validation errors detected** message is displayed.
3. Hovering over this displays the error message giving the details.

<figure><img src="../../../../.gitbook/assets/image (4818).png" alt="Filter Validation error" width="563"><figcaption></figcaption></figure>

## Available Time

The **Available Time** field controls when an Intune application or update becomes available to devices for a specific assignment:

* For **Required for enrolled devices** assignments, content download begins at the available time.
* For **Available for enrolled devices** assignments, the application becomes visible in the Company Portal at the available time.

If no custom availability is configured, the default behavior is **As soon as possible**, which makes the assignment available as soon as policy is received.

{% hint style="danger" %}
**Important**

Intune has a known issue when multiple **Required** assignments exist for the same application and different availability times are configured.

If one assignment uses **As soon as possible** and another assignment uses a future availability time, the Intune Management Extension may delay content download and installation until the later availability time is reached.

This behavior is documented in a Patch My PC blog at [https://patchmypc.com/blog/intune-asap-assignments-bug/](https://patchmypc.com/blog/intune-asap-assignments-bug/).

A recommended workaround is to configure availability as **Publishing date plus 0 days**. This sets the availability to the application publish time, which is already in the past when the device evaluates the assignment. As a result, Intune processes the assignment immediately and avoids delays caused by mixed availability configurations.
{% endhint %}

### Steps to Configure an Available Time

To configure an **Available Time**:

1. [Add](add-remove-assignment.md#add-an-assignment) or [Edit](add-remove-assignment.md#edit-an-assignment) an assignment.
2. On the **Manage Assignments** dialog, click the relevant tab for the type of assignment you want to configure the **Available Time** for.
3. In the **Available Time** column, click **As soon as possible** beside the relevant assignment.

<figure><img src="../../../../.gitbook/assets/image (4819).png" alt="Clicking &#x27;As soon as possible&#x27; beside the relevant assignment" width="563"><figcaption></figcaption></figure>

4. On the **Edit Availability** screen, select the **Application availability** checkbox and configure the number of **Days** and time as required.

<figure><img src="../../../../.gitbook/assets/image (4821).png" alt="configuring the &#x27;Edit Availability&#x27; screen" width="445"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The **Application availability** and **Installation deadline** settings can appear on the same dialog, depending on the assignment type:

* **Required for enrolled devices** assignments show both **Application availability** and **Installation deadline** settings. **Application availability** controls when content is downloaded. **Installation deadline** controls when installation is enforced.
* **Available for enrolled devices** assignments show **Application availability** only. Deadlines are not supported. **Application availability** controls when the app appears in the Company Portal and when users can start installation.
* **Uninstall for enrolled devices** assignments show **Installation deadline** only. Availability is not used for uninstall intent. **Installation deadline** controls when the uninstall is enforced.
{% endhint %}

5. Choose **UTC** or **Device time** **zone** as required.
6. Click **OK** to save the configuration.

The updated availability setting is shown in the **Available Time** column and is applied during the next Publisher [Synchronization](../../../manage/sync-schedule-tab/).

### Availability Time Processing Behavior

Availability time should be treated as an earliest eligible time, not a guaranteed execution time.

When a device receives policy, the Intune Management Extension processes assignments through the Global Resource Scheduler (GRS). Assignment evaluation is not continuous. Instead, a background processing cycle runs periodically, every 8 hours.

Because of this behavior, even if you configure a specific date and time for availability, the assignment may not be processed at that exact time. As long as the device is powered on, the assignment can be actioned any time from the configured availability onward, up to several hours later.

This is a limitation of the Intune Management Extension scheduling model and not a limitation of the Publisher configuration.

When setting a specific availability time, plan for a possible delay window and avoid assuming precise execution at the configured minute.

## Deadline

The **Deadline** field controls when installation or removal is enforced for an assignment.

{% hint style="danger" %}
**Important**

Deadlines are only supported for **Required for enrolled devices** and **Uninstall for enrolled devices** assignments. Deadlines are not supported for **Available for enrolled devices** assignments.
{% endhint %}

* For **Required for enrolled devices assignments**, installation is enforced when the deadline is reached.
* For **Uninstall for enrolled devices assignments**, removal of the application is enforced when the deadline is reached.

If **no deadline is configured**, enforcement still occurs, but it happens after the **Available Time** is reached. In this case, installation or uninstall is processed based on availability and policy evaluation scheduling timing rather than a fixed enforcement deadline.

{% hint style="danger" %}
**Important**

When multiple **Required** assignments exist for the same application and devices belong to more than one assignment, Intune determines applicability based on availability first. If availability processing is delayed due to a known bug, deadline enforcement is also delayed because the assignment is not considered applicable until availability is reached.

In scenarios where one assignment uses **As soon as possible** and another uses a future availability time, Intune may defer both content download and subsequent deadline enforcement until the later availability time is reached.

This behavior is an Intune platform limitation and is documented in the Patch My PC blog [https://patchmypc.com/blog/intune-asap-assignments-bug/](https://patchmypc.com/blog/intune-asap-assignments-bug/).

To ensure predictable deadline enforcement, avoid mixing **As soon as possible** with future availability times. A recommended approach is to configure availability as **Publishing date plus 0 days**, which sets availability to the publish time and allows both availability processing and deadline enforcement to occur as expected.
{% endhint %}

### Steps to Configure a Deadline

To configure a **Deadline**:

1. [Add](add-remove-assignment.md#add-an-assignment) or [Edit](add-remove-assignment.md#edit-an-assignment) an assignment.
2. On the **Manage Assignments** dialog, click the relevant tab for the type of assignment you want to configure the **Deadline** for.
3. In the **Deadline** column, click **Not configured** beside the relevant assignment.

<figure><img src="../../../../.gitbook/assets/image (4822).png" alt="Clicking &#x27;Not configured&#x27; beside the relevant assignment." width="563"><figcaption></figcaption></figure>

4. On the **Edit Availability & Deadline** screen, select the **Installation deadline** checkbox and configure the number of **Days** and time as required.

<figure><img src="../../../../.gitbook/assets/image (4823).png" alt="Configuring the deadline" width="448"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The **Application availability** and **Installation deadline** settings can appear on the same dialog, depending on the assignment type:

* **Required for enrolled devices** assignments show both **Application availability** and **Installation deadline** settings. **Application availability** controls when content is downloaded. **Installation deadline** controls when installation is enforced.
* **Available for enrolled devices** assignments show **Application availability** only. Deadlines are not supported. **Application availability** controls when the app appears in the Company Portal and when users can start installation.
* **Uninstall for enrolled devices** assignments show **Installation deadline** only. Availability is not used for uninstall intent. **Installation deadline** controls when the uninstall is enforced.
{% endhint %}

5. Choose **UTC** or **Device time** **zone** as required.
6. Click **OK** to save the configuration.

The updated availability setting is shown in the **Deadline** column and is applied during the next Publisher [Synchronization](../../../manage/sync-schedule-tab/).

### Deadline Processing Behavior

A Deadline should be treated as the earliest enforcement time, not a guaranteed execution time.

After the deadline is reached, the Intune Management Extension evaluates enforcement through the Global Resource Scheduler. Enforcement checks are not continuous. Instead, a background processing cycle runs periodically, every 8 hours.

Because of this behavior, even if you configure a specific date and time for a deadline, installation or uninstall enforcement may not occur at that exact time. As long as the device is powered on, enforcement can occur any time after the configured deadline, up to several hours later.

This is a limitation of the Intune Management Extension scheduling model and not a limitation of the Publisher configuration.

When setting a specific deadline, plan for a possible enforcement delay window and avoid assuming precise execution at the configured minute.

## Grace Period

The value defined in the **Grace Period** field controls how long a device can delay a required reboot after an application install or uninstall is enforced.

During a configured grace period, the user can continue working before the Win32 app indicates that a reboot becomes mandatory.

### Steps to Configure a Grace Period

To configure a **Grace Period**:

1. [Add](add-remove-assignment.md#add-an-assignment) or [Edit](add-remove-assignment.md#edit-an-assignment) an assignment.
2. On the **Manage Assignments** dialog, click the relevant tab for the type of assignment you want to configure the **Grace Period** for.
3. In the **Grace Period** column, click **Not configured** beside the relevant assignment.

<figure><img src="../../../../.gitbook/assets/image (4825).png" alt="Clicking &#x27;Not configured&#x27; beside the relevant assignment." width="563"><figcaption></figcaption></figure>

4. On the **Edit Availability** screen, under the **Restart Settings** section, select the **Configure restart grace period** checkbox and configure the settings as required.

<figure><img src="../../../../.gitbook/assets/image (4826).png" alt="Configuring the restart grace period settings" width="448"><figcaption></figcaption></figure>

5. Optionally select the **Allow snooze** checkbox and set the **Snooze duration**.
6. Choose **UTC** or **Device time** **zone** as required.
7. Click **OK** to save the configuration.

The updated availability setting is shown in the **Grace Period** column and is applied during the next Publisher [Synchronization](../../../manage/sync-schedule-tab/).

{% hint style="info" %}
**Note**

For a deeper explanation of how Intune processes restart grace periods, notification behavior, countdown timing, and enforcement nuances, review the Patch My PC blog at [https://patchmypc.com/blog/intune-s-restart-grace-period/](https://patchmypc.com/blog/intune-s-restart-grace-period/).
{% endhint %}

### Restart Grace Period Behavior

When a restart is required, the Intune Management Extension displays Windows toast notifications informing the user that a restart is pending.

As the grace period progresses, Intune escalates the user experience. This includes toast notifications and a restart countdown dialog that appears shortly before enforcement. The **Restart countdown** setting controls how long before enforcement the countdown dialog is shown. The default value is **15 minutes**, giving the user a final opportunity to save work.

If **Allow snooze** is enabled, users can temporarily delay the reboot. The **Snooze duration** determines how long the reboot is postponed before notifications resume.

### Installer Dependency

The restart grace period is enforced only when the installer explicitly signals that a reboot is required.

If the installer does not return a reboot-required exit code, Intune does not enforce a restart, even if a restart grace period is configured. In this scenario, no reboot countdown or enforcement occurs.

This behavior ensures that restart enforcement is predictable and based on the installer’s actual reboot requirement, with the Intune Management Extension honoring that signal.

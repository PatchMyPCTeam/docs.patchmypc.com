# Add/Remove an Assignment

_Applies to: Patch My PC Publisher V2.x_
\
Available at level: All Custom Products, All Products, Vendor, Product
\
Available on tab: Intune Apps, Intune Updates

## Add an Assignment

When you select **Add Assignment**, a window opens that displays the Entra ID groups in your tenant. You can filter the list to quickly locate the groups you want to target and select one or more groups at the same time.

![Add Assignment](/_images/image-(4024).png "Add Assignment")

After an assignment is added, it appears in the assignment list. Each column value such as Name, Mode, Notification, Delivery Optimization priority, Availability, Deadline, or Restart grace period can be selected to open the Assignment editor. The Assignment editor allows you to configure detailed behavior for that specific assignment.

### Add Assignment Form

The Add Assignment form is used to select Entra groups that will be targeted for an Intune application or update assignment in the Publisher. This form appears when you select **Add Assignment** from the Manage Application Assignments window.

The form displays a searchable list of Entra groups available in your tenant. You can select one or more groups and add them to the assignment in a single action.

![Select Entra Groups](/_images/image-(4025).png "Select Entra Groups")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>All filters automatically work like a contains search and match text anywhere in the field.</p>
<p>Use explicit wildcards such as \* and ? for more precise matching. Filters are evaluated server side against Entra groups.</p>
</blockquote>

**Search**
\
Allows you to search for Entra groups by name or description. Filters support **Contains and Starts With**. The **Contains** search filter is selected by default. **Reload** refreshes the group list using the current Search box content while preserving any selected groups.

**Name like**
\
Filters the group list by matching text in the group name from the results returned by the Search.

**Description like**
\
Filters the group list by matching text in the group description from the results returned by the Search.

**Load More Groups**
\
When the Add Assignment form first opens, the Publisher loads an initial limited set of Entra groups. This initial list is intentionally constrained for performance reasons and typically includes the first set of \~20 groups returned by Entra ID.

**Load All Groups**
\
Loads all Entra groups from Entra ID and replaces the current search results. This performs a full retrieval of groups, still limited to the first set of \~20 groups returned by Entra ID, but does not clear any existing selections.

**Built in Targets**
\
Allows selection of the built in Intune targets **All Users** and **All Devices**.

**Selected Groups Counter**
\
Shows the number of groups currently selected.

### Steps to Add an Assignment

1. Select **Add Assignment** from the Manage Application Assignments form.
2. Use the search or filters to locate the required Entra groups.
3. Select one or more groups or built in targets.
4. Click **OK** to add the assignment.

After the assignment is added, it appears in the assignment list where you can configure assignment options such as mode notifications availability deadlines and restart grace period.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>All changes made in this window are applied during the next Publisher [synchronization](../../administration/sync-schedule.md). Changes are not applied immediately to Win32 apps that already exist in Intune.</p>
<p>If you want to make changes to assignments for applications and updates that have already been published to Intune, use the [Intune Application Manager](../../administration/intune-apps-updates/form-controls/intune-application-manager.md) instead.</p>
</blockquote>

## Remove an Assignment

Selecting **Remove Assignment** removes the selected assignment from the Publisher configuration. You can select multiple assignments and remove them in a single action.

The removal takes effect during the next Publisher synchronization. Removing an assignment here does not delete the Entra ID group and does not immediately delete the assignment from Intune.

### Steps to Remove an Assignment

1. Open the Manage Application Assignments form.
2. Select one or more assignments from the assignment list. Use **Shift** to select a range of assignments or **Ctrl** to select multiple individual assignments.
3. Select **Remove Assignment**.
4. Click **OK** to save the changes.

The removed assignments are deleted from the Publisher configuration and will no longer be recreated for future versions. The change is applied during the next Publisher synchronization.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>When an assignment is removed in the Publisher, it will not be recreated for future application or update versions. However, the assignment that already exists in Intune remains unless it is manually removed.</p>
<p>All changes made in this window are applied during the next Publisher [synchronization](../../administration/sync-schedule.md). Changes are not applied immediately to Win32 apps that already exist in Intune.</p>
<p>If you want to make changes to assignments for applications and updates that have already been published to Intune, use the[ Intune Application Manager](../../administration/intune-apps-updates/form-controls/intune-application-manager.md) instead.</p>
</blockquote>

## Override Manual Assignment Changes

By default, assignment settings such as Mode, Notification, and Restart grace period are configured when a new Win32 app is first published. During future syncs, the Publisher does not overwrite manual changes made directly in Intune for existing assignments.

![Override Manual Assignment Changes](/_images/image-(72).png "Override Manual Assignment Changes")

Enabling **Override manual assignment changes made in Intune during the synchronization of the Publisher** instructs the Publisher to reapply the configured assignment settings on each sync.

When this option is enabled:

* Any manual changes made in Intune to assignment properties will be overwritten.
* Assignment settings defined in the Publisher will become the authoritative configuration.
* Existing assignments will be updated to match the current Publisher configuration during sync.

When this option is not enabled:

* Manual changes made in Intune will be preserved.
* The Publisher will not modify assignment properties for existing assignments during synchronization.

Use this option when you want assignment configuration to be centrally managed and consistently enforced from the Publisher.

## Copy Assignments from Previous Versions Consideration

When the [Copy the requirements from previously created applications or updates when an updated application is created](../../administration/intune-apps-updates/options/application-options.md#copy-the-assignments-from-previously-created-applications-when-an-updated-application-is-created) option is enabled in global [Options](../../administration/intune-apps-updates/options/), Intune assignments from the previous application or update version are automatically copied forward when a new version is published.

This behavior applies even if assignments were removed using the Manage Application Assignments option. In this scenario, the Publisher does not recreate the removed assignments, but copies them forward from the previous version as part of the Win32 app creation process.

If you do not want assignments to be copied forward, remove the unwanted assignments from the existing version in Intune by using the [Intune Application Manager](../../administration/intune-apps-updates/form-controls/intune-application-manager.md). This ensures the previous version no longer contains those assignments, preventing them from being inherited by newer versions.

Alternatively, you can disable the copy forward behavior entirely by turning off the [Copy the requirements from previously created applications or updates when an updated application is created](../../administration/intune-apps-updates/options/application-options.md#copy-the-requirements-from-previously-created-applications-or-updates-when-an-updated-application-is) option is enabled in global [Options ](../../administration/intune-apps-updates/options/)form,

You can also override this behavior at a more granular level. The copy forward setting can be overridden at the Vendor or Product level by using the [Override Win32 Application Options](../override-win32-application-options.md) right-click customization option. This allows you to control assignment inheritance for specific products or vendors without changing the global configuration.

Carefully review copy forward settings to ensure assignment behavior aligns with your intended deployment strategy, especially when managing assignment removals across versions.
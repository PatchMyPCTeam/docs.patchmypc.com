# Add/Remove an Assignment in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_Available on tab: Intune Apps, Intune Updates_

The **Manage Assignments** right-click option in Patch My PC (PMPC) Publisher allows you to manage the assignments for an Intune App/Update.

When you select the **Manage Assignments** right-click option, the **Manage&#x20;**_**\<intune\_type>**_**&#x20;Assignments for&#x20;**_**\<scope>**_ dialog is displayed, where:

* _**\<intune\_type>**_ is either **Application** or **Update** (depending on whether you selected an Intune App or Update)
* _**\<scope>**_ is the level in the Product Tree for the object you right-clicked on.

For example, right-clicking the **Google Chrome (MSI-x64)** Intune App opens the **Manage Application Assignments for Google Chrome (MSI-x64)** dialog.

<figure><img src="../../../../.gitbook/assets/image (4807).png" alt="&#x27;Manage Application Assignments for Google Chrome (MSI-x64)&#x27; dialog" width="563"><figcaption></figcaption></figure>

Whereas right-clicking **Google, Inc.** in the **Intune Updates** node opens the **Manage Update Assignments for Google, Inc.** dialog.

<figure><img src="../../../../.gitbook/assets/image (4808).png" alt="&#x27;Manage Update Assignments for Google, Inc.&#x27; dialog" width="563"><figcaption></figcaption></figure>

From the **Manage&#x20;**_**\<intune\_type>**_**&#x20;Assignments for&#x20;**_**\<scope>**_ dialog you can:

* [Add an Assignment](add-remove-assignment.md#add-an-assignment)
* [Edit an Assignment](add-remove-assignment.md#edit-an-assignment)
* [Remove an Assignment](add-remove-assignment.md#remove-an-assignment)

## Add an Assignment

When you click **Add Assignment**, the **Select Entra ID Groups** dialog appears, displaying all of the Entra ID groups in your Intune tenant.

<figure><img src="../../../../.gitbook/assets/image (4809).png" alt="&#x27;Select Entra ID Groups&#x27; dialog" width="563"><figcaption></figcaption></figure>

Using the capabilities on this dialog, you can use the:

* **Search** field to enter a search query to search for Entra ID groups by name or description. Use the filter dropdown and select **Contains** (default) or **Starts With** to help narrow your search even further, then click **Search**.&#x20;
* **Name like** field to filter the group list by matching text in the group name from the results returned by the Search.
* **Description like** field to filter the group list by matching text in the group description from the results returned by the Search.

{% hint style="success" %}
**Tip**

All filters automatically work like a contains search and match text anywhere in the field.

Use explicit wildcards such as **\*** and **?** for more precise matching. Filters are evaluated server-side against Entra ID groups.
{% endhint %}

* **Reload** button to refresh the group list using the current **Search** box content while preserving any selected groups.
* **Load More Groups** button to load more than the initial limited set of Entra ID groups. This initial list is intentionally constrained for performance reasons and typically includes the first set of \~20 groups returned by Entra ID.
* **Load All Groups** button to load all Entra ID groups from Entra ID and replaces the current search results. This performs a full retrieval of groups, still limited to the first set of \~20 groups returned by Entra ID, but does not clear any existing selections.
* **Built-in targets** checkboxes to select the built-in **All users** and **All devices** Intune targets.

The **Selected&#x20;**_**x**_**&#x20;groups** counter shows the number of groups currently selected, as you can select more than one group from the **Select Entra ID Groups** dialog.

Once you have selected the required groups and clicked **OK** on the **Select Entra ID Groups** dialog, the assignment is added to the **Manage Assignments** dialog.

<figure><img src="../../../../.gitbook/assets/image (4810).png" alt="Added assignment" width="563"><figcaption></figcaption></figure>

At this point, you can either click **OK** to close the **Manage Assignments** dialog or modify the settings for a field (where supported) by either clicking the:

* Down arrow and selecting the required option from the dropdown.
* Link under the field value to open an edit dialog, where you can configure the required settings.

{% hint style="info" %}
**Note**

See [Assignment Options](assignment-options.md) for more details on the available options.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (4812).png" alt="Edit dialog" width="446"><figcaption></figcaption></figure>

### Steps to Add an Assignment

To add an assignment:

1. Right-click the relevant object in the Product Tree and select **Manage Assignments**
2. On the **Manage Assignments** dialog, click the relevant tab for the type of assignment you want to add.
3. Click **Add Assignment**
4. On the **Select Entra ID Groups** dialog, select the relevant Entra ID groups/built-in groups, then click **OK**.
5. Configure [any required settings ](assignment-options.md)on the **Manage Assignments** dialog (such as notifications,  availability deadlines, the restart grace period, etc), then click **OK**.

{% hint style="danger" %}
**Important**

All changes made in this window are applied during the next Publisher [Synchronization](../../../manage/sync-schedule-tab/). Changes are not applied immediately to Win32 apps that already exist in Intune.

If you want to make changes to assignments for applications and updates that have already been published to Intune, use the [Intune Manager](../../../manage/intune-tabs/intune-manager.md) instead.
{% endhint %}

## Edit an Assignment

Once an assignment has been [added](add-remove-assignment.md#add-an-assignment), it can be edited by:

1. Right-click the relevant object in the Product Tree and select **Manage Assignments**
2. On the **Manage Assignments** dialog, click the relevant tab for the type of assignment you want to edit.
3. Click **Add Assignment** to [add an additional assignment](add-remove-assignment.md#steps-to-add-an-assignment) or **Remove Assignment** to [remove an existing assignment](add-remove-assignment.md#steps-to-remove-an-assignment).
4. Modify [the settings](assignment-options.md) for an existing assignment (where supported) by either clicking the down arrow (and selecting the required option from the dropdown) or clicking the link under the field value to open an edit dialog where you can configure the required settings.&#x20;
5. Click **OK** on the **Manage Assignments** dialog to save your settings.

## Remove an Assignment

Clicking **Remove Assignment** removes the selected assignment from Publisher. You can select multiple assignments and remove them in a single action.

The removal takes effect during the next Publisher synchronization. Removing an assignment here does not delete the Entra ID group and does not immediately delete the assignment from Intune.

### Steps to Remove an Assignment

To remove an assignment:

1. Right-click the relevant object in the Product Tree and select **Manage Assignments**
2. On the **Manage Assignments** dialog, click the relevant tab for the type of assignment you want to remove.
3. Select the assignment(s) you want to delete and click **Remove Assignment**\
   \
   The assignments are removed.
4. Click **OK** to close the **Manage Assignments** dialog.

Any assignments removed are deleted from Publisher's configuration and will no longer be recreated for future versions. The change is applied during the next Publisher synchronization.

{% hint style="danger" %}
**Important**

When an assignment is removed in Publisher, it will not be recreated for future application or update versions. However, the assignment that already exists in Intune remains unless it is manually removed.

All changes made in this window are applied during the next Publisher [Synchronization](../../../manage/sync-schedule-tab/). Changes are not applied immediately to Win32 apps that already exist in Intune.

If you want to make changes to assignments for applications and updates that have already been published to Intune, use the [Intune Manager](../../../manage/intune-tabs/intune-manager.md) instead.
{% endhint %}

## Override Manual Assignment Changes

By default, assignment settings such as Mode, Notification, and Restart grace period are configured when a new Win32 app is first published. During future syncs, Publisher does not overwrite manual changes made directly in Intune for existing assignments.

However, enabling the **Override manual assignment changes made in Intune during the synchronization of the Publisher** option instructs Publisher to reapply the configured assignment settings on each sync.

<figure><img src="../../../../.gitbook/assets/image (4811).png" alt="&#x27;Override manual assignment changes made in Intune during the synchronization of the Publisher&#x27; option" width="563"><figcaption></figcaption></figure>

When the **Override manual assignment changes made in Intune during the synchronization of the Publisher** option is enabled:

* Any manual changes made in Intune to assignment properties will be overwritten.
* Assignment settings defined in Publisher will become the authoritative configuration.
* Existing assignments will be updated to match the current Publisher configuration during sync.

When this option is not enabled:

* Manual changes made in Intune will be preserved.
* Publisher will not modify assignment properties for existing assignments during synchronization.

Use this option when you want assignment configuration to be centrally managed and consistently enforced from the Publisher.

## Copy Assignments from Previous Versions Consideration

When the [Copy assignments from the previous release when a new application or update is published](../../../manage/intune-tabs/intune-options/publishing-options.md#copy-assignments-from-the-previous-release-when-a-new-application-or-update-is-published) option is enabled under the [Publishing Options](../../../manage/intune-tabs/intune-options/publishing-options.md) section of the [Intune Options](../../../manage/intune-tabs/intune-options/) tab, Intune assignments from the previous application or update version are automatically copied forward when a new version is published.

This behavior applies even if assignments were removed using the **Manage Assignments** option. In this scenario, Publisher does not recreate the removed assignments, but copies them forward from the previous version as part of the Win32 app creation process.

If you do not want assignments to be copied forward, remove the unwanted assignments from the existing version in Intune by using [Intune Manager](../../../manage/intune-tabs/intune-manager.md). This ensures the previous version no longer contains those assignments, preventing them from being inherited by newer versions.

Alternatively, you can disable the copy forward behavior entirely by disabling the [Copy requirements from previous release when a new application or update is published](../../../manage/intune-tabs/intune-options/publishing-options.md#copy-requirements-from-previous-release-when-a-new-application-or-update-is-published) option under the [Publishing Options](../../../manage/intune-tabs/intune-options/publishing-options.md) section of the [Intune Options](../../../manage/intune-tabs/intune-options/) tab.

{% hint style="success" %}
**Tip**

You can also override this behavior at a more granular level by using the [Override Win32 Options](../override-win32-options.md) right-click customization option at the Vendor or Product level. This allows you to control assignment inheritance for specific products or vendors without changing the global configuration.
{% endhint %}

{% hint style="danger" %}
**Important**

Carefully review copy forward settings to ensure assignment behavior aligns with your intended deployment strategy, especially when managing assignment removals across versions.
{% endhint %}

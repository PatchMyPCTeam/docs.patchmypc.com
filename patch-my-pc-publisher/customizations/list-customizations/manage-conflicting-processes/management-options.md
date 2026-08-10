# Management Options section of Manage Conflicting Processes in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_\
_Available on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

{% hint style="danger" %}
**Important**

This article has not been updated for Version 3.x. Once it has, this banner will be removed.
{% endhint %}

The **Management Options** section allows you to control which running processes are evaluated for conflicting process management and configure the notification branding.

<figure><img src="../../../../.gitbook/assets/image (3981).png" alt="Management Options" width="525"><figcaption></figcaption></figure>

## Manage process list

The process list defines the executable names that are checked when determining whether an application is in use during an update.

The default process list is populated automatically based on the processes defined in the Patch My PC catalog for the selected product. These defaults represent the processes that are known to prevent the application from updating successfully while running.

You can add additional process names if your environment uses processes that should also be considered conflicting. You can also remove processes if required, although this is generally not recommended unless you are certain the process does not interfere with updates.

<figure><img src="../../../../.gitbook/assets/image (3982).png" alt="Manage process list" width="375"><figcaption></figcaption></figure>

Use the process list to define which running executables are treated as conflicting during update installation.

1. Select **Manage process list** from the [Management Options](management-options.md#management-options) section.
2. Review the default processes shown. These are populated automatically from the Patch My PC catalog.
3. Select the **plus** icon to add an additional process name if needed.
4. Select an existing process and choose the **minus** icon to remove it if appropriate.
5. Select **Reset** to restore the list to the default processes defined in the Patch My PC catalog.
6. Select **OK** to save changes or **Cancel** to discard them.

## Manage default settings

Click this button to open the **Conflicting Process UI Settings** window to customize the end user notification experience shown when an application must be closed to complete an update.

For detailed configuration steps and examples, see [Branding Configuration](../../../../patch-my-pc-publisherv2/customizations-right-click-options/manage-conflicting-processes/branding-configuration.md).

# Disable Self-Updater option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Products, Vendor, Product_\
_Available on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Disable Self-Updater** right-click option in Patch My PC (PMPC) Publisher disables a product’s built-in automatic update feature.

When enabled, Publisher applies the required configuration to prevent the product from updating itself. This may include actions such as setting a registry value or modifying a scheduled task, depending on how the product implements self-updating.

{% hint style="danger" %}
**Important**

Disabling this option later in Publisher does not remove or reverse the configuration previously applied to devices.&#x20;

Publisher does not attempt to revert these settings because it cannot reliably determine whether the configuration was originally applied by Patch My PC ScriptRunner (that manages the installation), or by a customer-managed script or policy.

As a result, changes to this option only apply to new installations or devices that have not yet received the configuration.&#x20;

Devices that already have the self-updater disabled will retain the existing configuration.

To re-enable a product’s automatic update feature on existing devices, you must apply your own script or policy to manually reverse the configuration that was applied.
{% endhint %}

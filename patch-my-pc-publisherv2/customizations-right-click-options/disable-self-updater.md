# Disable Self-Updater

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Products, Vendor, Product_
\
_Available on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

This option disables a product’s built in automatic update feature.

![Disable Self-Updater](/_images/image-(4009).png "Disable Self-Updater")

When this option is enabled, the Publisher applies the required configuration to prevent the product from updating itself. This may include actions such as setting a registry value or modifying a scheduled task, depending on how the product implements self updating.

## Important Behavior

Disabling this option later in the Publisher does not remove or reverse the configuration that was previously applied to devices. The Publisher does not attempt to revert these settings because it cannot reliably determine whether the configuration was originally applied by Patch My PC ScriptRunner, which manages the installation, or by a customer managed script or policy.

As a result, changes to this option only apply to new installations or devices that have not yet received the configuration. Devices that already have the self updater disabled will retain the existing configuration.

To re-enable a product’s automatic update feature on existing devices, you must apply your own script or policy to manually reverse the configuration that was applied.
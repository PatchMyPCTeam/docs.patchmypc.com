# Override Win32 Application Options

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: Vendor, Product_\
_&#x41;vailable on tab: Intune Apps, Intune Updates_

## Overview

**Override Win32 Application Options** allows you to override the global Win32 application options for a specific vendor or product. It is used when certain Intune applications or updates require different behavior than what is defined globally.

![Override Win32 Application Options](/_images/image-(4058).png)

Global Win32 app options are configured on the [Intune Apps and Intune Updates](../administration/intune-apps-updates/) tab by selecting [Options](../administration/intune-apps-updates/options/). These settings control behaviors such as assignment copying, retention of previous versions, dependency handling, runtime limits, and cleanup of older apps or updates.

In some scenarios, applying the same behavior to every application is not ideal. Override Win32 Application Options lets you customize these behaviors at the vendor or product level without changing your global defaults.

## When Overrides Are Useful

Overrides are especially useful for applications that update frequently, such as web browsers.

Products like Google Chrome, Microsoft Edge, and Mozilla Firefox release updates often. Issues introduced by these updates may not be identified immediately. If your global retention setting keeps only a small number of previous versions, the version you want to roll back to may no longer be available when a problem is discovered.

By configuring a product level override, you can retain more versions for specific applications. For example, you might retain five previous versions of Chrome while keeping a global default of two for all other apps. This provides additional time for validation and a safer rollback path for frequently updated software.

## Supported Override Options

The available override options differ slightly depending on whether you are working with Intune Apps or Intune Updates.

**Applies to Intune Apps and Intune Updates**

* Copy the assignments from previously created applications or updates
* Delete the assignments from previously created applications or updates
* Update application dependencies
* Copy the requirements from previously created applications or updates
* Configure maximum runtime of Win32 applications

**Applies to Intune Apps only**

* Enable Allow available uninstall
* Update Enrollment Status Page associations
* Delete any previously created applications when an updated application is published
* Retain up to a specified number of previously created applications

**Applies to Intune Updates only**

* Delete any previously created updates when a new update is published
* Retain up to a specified number of previously created updates

Configuring Overrides

Overrides configured here take precedence over the global options defined on the Intune Apps and Intune Updates tab and are applied only to the selected vendor or product during publishing.

![Override Win32 Application Options](/_images/image-(4059).png)

To Configure a Win32 Application Option Override:

1. Right-click the Vendor or Product you want to customize.
2. Select **Override Win32 Application Options**.
3. Review the available options based on whether you are configuring an app or an update.
4. Enable or disable the required settings to override the global behavior.
5. Click **OK** to save the configuration.

The override is evaluated and applied during the next Publisher [synchronization](../administration/sync-schedule.md) and affects only the selected vendor or product.

> Note
>
> For more details about Application and Retention Settings, use the \[Intune Apps/Updates Global Options]\(../administration/intune-apps-updates/options/application-options.md) page for reference.
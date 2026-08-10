# Override Win32 Options in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: Vendor, Product_\
_&#x41;vailable on tab: Intune Apps, Intune Updates_

The **Override Win32 Options** right-click option in Patch My PC (PMPC) Publisher allows you to override the global Win32 application options for a specific vendor or product when certain Microsoft Intune applications or updates require different behavior than what is defined globally.

These settings control behaviors such as assignment copying, retention of previous versions, dependency handling, runtime limits, and cleanup of older apps or updates.

In some scenarios, applying the same behavior across all applications is not ideal. The **Override Win32 Options** lets you customize these behaviors at the Vendor or Product level without changing your global defaults.

## When Overrides Are Useful

Overrides are especially useful for applications that update frequently, such as web browsers.

Products like Google Chrome, Microsoft Edge, and Mozilla Firefox release updates often. Issues introduced by these updates may not be identified immediately.

If your global retention setting keeps only a small number of previous versions, the version you want to roll back to may no longer be available when a problem is discovered.

By configuring a product-level override, you can retain more versions for specific applications. For example, you might retain five previous versions of Chrome whilst keeping a global default of two for all other apps. This provides additional time for validation and a safer rollback path for frequently updated software.

## Supported Override Options

There are some common override options that [apply to both Intune Apps and Updates](override-win32-options.md#applies-to-both-intune-apps-and-updates).

There are also different override options depending on whether you are working with [Intune Apps](override-win32-options.md#intune-apps-only) or [Intune Updates](override-win32-options.md#intune-updates-only).

### **Applies to both Intune Apps and Updates**

The following **Publishing Options** apply to both Intune Apps and Updates:

* Copy assignments from the previous release when a new application or update is published
* Delete assignments from the previous release when a new application or update is published
* Copy dependencies from the previous release when a new application or update is published
* Copy requirements from the previous release when a new application or update is published
* Configure maximum runtime of Win32 applications to x minutes (120 by default)

### **Intune Apps Only**

The following **Publishing Options** apply to only Intune Apps:

* Delete any previously created applications when an updated application is published
  * Retain up to _x_ previously created applications (0 by default)
* Delay in-place updates of previously created applications by _x_ day(s) (1 by default).

### **Intune Updates Only**

The following **Publishing Options** apply to only Intune Updates:

* Delete any previously created updates when a new update is published
  * Retain up to _x_ previously created updates (0 by default)
* Delay in-place updates of previously created updates by _x_ day(s) (1 by default).

Configure Overrides

Overrides can be configured both globally under the [Publishing Options](../../manage/intune-tabs/intune-options/publishing-options.md) section of the [Intune tabs](../../manage/intune-tabs/), or by using the **Override Win32 Options** right-click option.

> \*\*Important\*\*
>
> Any overrides configured at the Vendor/Product level take precedence over the global options and are applied only to the selected vendor or product during publishing.

To configure **Override Win32 Options:**

1. Right-click the Vendor/Product you want to customize and select **Override Win32 Options**.
2. Review the available options based on whether you are configuring an app or an update.

> \*\*Note\*\*
>
> See \[Publishing Options]\(../../manage/intune-tabs/intune-options/publishing-options.md) for more information about each option.

![Override Win32 Options](/_images/image-(4778).png)

3. Configure the required settings to override the global behavior.
4. Click **OK** to save the configuration.

The override is evaluated and applied during the next Publisher [synchronization](../../manage/sync-schedule-tab/) and affects only the selected vendor or product.
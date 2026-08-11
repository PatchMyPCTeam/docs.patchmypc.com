# Policy section of Manage Conflicting Processes in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Policy** section of **Manage Conflicting Processes** defines how the Patch My PC (PMPC) Publisher handles update installation when a conflicting application process is detected on the device. These settings determine whether the update proceeds, how running applications are handled, and whether user interaction is required before installation begins.

![Manage Conflicting Processes Settings](../../../../.gitbook/assets/image-\(3965\).png)

## Perform the Installation

This option allows the update installation to proceed even if a conflicting process is detected. No attempt is made to notify the user or close the running application. This setting relies entirely on the vendor installer behavior and may result in installation failure if the application cannot be updated while running.

> \*\*Note\*\*
>
> This option is the default setting for most applications in the Patch My PC Catalog where conflicting process configuration is not required. It should only be selected for applications that are designed to be updated while running.

> \*\*Important\*\*
>
> While some applications can be updated while running, they often must be closed and reopened before the new version is actually in use. Until the application is restarted, the previous version may continue running in memory.
>
> Some customers choose to use the \[Notify the user to close the application]\(policy-section.md#notify-the-user-to-close-the-application) policy for applications, such as web browsers, to ensure they are closed before updating. This helps ensure that when the user next launches the application, it is immediately running the updated version.
>
> If an application such as a browser is frequently left open, it may remain vulnerable until it is restarted, even if the update installs successfully in the background.

## Auto-close conflicting application process before installation

This option automatically terminates the configured conflicting processes before the update installation begins. No user interaction is required.

This ensures the update can proceed successfully but may result in data loss if the user has unsaved work.

> \*\*Important\*\*
>
> Automatically closing applications is often considered a poor end user experience, as it can interrupt active work and cause loss of unsaved data. This option should be reserved for scenarios where unattended enforcement is required and update completion is prioritized over user experience.

## Skip installation when conflicting processes are in use

This option prevents the update from installing if any configured conflicting process is detected. The update is skipped and retried during the next deployment evaluation cycle.

This option is generally considered a safe approach and is appropriate for non-critical updates that should only install when the application is not actively being used. However, compliance can drift over time if the application is frequently in use and the update is repeatedly skipped.

> \*\*Note\*\*
>
> This is the default behavior configured by the Publisher for applications that must be closed to update successfully, helping reduce the risk of installation failures. By skipping the update when the application is in use, it avoids failed installations that can be difficult and time consuming to troubleshoot.

## Notify the user to close the application

This option displays a notification to the end user when a conflicting process is detected. The user is prompted to close the application before the update proceeds.

If the application is closed within the configured timeout, the installation continues. If no action is taken, the behavior depends on the configured deferral and enforcement settings.

This option provides the best balance between update reliability and user experience for applications that are commonly left open.

### Notify Timeout Configuration

The **Notify Timeout Configuration** setting controls how long the update waits for user action after a notification is displayed when a conflicting process is detected. It is used in conjunction with the policy setting to [Notify the user to close the application](policy-section.md#notify-the-user-to-close-the-application).

![Notify Timeout Configuration](../../../../.gitbook/assets/image-\(137\).png)

The timeout defines the period the user has to close the application before enforcement behavior occurs. If the application is closed within this window, the update proceeds. If no action is taken, the outcome depends on the [configured deferral and enforcement settings](policy-section.md#defer-policy).

> \*\*Important\*\*
>
> A 15 minute buffer is automatically applied to all configured timeout values. This buffer accounts for platform execution limits and is not configurable.

* **For ConfigMgr applications**, the maximum timeout is limited by the configured application run time, minus the 15 minute buffer.
* **For Intune applications and Intune updates**, the maximum supported run time is **1444 minutes**. The notification timeout is calculated as this maximum minus the 15 minute buffer.
* **For WSUS based updates**, the maximum supported run time is 5 minutes. In this scenario, the **Use maximum runtime of 5 minutes for WSUS updates** option should be selected.

Patch My PC recommends configuring a timeout of one 105 minutes, which aligns with a 120 execution window minus the 15-minute buffer.

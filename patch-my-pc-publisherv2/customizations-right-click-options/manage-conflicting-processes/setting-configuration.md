# Setting Configuration

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Policy

The **Policy** section defines how the Publisher handles update installation when a conflicting application process is detected on the device. These settings determine whether the update proceeds, how running applications are handled, and whether user interaction is required before installation begins.

![Manage Conflicting Processes Settings](/_images/image-(3965).png)

### Perform the Installation

This option allows the update installation to proceed even if a conflicting process is detected. No attempt is made to notify the user or close the running application. This setting relies entirely on the vendor installer behavior and may result in installation failure if the application cannot be updated while running.

> \*\*Note\*\*
>
> This option is the default setting for most applications in the Patch My PC Catalog where conflicting process configuration is not required. It should only be selected for applications that are designed to be updated while running.

> \*\*Important\*\*
>
> While some applications can be updated while running, they often must be closed and reopened before the new version is actually in use. Until the application is restarted, the previous version may continue running in memory.
>
> Some customers choose to use the \[Notify the user to close the application]\(setting-configuration.md#notify-the-user-to-close-the-application) policy for applications, such as web browsers, to ensure they are closed before updating. This helps ensure that when the user next launches the application, it is immediately running the updated version.
>
> If an application such as a browser is frequently left open, it may remain vulnerable until it is restarted, even if the update installs successfully in the background.

### Auto-close conflicting application process before installation

This option automatically terminates the configured conflicting processes before the update installation begins. No user interaction is required.

This ensures the update can proceed successfully but may result in data loss if the user has unsaved work.

> \*\*Important\*\*
>
> Automatically closing applications is often considered a poor end user experience, as it can interrupt active work and cause loss of unsaved data. This option should be reserved for scenarios where unattended enforcement is required and update completion is prioritized over user experience.

### Skip installation when conflicting processes are in use

This option prevents the update from installing if any configured conflicting process is detected. The update is skipped and retried during the next deployment evaluation cycle.

This option is generally considered a safe approach and is appropriate for non-critical updates that should only install when the application is not actively being used. However, compliance can drift over time if the application is frequently in use and the update is repeatedly skipped.

> \*\*Note\*\*
>
> This is the default behavior configured by the Publisher for applications that must be closed to update successfully, helping reduce the risk of installation failures. By skipping the update when the application is in use, it avoids failed installations that can be difficult and time consuming to troubleshoot.

### Notify the user to close the application

This option displays a notification to the end user when a conflicting process is detected. The user is prompted to close the application before the update proceeds.

If the application is closed within the configured timeout, the installation continues. If no action is taken, the behavior depends on the configured deferral and enforcement settings.

This option provides the best balance between update reliability and user experience for applications that are commonly left open.

#### Notify Timeout Configuration

The **Notify Timeout Configuration** setting controls how long the update waits for user action after a notification is displayed when a conflicting process is detected. It is used in conjunction with the policy setting to [Notify the user to close the application](setting-configuration.md#notify-the-user-to-close-the-application).

![Notify Timeout Configuration](/_images/image-(137).png)

The timeout defines the period the user has to close the application before enforcement behavior occurs. If the application is closed within this window, the update proceeds. If no action is taken, the outcome depends on the [configured deferral and enforcement settings](setting-configuration.md#defer-policy).

> \*\*Important\*\*
>
> A 15 minute buffer is automatically applied to all configured timeout values. This buffer accounts for platform execution limits and is not configurable.

* **For ConfigMgr applications**, the maximum timeout is limited by the configured application run time, minus the 15 minute buffer.
* **For Intune applications and Intune updates**, the maximum supported run time is **1444 minutes**. The notification timeout is calculated as this maximum minus the 15 minute buffer.
* **For WSUS based updates**, the maximum supported run time is 5 minutes. In this scenario, the **Use maximum runtime of 5 minutes for WSUS updates** option should be selected.

Patch My PC recommends configuring a timeout of one 105 minutes, which aligns with a 120 execution window minus the 15 minute buffer.

## Process Start Prevention

The **Process Restart Prevention** option prevents the end user from reopening the application while the update is in progress. This helps avoid scenarios where the application is closed for the update but immediately relaunched, which could cause the installation to fail or be delayed.

![Process Start Prevention](/_images/image-(138).png)

This option is only available at the Product level and should be used for applications where restarting the process during installation is likely to interfere with a successful update.

> \*\*Caution\*\*
>
> This setting is \*\*not recommended\*\* in most scenarios due to the potential for user disruption and residual system changes if the update process does not complete cleanly.
>
> For some applications, such as \*\*Google Chrome\*\*, enabling this setting can prevent the application from updating. These applications rely on helper processes or self update mechanisms that must be able to launch during the update process. Blocking the executable using Image File Execution Options can interfere with this behavior and cause the update to fail consistently.

### How the setting works

When Prevent the end user from opening an application while the application is updating is enabled, Patch My PC uses the Windows Image File Execution Options feature to block the application from launching.

A temporary registry entry is created for the application executable under the Image File Execution Options path. If the user attempts to launch the application during the update, they may see a message such as:

> "An update is currently being installed on your computer. Please do not try to start the application"

or

> "The requested operation requires elevation"

![Prevent the end user from opening an application](/_images/image-(3986).png)

### Potential Risk

If the ScriptRunner process is forcefully terminated or exits unexpectedly, the Image File Execution Options registry entries may not be cleaned up correctly. When this occurs, users may continue to see the blocking message even though no installation or update is actively running.\
If this happens, the registry entry for the affected process must be removed manually.

Depending on the operating system architecture and the application being blocked, you may need to check one or both of the following registry paths:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options
HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion\Image File Execution Options
```

Look for subkeys named after the blocked executable, such as `notepad++.exe`.

![Image File Execution Options registry entries](/_images/image-(3987).png)

> \*\*Note\*\*
>
> When Patch My PC ScriptRunner executes on a device, it checks for legacy Image File Execution Options entries that were created by previous Patch My PC update attempts that were not cleaned up correctly. If these entries are detected, ScriptRunner will remove them automatically.
>
> This cleanup only occurs when another Patch My PC application or update is executed on the device. If no further Patch My PC deployments run, the stale registry entries may remain in place.
>
> For this reason, if users are blocked from launching an application due to leftover Image File Execution Options entries, a manual registry cleanup or \[PowerShell based remediation]\(setting-configuration.md#powershell-based-remediation) is often required to immediately restore application access.

### **PowerShell-based Remediation**

If required, the following PowerShell commands can be used to locate and remove all Image File Execution Options entries created by Patch My PC ScriptRunner for process blocking:

```powershell
Get-ChildItem "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options" -ea SilentlyContinue |
Where-Object {
    if ($_.Property -contains "Debugger") {
        ($_ | Get-ItemProperty).Debugger -like "*PreventStart*"
    }
} | Remove-Item -Force -Recurse;

Get-ChildItem "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options" -ea SilentlyContinue |
Where-Object {
    if ($_.Property -contains "Debugger") {
        ($_ | Get-ItemProperty).Debugger -like "*PreventStart*"
    }
} | Remove-Item -Force -Recurse;

```

## Notification Policy

The **Notification Policy** options become available when the policy [Notify the user to close the application](setting-configuration.md#notify-the-user-to-close-the-application) is selected.

These settings control how end user notifications behave when a conflicting process is detected and the application is running.

![Notification Policy](/_images/image-(3979).png)

### Notification behavior

If the application to be updated is running, this setting controls how notifications are handled when Windows Focus Assist is active.

![Notification behavior](/_images/image-(3980).png)

**Discard the notification**\
When selected, the notification is suppressed while Focus Assist is enabled. No visible notification is shown to the user during this time.

The update behavior continues based on the configured [deferral settings](setting-configuration.md#defer-policy). This option minimizes user interruption but increases the likelihood that the user does not see the notification before enforcement occurs.

> \*\*Note\*\*
>
> This is the default option.

**Always show the notification**\
When selected, the notification is shown to the user even if Focus Assist is enabled.

This ensures the user is always informed that an update requires the application to be closed, but it may interrupt presentations or focus periods where Focus Assist is intentionally enabled.

**Show the notification if the deferral policy is reached**\
When selected, notifications are suppressed while Focus Assist is enabled until the deferral policy limit is reached.

Once the user has exhausted the allowed deferrals or the deferral time window has expired, the notification is shown regardless of Focus Assist. This provides a balance between respecting Focus Assist and ensuring the user is notified when enforcement is imminent.

#### Defer (Snooze) Policy

**Allow the user to defer the installation**\
This setting allows the end user to postpone the installation when a conflicting process is detected and a notification is displayed.

> \*\*Note\*\*
>
> When a user chooses to defer, the installation is recorded as a failed attempt for that evaluation cycle. The update or application will retry during the next evaluation cycle, which depends on the deployment platform being used, such as ConfigMgr software updates, ConfigMgr applications, or Intune Win32 applications.

When this option is enabled, the following deferral policies are available.

* **Indefinitely**\
  The user can defer the update without limit.

> \*\*Important\*\*
>
> This option may result in the update never being installed if the user continues to defer and should be used with caution.

* **Up to X times**\
  The user can defer the update up to the specified number of times. The minimum value is **once** and the maximum value is **999 times**.

> \*\*Note\*\*
>
> Each deferral consumes 1 count. Once the maximum number of deferrals is reached, the notification is still shown but the option to snooze or defer is no longer available. The installation will then proceed based on the remaining notification and timeout settings.

* **First notification displayed plus X days**\
  The user can defer the update for a specified number of days starting from when the first notification was displayed, or when it would have been displayed based on Focus Assist behavior. The minimum value is **1** day and the maximum value is **15** days.

> \*\*Note\*\*
>
> After the configured number of days has elapsed, the notification is shown without the option to snooze or defer.

> \*\*Tip\*\*
>
> This option is particularly useful when updates must be installed within a defined compliance window after being targeted, such as environments with Cyber Essentials Plus requirements where patches must be installed within 14 days.
>
> It allows organizations to use user notifications and deferrals early in the deployment while still enforcing installation once the allowed deferral period is reached.

* **Timeout expiration behavior**\
  This setting controls what happens if the notification timeout expires and the user takes no action. The available optiosn are:
  * **Defer the installation on behalf of the user (default)**\
    When selected, the notification closes after [the timeout expires](setting-configuration.md#notify-timeout-configuration) and the deferral is automatically applied on behalf of the user. This counts toward either the configured deferral count or deferral time window.\
    \
    If a deferral limit is reached, such as 5 missed notifications when the deferral count is set to 5, the application will be closed and the update will proceed automatically.
  * **Close the application and perform the update**\
    When selected, the notification closes after the timeout expires, the application is force closed, and the update begins immediately.\
    \
    This option enforces compliance but may negatively impact user experience. It can also cause the application to close unexpectedly if the user is not present, such as when the device is locked or unattended.

**Do not allow user deferral**\
When this option is selected, the user is not allowed to defer the installation.

If the application is still running when the notification timeout expires and no action is taken, the application is automatically closed and the update proceeds immediately. No additional prompts or deferral options are presented to the user.

## Management Options

The **Management Options** section allows you to control which running processes are evaluated for conflicting process management and configure the notification branding.

![Management Options](/_images/image-(3981).png)

### Manage process list

The process list defines the executable names that are checked when determining whether an application is in use during an update.

The default process list is populated automatically based on the processes defined in the Patch My PC catalog for the selected product. These defaults represent the processes that are known to prevent the application from updating successfully while running.

You can add additional process names if your environment uses processes that should also be considered conflicting. You can also remove processes if required, although this is generally not recommended unless you are certain the process does not interfere with updates.

![Manage process list](/_images/image-(3982).png)

Use the process list to define which running executables are treated as conflicting during update installation.

1. Select **Manage process list** from the [Management Options](setting-configuration.md#management-options) section.
2. Review the default processes shown. These are populated automatically from the Patch My PC catalog.
3. Select the **plus** icon to add an additional process name if needed.
4. Select an existing process and choose the **minus** icon to remove it if appropriate.
5. Select **Reset** to restore the list to the default processes defined in the Patch My PC catalog.
6. Select **OK** to save changes or **Cancel** to discard them.

### Manage default settings

Click this button to open the **Conflicting Process UI Settings** window to customize the end user notification experience shown when an application must be closed to complete an update.

For detailed configuration steps and examples, see [Branding Configuration](branding-configuration.md).
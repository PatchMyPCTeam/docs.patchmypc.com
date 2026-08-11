# Notification Policy section of Manage Conflicting Processes in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_\
_Available on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

{% hint style="danger" %}
**Important**

This article has not been updated for Version 3.x. Once it has, this banner will be removed.
{% endhint %}

The **Notification Policy** options become available when the policy [Notify the user to close the application](notification-policy.md#notify-the-user-to-close-the-application) is selected.

These settings control how end user notifications behave when a conflicting process is detected and the application is running.

<figure><img src="../../../../.gitbook/assets/image (3979).png" alt="Notification Policy" width="525"><figcaption></figcaption></figure>

### Notification behavior

If the application to be updated is running, this setting controls how notifications are handled when Windows Focus Assist is active.

<figure><img src="../../../../.gitbook/assets/image (3980).png" alt="Notification behavior" width="488"><figcaption></figcaption></figure>

**Discard the notification**\
When selected, the notification is suppressed while Focus Assist is enabled. No visible notification is shown to the user during this time.

The update behavior continues based on the configured [deferral settings](notification-policy.md#defer-policy). This option minimizes user interruption but increases the likelihood that the user does not see the notification before enforcement occurs.

{% hint style="info" %}
**Note**

This is the default option.
{% endhint %}

**Always show the notification**\
When selected, the notification is shown to the user even if Focus Assist is enabled.

This ensures the user is always informed that an update requires the application to be closed, but it may interrupt presentations or focus periods where Focus Assist is intentionally enabled.

**Show the notification if the deferral policy is reached**\
When selected, notifications are suppressed while Focus Assist is enabled until the deferral policy limit is reached.

Once the user has exhausted the allowed deferrals or the deferral time window has expired, the notification is shown regardless of Focus Assist. This provides a balance between respecting Focus Assist and ensuring the user is notified when enforcement is imminent.

#### Defer (Snooze) Policy

**Allow the user to defer the installation**\
This setting allows the end user to postpone the installation when a conflicting process is detected and a notification is displayed.

{% hint style="info" %}
**Note**

When a user chooses to defer, the installation is recorded as a failed attempt for that evaluation cycle. The update or application will retry during the next evaluation cycle, which depends on the deployment platform being used, such as ConfigMgr software updates, ConfigMgr applications, or Intune Win32 applications.
{% endhint %}

When this option is enabled, the following deferral policies are available.

* **Indefinitely**\
  The user can defer the update without limit.

{% hint style="danger" %}
**Important**

This option may result in the update never being installed if the user continues to defer and should be used with caution.
{% endhint %}

* **Up to X times**\
  The user can defer the update up to the specified number of times. The minimum value is **once** and the maximum value is **999 times**.

{% hint style="info" %}
**Note**

Each deferral consumes 1 count. Once the maximum number of deferrals is reached, the notification is still shown but the option to snooze or defer is no longer available. The installation will then proceed based on the remaining notification and timeout settings.
{% endhint %}

* **First notification displayed plus X days**\
  The user can defer the update for a specified number of days starting from when the first notification was displayed, or when it would have been displayed based on Focus Assist behavior. The minimum value is **1** day and the maximum value is **15** days.

{% hint style="info" %}
**Note**

After the configured number of days has elapsed, the notification is shown without the option to snooze or defer.
{% endhint %}

{% hint style="success" %}
**Tip**

This option is particularly useful when updates must be installed within a defined compliance window after being targeted, such as environments with Cyber Essentials Plus requirements where patches must be installed within 14 days.&#x20;

It allows organizations to use user notifications and deferrals early in the deployment while still enforcing installation once the allowed deferral period is reached.
{% endhint %}

* **Timeout expiration behavior**\
  This setting controls what happens if the notification timeout expires and the user takes no action. The available optiosn are:
  * **Defer the installation on behalf of the user (default)**\
    When selected, the notification closes after [the timeout expires](notification-policy.md#notify-timeout-configuration) and the deferral is automatically applied on behalf of the user. This counts toward either the configured deferral count or deferral time window.\
    \
    If a deferral limit is reached, such as 5 missed notifications when the deferral count is set to 5, the application will be closed and the update will proceed automatically.
  * **Close the application and perform the update**\
    When selected, the notification closes after the timeout expires, the application is force closed, and the update begins immediately.\
    \
    This option enforces compliance but may negatively impact user experience. It can also cause the application to close unexpectedly if the user is not present, such as when the device is locked or unattended.

**Do not allow user deferral**\
When this option is selected, the user is not allowed to defer the installation.

If the application is still running when the notification timeout expires and no action is taken, the application is automatically closed and the update proceeds immediately. No additional prompts or deferral options are presented to the user.

# Notification Policy section of Manage Conflicting Processes in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Notification Policy** section of **Manage Conflicting Processes** defines which Patch My PC (PMPC) Publisher options become available when the policy [Notify the user to close the application](policy-section.md#notify-the-user-to-close-the-application) is selected.

<figure><img src="../../../../.gitbook/assets/image (751).png" alt="&#x27;Notification Policy&#x27; section" width="501"><figcaption></figcaption></figure>

These settings control how end-user notifications behave when a conflicting process is detected and the application is running.

## Notification behavior if the application running and focus assist is enabled

If the application to be updated is running, the **Notification behavior if the application running and focus assist is enabled** setting controls how notifications are handled when Windows Focus Assist is active.

<figure><img src="../../../../.gitbook/assets/image (3980).png" alt="Notification behavior" width="488"><figcaption></figcaption></figure>

The available options are:

* [Discard the notification](notification-policy.md#discard-the-notification)
* [Always show the notification](notification-policy.md#always-show-the-notification)
* [Show the notification if the deferral policy is reached](notification-policy.md#show-the-notification-if-the-deferral-policy-is-reached)

### **Discard the notification**

If **Discard the notification** is selected (which it is by default), Focus Assist suppresses the notification while it is enabled. The user sees no visible notifications during this time.

The update behavior continues based on the configured [deferral settings](notification-policy.md#defer-policy). This option minimizes user interruption but increases the likelihood that the user does not see the notification before enforcement occurs.

### **Always show the notification**

If **Always show the notification** is selected, the user notification appears even if Focus Assist is enabled.

This ensures the user is always informed that an update requires the application to be closed, but it may interrupt presentations or focus periods where Focus Assist is intentionally enabled.

### **Show the notification if the deferral policy is reached**

If **Show the notification if the deferral policy is reached** is selected, notifications are suppressed while Focus Assist is enabled until the deferral policy limit is reached.

Once the user has exhausted the allowed deferrals or the deferral time window has expired, the notification is shown regardless of Focus Assist. This balances respecting Focus Assist with ensuring the user is notified when enforcement is imminent.

## **Allow the user to defer the installation**

The **Allow the user to defer the installation** setting allows the end user to postpone the installation when a conflicting process is detected and a notification is displayed.

{% hint style="info" %}
**Note**

When a user chooses to defer, the installation is recorded as a failed attempt for that evaluation cycle. The update or application will retry during the next evaluation cycle, depending on the deployment platform being used (such as ConfigMgr software updates, ConfigMgr applications, or Intune Win32 applications).
{% endhint %}

### Defer Policy

When this option is enabled, the following deferral policies are available.

* **Indefinitely -** The user can defer the update without limit.

{% hint style="danger" %}
**Important**

This option may result in the update never being installed if the user continues to defer, so use it with caution.
{% endhint %}

* **Up to 'x' times -** The user can defer the update up to the specified number of times. The minimum value is **1** time, and the maximum is **999** times.

{% hint style="info" %}
**Note**

Each deferral consumes one count. Once the maximum number of deferrals is reached, the notification is still shown, but the option to snooze or defer is no longer available. The installation will then proceed based on the remaining notification and timeout settings.
{% endhint %}

* **First notification displayed + 'x' days -** The user can defer the update for a specified number of days starting from when the first notification is displayed, or when it would have been displayed based on Focus Assist behavior. The minimum value is **1** day and the maximum value is **15** days.

{% hint style="info" %}
**Note**

After the configured number of days has elapsed, the notification is shown without the option to snooze or defer.
{% endhint %}

{% hint style="success" %}
**Tip**

This option is particularly useful when updates must be installed within a defined compliance window after being targeted, such as environments with Cyber Essentials Plus requirements where patches must be installed within 14 days.

It lets organizations use user notifications and deferrals early in deployment while still enforcing installation once the allowed deferral period ends.
{% endhint %}

* **If the timeout expired and no action is taken -** Controls what happens if the notification timeout expires and the user takes no action. Options available are:
  * **Defer the installation on behalf of the user** (default)\
    If selected, the notification closes after [the timeout expires](notification-policy.md#notify-timeout-configuration) and the deferral is automatically applied on behalf of the user. This counts toward either the configured deferral count or deferral time window.\
    \
    If a deferral limit is reached, such as 5 missed notifications when the deferral count is set to 5, the application will be closed, and the update will proceed automatically.
  * **Close the application and perform the update**\
    If selected, the notification closes after the timeout expires, the application is force-closed, and the update begins immediately.\
    \
    This option enforces compliance but may negatively impact user experience. It can also cause the application to close unexpectedly if the user is not present, such as when the device is locked or unattended.

## **Do not allow user deferral**

If the **Do not allow user deferral. The application will close and update if no action is taken before the timeout expires** option is selected, the user is not allowed to defer the installation.

If the application is still running when the notification timeout expires and no action is taken, the system automatically closes the application and proceeds with the updateimmediately. No additional prompts or deferral options are presented to the user.

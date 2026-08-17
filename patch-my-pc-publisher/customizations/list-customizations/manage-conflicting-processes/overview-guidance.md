# Overview and Guidance on Managing Conflicting Processes in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Manage Conflicting Processes** right-click option in Patch My PC (PMPC) Publisher is used to handle scenarios in which an application being updated is currently running on an end-user device. Some third party updates require the application to be closed before the installer can run successfully.

This option allows you to define which running processes should be detected and how Patch My PC ScriptRunner (which manages the installation), should respond when those processes are found during installation.

## Guidance

Products shown in the Product Tree with a blue cross icon (![Blue cross icon](<../../../../.gitbook/assets/image (4767).png>)) indicate that the application must be closed before updating.

PMPC has identified that these applications cannot be reliably updated whilst running.

<figure><img src="../../../../.gitbook/assets/image (4415).png" alt="Product Tree icon indicating the Manage Conflicting Processes feature should be configured" width="563"><figcaption></figcaption></figure>

For these products, Publisher's default behavior is to configure conflicting processes to [Skip installation when conflicting processes are in use](policy-section.md#skip-installation-when-conflicting-processes-are-in-use).

This prevents installation failures when the application is open. The update will retry at the next configured retry interval, which differs between Microsoft ConfigMgr and Intune update workflows.

For many organizations, a better compromise for these applications is to configure [Notify the user to close the application](policy-section.md#notify-the-user-to-close-the-application) and allow the user to [defer the installation](notification-policy.md#defer-snooze-policy) a limited number of times.

This approach balances application compliance with a positive end-user experience by allowing users time to close the application and save work.

When the notification is presented to the end user, the available actions control how the update proceeds.

<figure><img src="../../../../.gitbook/assets/image (132).png" alt="User options for Manage Conflicting Processes" width="282"><figcaption></figcaption></figure>

Selecting **Close All and Install** immediately closes the defined [conflicting processes](management-options.md#manage-process-list) and starts the update installation.

{% hint style="danger" %}
**Important**

If an application is closed by this process, it is not automatically reopened after the update completes. Application relaunch behavior depends on the application itself or user action.
{% endhint %}

Selecting **Snooze Install** records a deferral for the installation. The update does not run at that time and is retried during the next evaluation cycle based on the configured [deferral policy](notification-policy.md#defer-snooze-policy) and deployment platform.

## Applications that require closing during updates

See [Manage Conflicting Processes when Updating Third-Party Applications](https://patchmypc.com/kb/manage-conflicting-processes-when-updating) for a list we maintain of applications that should be closed during updates.

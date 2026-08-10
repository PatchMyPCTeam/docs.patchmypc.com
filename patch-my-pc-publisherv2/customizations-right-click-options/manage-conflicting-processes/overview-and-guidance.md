# Overview and Guidance

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

The **Manage Conflicting Processes** option is used to handle scenarios where an application that is being updated is currently running on an end user device. Some third party updates require the application to be closed before the installer can run successfully.

![Manage Conflicting Processes](/_images/image-(3964).png)

This option allows you to define which running processes should be detected and how Patch My PC ScriptRunner, which manages the installation, should respond when those processes are found during installation.

## Guidance

Products shown in the product tree with a **blue cross icon** indicate that the application must be closed while it is being updated. Patch My PC has identified that these applications cannot be reliably updated while running.

![Product Tree icon indicating the Manage Conflicting Processes feature should be configured](/_images/image-(3966).png)

For these products, the Publishers default behavior is to configure conflicting processes to [Skip installation when conflicting processes are in use](setting-configuration.md#skip-installation-when-conflicting-processes-are-in-use). This prevents installation failures when the application is open. The update will retry at the next configured retry interval, which differs between ConfigMgr and Intune update workflows.

For many organizations, a better compromise for these applications is to configure [Notify the user to close the application](setting-configuration.md#notify-the-user-to-close-the-application) and allow the user to[ defer the installation](setting-configuration.md#defer-policy) a limited number of times. This approach provides a balance between maintaining application compliance and preserving a positive end user experience by allowing users time to close the application and save work.

When the notification is presented to the end user, the available actions control how the update proceeds.

![User options for Manage Conflicting Processes](/_images/image-(135).png)

Selecting **Close All and Install** immediately closes the defined [conflicting processes](setting-configuration.md#manage-process-list) and starts the update installation.

> \*\*Important\*\*
>
> The closed applications are not automatically reopened after the update completes. Application relaunch behavior depends on the application itself or user action.

Selecting **Snooze Install** records a deferral for the installation. The update does not run at that time and is retried during the next evaluation cycle based on the configured [deferral policy](setting-configuration.md#defer-policy) and deployment platform.

## Applications that require closing during updates

For a maintained list of applications that should be closed during updates, see [https://patchmypc.com/kb/manage-conflicting-processes-when-updating](https://patchmypc.com/kb/manage-conflicting-processes-when-updating)
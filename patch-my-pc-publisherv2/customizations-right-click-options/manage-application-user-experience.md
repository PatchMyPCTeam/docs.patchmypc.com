# Manage Application User Experience

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_\
_Available on tab: ConfigMgr Apps_

## Overview

**Manage Application User Experience** allows you to customize the user experience settings applied to the ConfigMgr application deployment type created by the Publisher.

<figure><img src="../../.gitbook/assets/image (4062).png" alt="Manage Application User Experience" width="563"><figcaption></figcaption></figure>

These settings control how the application behaves during installation, including installation behavior, logon requirements, and user interaction.

## Inheritance and Scope

This option can be configured at multiple levels.

When configured at the All Products or Vendor level, you can choose which specific user experience settings should be inherited by products below. This allows you to define consistent defaults across many applications while still allowing exceptions at the product level.

<figure><img src="../../.gitbook/assets/image (4092).png" alt="Application User Experience" width="510"><figcaption></figcaption></figure>

At the Product level, all settings apply directly to that application and override inherited values.

## Application Behavior Constraints

If an application only supports system-wide installation, the Installation behavior option is disabled. The interface prevents selecting user based installation when the application does not support it.

<figure><img src="../../.gitbook/assets/image (4093).png" alt="Installation behavior for system-wide context apps" width="510"><figcaption></figcaption></figure>

For catalog applications that are user based, identified by **User** in the product name, the following behavior applies.

<figure><img src="../../.gitbook/assets/image (4094).png" alt="Installation behavior for user context apps" width="510"><figcaption></figcaption></figure>

* Installation behavior is fixed to user context.
* Logon requirement is fixed to require a logged on user.

These settings are preconfigured by design, cannot be changed, and do not inherit values from the Vendor or All Products level.

## RunTime

The Runtime settings control how long ConfigMgr allows the application installation to run and how the installation time is communicated to users.

* **Maximum allowed run time (minutes)**\
  Defines the maximum amount of time ConfigMgr will wait for the installation to complete before marking it as failed. If the installer exceeds this time, the deployment is terminated and reported as unsuccessful.
* **Estimated installation time (minutes)**\
  Specifies the expected duration of the installation and is shown to users in Software Center.\
  This value is informational only and does not affect enforcement or execution. It helps set user expectations during installation, particularly for longer-running installs.

## Reset Behavior

The Reset button restores all user experience settings to Patch My PC recommended defaults. This is useful if custom values were applied previously and you want to return to a known good configuration.

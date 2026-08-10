# Manage App Experience option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_
\
_Available on tab: ConfigMgr Apps_

The **Manage App Experience** right-click option in Patch My PC (PMPC) Publisher allows you to customize the user experience settings applied to the Microsoft ConfigMgr application deployment type created by Publisher.

These settings control how the application behaves during installation, including behavior, logon requirements, and user interaction.

When you right-click at a supported level and select **Manage App Experience**, the **Application User Experience** dialog is displayed.

!['Application User Experience' dialog](/_images/image-(4795).png "&#x27;Application User Experience&#x27; dialog")

## Specify user experience settings for application to inherit

This option can be configured at multiple levels.

When configured at the **All Products** or Vendor level, you can choose which specific user experience settings should be inherited by products below. This allows you to define consistent defaults across many applications whilst still allowing exceptions at the product level.

![Application User Experience settings when configured at a Vendor level](/_images/image-(4798).png "Application User Experience settings when configured at a Vendor level")

At the Product level, all settings apply directly to that application and override inherited values.

![Application User Experience settings when configured at a Product level](/_images/image-(4799).png "Application User Experience settings when configured at a Product level")

## Installation behavior Constraints

If an application only supports system-wide installation, the Installation behavior option is disabled. The interface prevents selecting user-based installation when the application does not support it.

![Installation behavior for system-wide context apps](/_images/image-(4800).png "Installation behavior for system-wide context apps")

For catalog applications that are user-based (identified by **User** in the product name), the following behavior applies:

* Installation behavior is fixed to user context.
* Logon requirement is fixed to require a logged-on user.

![Installation behavior for user-based apps](/_images/image-(4797).png "Installation behavior for user-based apps")

These settings are preconfigured by design, cannot be changed, and do not inherit values from the Vendor or All Products level.

## RunTime

The **RunTime** settings control how long ConfigMgr allows the application installation to run and how the installation time is communicated to users:

* **Maximum allowed run time (minutes)**\
  Defines the maximum amount of time ConfigMgr will wait for the installation to complete before marking it as failed. If the installer exceeds this time, the deployment is terminated and reported as unsuccessful.
* **Estimated installation time (minutes)**\
  Specifies the expected duration of the installation and is shown to users in the Software Center.\
  This value is informational only and does not affect enforcement or execution. It helps set user expectations during installation, particularly for longer-running installs.

![RunTime settings](/_images/image-(4801).png "RunTime settings")

## Restart Behavior

The **Restart Behavior** dropdown allows you to choose whether ConfigMgr should enforce a specific behavior you configure, regardless of the application's intended behavior.

If required, select the relevant option from the **Restart Behavior** dropdown.

!['Restart Behavior' dropdown](/_images/image-(4803).png "&#x27;Restart Behavior&#x27; dropdown")

## Reset button

The **Reset** button restores all user experience settings to PMPC recommended defaults. This is useful if custom values were applied previously and you want to return to a known good configuration.

!['Reset' buton](/_images/image-(4802).png "&#x27;Reset&#x27; buton")


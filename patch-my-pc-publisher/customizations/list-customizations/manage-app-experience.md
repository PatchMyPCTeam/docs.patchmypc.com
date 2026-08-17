# Manage App Experience option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

The **Manage App Experience** right-click option in Patch My PC (PMPC) Publisher allows you to customize the user experience settings applied to the Microsoft ConfigMgr application deployment type created by Publisher.

These settings control how the application behaves during installation, including behavior, logon requirements, and user interaction.

When you right-click at a supported level and select **Manage App Experience**, the **Application User Experience** dialog is displayed.

<figure><img src="../../../.gitbook/assets/image (4795).png" alt="&#x27;Application User Experience&#x27; dialog" width="506"><figcaption></figcaption></figure>

## Specify user experience settings for application to inherit

This option can be configured at multiple levels.

When configured at the **All Products** or Vendor level, you can choose which specific user experience settings should be inherited by products below. This allows you to define consistent defaults across many applications whilst still allowing exceptions at the product level.

<figure><img src="../../../.gitbook/assets/image (4798).png" alt="Application User Experience settings when configured at a Vendor level" width="508"><figcaption></figcaption></figure>

At the Product level, all settings apply directly to that application and override inherited values.

<figure><img src="../../../.gitbook/assets/image (4795).png" alt="Application User Experience settings when configured at a Product level" width="506"><figcaption></figcaption></figure>

## Installation behavior Constraints

If an application only supports system-wide installation, the Installation behavior option is disabled. The interface prevents selecting user-based installation when the application does not support it.

<figure><img src="../../../.gitbook/assets/image (4800).png" alt="Installation behavior for system-wide context apps" width="506"><figcaption></figcaption></figure>

For catalog applications that are user-based (identified by **User** in the product name), the following behavior applies:

* Installation behavior is fixed to user context.
* Logon requirement is fixed to require a logged-on user.

<figure><img src="../../../.gitbook/assets/image (4797).png" alt="Installation behavior for user-based apps" width="507"><figcaption></figcaption></figure>

These settings are preconfigured by design, cannot be changed, and do not inherit values from the Vendor or All Products level.

## RunTime

The **RunTime** settings control how long ConfigMgr allows the application installation to run and how the installation time is communicated to users:

* **Maximum allowed run time (minutes)**\
  Defines the maximum amount of time ConfigMgr will wait for the installation to complete before marking it as failed. If the installer exceeds this time, the deployment is terminated and reported as unsuccessful.
* **Estimated installation time (minutes)**\
  Specifies the expected duration of the installation and is shown to users in the Software Center.\
  This value is informational only and does not affect enforcement or execution. It helps set user expectations during installation, particularly for longer-running installs.

<figure><img src="../../../.gitbook/assets/image (4801).png" alt="RunTime settings" width="506"><figcaption></figcaption></figure>

## Restart Behavior

The **Restart Behavior** dropdown allows you to choose whether ConfigMgr should enforce a specific behavior you configure, regardless of the application's intended behavior.

If required, select the relevant option from the **Restart Behavior** dropdown.

<figure><img src="../../../.gitbook/assets/image (4803).png" alt="&#x27;Restart Behavior&#x27; dropdown" width="507"><figcaption></figcaption></figure>

## Reset button

The **Reset** button restores all user experience settings to PMPC recommended defaults. This is useful if custom values were applied previously and you want to return to a known good configuration.

<figure><img src="../../../.gitbook/assets/image (4802).png" alt="&#x27;Reset&#x27; buton" width="506"><figcaption></figcaption></figure>

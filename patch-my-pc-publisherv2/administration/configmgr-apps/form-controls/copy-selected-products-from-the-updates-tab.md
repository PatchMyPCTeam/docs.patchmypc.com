# Copy Selected Products from the Updates Tab

_Applies to: Patch My PC Publisher V2.x_

## ![](<../../../../.gitbook/assets/image (497).png>) Overview

This form control synchronizes product selections and/or customizations from the **Updates** tab to the **ConfigMgr Apps** tab. This option is intended to provide a quick and consistent way to align application management behavior with update publishing selections while preserving the standard inheritance behavior of the product tree.

<figure><img src="../../../../.gitbook/assets/image (498).png" alt="" width="545"><figcaption></figcaption></figure>

When this form control is used, the Publisher can copy product selections only or product selections together with customizations from the Updates tab to the ConfigMgr Apps tab.

If you choose to copy product selections only, the Publisher enables the same products in the ConfigMgr Apps tab that are selected on the Updates tab, but does not copy any custom actions. Existing application level customizations in the ConfigMgr Apps tab remain unchanged.

If you choose to copy product selections with customizations, the Publisher copies the full customization state from the Updates tab into the ConfigMgr Apps tab using the same product tree hierarchy. This includes settings applied at the All Products, vendor, and product levels, such as pre and post scripts, disabling updates, and shortcut removal.

The copy operation is **not cumulative**. If customizations already exist on the ConfigMgr Apps tab at the same level, they are **overwritten**, not merged.&#x20;

{% hint style="warning" %}
**Important**

Product level selections that exist only on the ConfigMgr Apps tab and are not selected on the Updates tab remain unchanged. However, if a customization is applied at the **vendor** or **All Products** level, that configuration is inherited by all child products, including those that were previously configured only on the ConfigMgr Apps tab.
{% endhint %}

To copy selected products and customizations from the Updates tab for ConfigMgr Apps tab:

1. Select the **Enable the selected products from the Updates tab that support installation packages** button.
2. When prompted with the confirmation dialog, choose one of the following options.

<figure><img src="../../../../.gitbook/assets/image (85).png" alt="Confirm Customizations &#x26; Selections Copy" width="444"><figcaption></figcaption></figure>

* Select **Yes** to copy custom actions, as well as products, from the Updates tab, including pre and post scripts, disabling updates, and removing shortcuts.
* Select **No** to copy only the product selections without copying custom actions.
* Select **Cancel** to stop the operation and make no changes.

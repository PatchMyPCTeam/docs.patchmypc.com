# Copy Selected Products from the Updates/Intune Apps Tab

_Applies to: Patch My PC Publisher V2.x_

## &#x20;Overview

This form control synchronizes product selections and/or customizations from the **Updates** tab to the **Intune Apps** tab and/or the **Intune Apps** tab to the **Intune Updates** tab. This option is intended to provide a quick and consistent way to align application management behavior with update publishing selections while preserving the standard inheritance behavior of the product tree.

![](/_images/image-(498).png)

## **Form Control behavior on the Intune Apps tab**

When this form control is used on the **Intune Apps** tab, the Publisher can copy product selections only or product selections together with customizations from the Updates tab to the Intune Apps tab.

If you choose to copy product selections only, the Publisher enables the same products in the Intune Apps tab that are selected on the Updates tab, but does not copy any custom actions. Existing application level customizations in the Intune Apps tab remain unchanged.

If you choose to copy product selections with customizations, the Publisher copies the full customization state from the Updates tab into the Intune Apps tab using the same product tree hierarchy. This includes settings applied at the All Products, vendor, and product levels, such as pre and post scripts, disabling updates, and shortcut removal.

The copy operation for customizations is **not cumulative**. If customizations already exist on the Intune Apps tab at the same level, they are **overwritten**, not merged.

> \*\*Important\*\*
>
> Product level selections that exist only on the Intune Apps tab and are not selected on the Updates tab remain unchanged. However, if a customization is applied at the \*\*vendor\*\* or \*\*All Products\*\* level, that configuration is inherited by all child products, including those that were previously configured only on the Intune Apps tab.

## **Form Control behavior on the Intune Updates tab**

When this form control is used on the **Intune Updates** tab, the Publisher can copy product selections only or product selections together with customizations from the Intune Apps tab to the Intune Updates tab.

If you choose to copy product selections only, the Publisher enables the same products in the Intune Updates tab that are selected on the Intune Apps tab, but does not copy any custom actions. Existing application level customizations in the Intune Updates tab remain unchanged.

If you choose to copy product selections with customizations, the Publisher copies the full customization state from the Intune Apps tab into theIntune Updates tab using the same product tree hierarchy. This includes settings applied at the All Products, vendor, and product levels, such as pre and post scripts, disabling updates, and shortcut removal.

The copy operation for customizations is **not cumulative**. If customizations already exist on the Intune Updates tab at the same level, they are **overwritten**, not merged.

> \*\*Important\*\*
>
> Product level selections that exist only on the Intune Updates tab and are not selected on the Intune Apps tab remain unchanged. However, if a customization is applied at the \*\*vendor\*\* or \*\*All Products\*\* level, that configuration is inherited by all child products, including those that were previously configured only on the Intune Updates tab.

## **Form Control behavior on both the Intune Apps and Intune Updates tab**

To copy selected products and customizations from the Updates tab to the Intune Apps tab or from the Intune Apps tab to the Intune Updates tab:

1. Select the **Enable the selected products from the Updates tab that support installation packages** button.
2. When prompted with the confirmation dialog, choose one of the following options.

![Confirm Customizations & Selections Copy](/_images/image-(4083).png)

* Select **Yes** to copy custom actions, as well as products, from the Updates tab, including pre and post scripts, disabling updates, and removing shortcuts.
* Select **No** to copy only the product selections without copying custom actions.
* Select **Cancel** to stop the operation and make no changes.

> \*\*Note\*\*
>
> In non-WSUS environments, the Updates tab may have been hidden by using the \*\*Disable the Updates tab for publishing software to WSUS\*\* setting in the \[Intune Standalone Options]\(../../advanced/intune-standalone-options.md) section on the \[Advanced]\(../../advanced/) tab. In this scenario, the form control is not visible on the Intune Apps tab.
# Manage Naming Convention

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_\
_Available on tab: Intune Apps, Intune Updates_

## Overview

**Manage Naming Convention** allows you to define a custom naming standard for the Win32 applications and updates created by the Publisher. This helps ensure application names in Intune are consistent, descriptive, and aligned with your organizational standards.

<figure><img src="../../.gitbook/assets/image (4060).png" alt="Manage Naming Convention" width="512"><figcaption></figcaption></figure>

If no custom naming convention is configured, or if the pattern is left empty, the Publisher uses its default naming format.

{% hint style="info" %}
**Note**

This right-click option is only available at the [product level](../administration/intune-apps-updates/product-tree.md#product-level-recommended) in the [product tree](../administration/intune-apps-updates/product-tree.md) for **Intune Updates**. For **Intune Apps**, use [Set Custom Application Icon and Properties](set-custom-application-icon-and-properties.md) instead to change the name of a single product, including the description and icon.
{% endhint %}

## Intune Naming Convention

When you select **Manage naming convention**, the **Intune Naming Convention** dialog is used to define a custom name format for Win32 applications created by the Publisher.&#x20;

<figure><img src="../../.gitbook/assets/image (4061).png" alt="Intune Naming Convention" width="374"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The default Patch My PC naming is represented by **%OriginalName%** and can be reused or extended in your custom pattern.
{% endhint %}

If the custom name field is left empty, the Publisher uses the default application name.

### Token Values

Naming conventions are built using token values. At least one token must be included.

The available tokens are shown at the top of the dialog and can be clicked to insert them at the cursor position.

* **%VendorName%**\
  Resolves to the software vendor name.
* **%ProductName%**\
  Resolves to the product name and architecture.
* **%Version%**\
  Resolves to the application version.
* **%OriginalName%**\
  Resolves to the default Patch My PC application or update name.

**Example**\
Custom Intune App name configured as:

```
[App] - %OriginalName%
```

Resulting Intune application name:

```
[App] - Google Chrome 142.0.7444.176 (x64)
```

{% hint style="info" %}
**Note**

When creating naming conventions for **Intune Updates**, remember that **%OriginalName%** already includes the **Update** **for** prefix.

Avoid adding additional wording like **Update** to prevent duplicated names.
{% endhint %}

This approach allows you to clearly identify Publisher created applications while retaining the original product and version details.

## Configure a Naming Convention

To configure a naming convention:

1. Right-click the All Products, Vendor or Product (Intune Updates tab only) node in the Product Tree.
2. Select **Manage Naming Convention**.
3. Click one or more **token values** to build the naming pattern.
4. Enter the desired custom name format.
5. Click  **OK** to save the configuration.

The naming convention is applied during the next Publisher [synchronization](../administration/sync-schedule.md) and affects newly created applications and updates only.

{% hint style="warning" %}
**Important**

If a naming convention is configured at the All Products or Vendor level, that configuration is inherited automatically to products lower in the product tree.
{% endhint %}




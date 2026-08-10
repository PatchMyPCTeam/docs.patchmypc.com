# Manage Naming Convention option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Custom Products, All Vendors, Vendor_
\
_Available on tab: Intune Apps, Intune Updates_

The **Manage Naming Convention** right-click option in Patch My PC (PMPC) Publisher allows you to define a custom naming standard for the Win32 applications and updates created by Publisher at the levels detailed above.

This helps ensure application names in Intune are consistent, descriptive, and aligned with your organizational standards.

If no custom naming convention is configured, or if the pattern is left empty, Publisher uses its default naming format.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>This right-click option is only available at the Product Tree levels specified in the _Applies to:_ section for Intune Apps and Updates. For options available at the Product level, see [Custom Intune App Properties](custom-intune-app-properties.md).</p>
</blockquote>

When you select the **Manage Naming Convention** right-click option, the **Custom Intune Application Properties** dialog appears.

!['Custom Intune Application Properties' dialog](/_images/image-(4804).png "&#x27;Custom Intune Application Properties&#x27; dialog")

From here, you can configure a custom name format for Win32 applications created by Publisher by using at least one or more of the provided token values (which can be clicked to insert them at the cursor position):

* **%VendorName%**\
  Resolves to the software vendor name.
* **%ProductName%**\
  Resolves to the product name and architecture.
* **%Version%**\
  Resolves to the application version.
* **%OriginalName%**\
  Resolves to the default Patch My PC application or update name, which can be reused or extended in your custom pattern.

### **Example**

Custom Intune App name configured as:

```
[App] - %OriginalName%
```

Resulting Intune application name:

```
[App] - Google Chrome 142.0.7444.176 (x64)
```

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>When creating naming conventions for **Intune Updates**, remember that **%OriginalName%** already includes the **Update** **for** prefix.</p>
<p>Avoid adding additional wording like **Update** to prevent duplicated names.</p>
</blockquote>

This approach allows you to clearly identify Publisher-created applications whilst retaining the original product and version details.

## Configure a Naming Convention

To configure a naming convention:

1. Right-click the relevant object in the Product Tree and select **Manage Naming Convention**.
2. On the **Custom Intune Application Properties** dialog, click one or more token values to build your required naming pattern.
3. Click **OK** to save the configuration.

The naming convention is applied during the next Publisher [Synchronization](../../manage/sync-schedule-tab/) and affects newly created applications and updates only.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If a naming convention is configured at the All Products or Vendor level, that configuration is inherited automatically by any products lower in the Product Tree, unless they are overridden at a product level by using the [Custom Intune App Properties](custom-intune-app-properties.md) right-click option.</p>
</blockquote>
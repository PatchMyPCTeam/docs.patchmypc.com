# Modify Command Line

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: Product_\
_&#x41;vailable on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

The **Modify Command Line** dialog allows you to customize the silent installation command line for a specific product in the Publisher. The dialog shows the default command line, lets you append additional arguments, and provides a preview of the final command line that will be executed.

![Modify Command Line](/_images/image-(4016).png)

## Default Command Line

The **Default Command Line** section displays the silent installation command line defined in the Patch My PC catalog for the selected product. This command line cannot be edited from this dialog and is shown for reference only.

> \*\*Note\*\*
>
> Use this section to understand which parameters are already included before adding any custom arguments.

![Modify Command Line Settings](/_images/image-(4015).png)

## Your Additional Arguments

The **Your Additional Arguments** field is where you enter custom command line parameters that will be appended to the default command line.

Only include parameters that are specific to your customization. Do not re-add standard silent install switches such as quiet or norestart unless explicitly required.

You can insert supported variables such as `%CurrentDir%` by using the **Insert Variable** option. Variables are expanded at runtime and will still appear as variables in the preview.

> \*\*Important\*\*
>
> Although this setting can be used to apply a transform file by using TRANSFORMS=xxx.mst and adding the MST as an extra file through the \[Add Pre or Post Scrip]\(add-custom-pre-post-scripts.md)t option, we recommend using the dedicated \[Add MST Transform File]\(add-mst-transformation-file.md) right click option instead.
>
> The transform option handles MST files correctly and is much simpler than bundling and referencing the transform manually through pre and post script actions.

## Parameter Precedence for MSI Installers

When the installer is an MSI, and you specify a property that already exists in the default command line, the last occurrence of that property takes precedence. This means your custom value overrides the default value provided by the Publisher.

For example, if Patch My PC includes `AllUsers=1` in the default command line and you add `AllUsers=2` in the **Your Additional Arguments** field, the installer will use `AllUsers=2`.

This behavior allows you to override existing MSI properties without modifying the default command line.

## Examples and Special Variables

The **Examples and Special Variables** section helps you build custom command line arguments and shows the variables you can use.

> \*\*Note\*\*
>
> This section is informational and cannot be edited.

![Examples and Special Values](/_images/image-(4130).png)

The Examples area shows sample installer parameters that can be appended to the default silent command line. Examples include:

```
PID=12345-54321
/LANG=EN-US
INSTALLDIR="%ProgramFiles%\MyApp"
```

In addition to standard Windows environment variables such as `%ProgramFiles%` and `%TEMP%`, the following Publisher specific variables are available:

* **%CurrentDir%**\
  Resolves to the full path where the installer is executed. The value of %CurrentDir% depends on the publishing platform. For example, it may differ when the update is installed through WSUS, ConfigMgr, or Intune. The path shown in the dialog is an example and may not match the exact runtime location in every scenario.
* **%VendorName%**\
  Resolves to the vendor name of the product that was right clicked to modify the command line.
* **%ProductName%**\
  Resolves to the product name of the product that was right clicked.
* **%Version%**\
  Resolves to the version of the specific update being published for that product.

These variables are resolved dynamically based on the selected product and update at runtime. They allow you to create reusable and version aware command line arguments without needing to hard code product specific values.

## Final Command Line Preview

The Final Command Line Preview section shows how the complete command line will look once your additional arguments are appended. Variables are not expanded in this view and are displayed as variables.
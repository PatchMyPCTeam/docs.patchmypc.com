# Modify Command Line option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: Product_
\
_Available on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Modify Command Line** right-click option in Patch My PC (PMPC) Publisher allows you to customize the silent installation command line for a specific product in Publisher.&#x20;

Selecting this option opens the dialog that shows:

* [Default Command Line](modify-command-line.md#default-command-line)
* [Your Additional Arguments](modify-command-line.md#your-additional-arguments)
* [Final Command Line Preview](modify-command-line.md#final-command-line-preview)

## Default Command Line

The **Default Command Line** section displays the silent installation command line defined in the Patch My PC catalog for the selected product. This command line cannot be edited from this dialog and is shown for reference only.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Use this section to understand which parameters are already included before adding any custom arguments.</p>
</blockquote>

!['Default Command Line'](/_images/image-(4424).png "&#x27;Default Command Line&#x27;")

## Your Additional Arguments

The **Your Additional Arguments** section is where you can enter custom command-line parameters that will be appended to the default command line.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Include only parameters specific to your customization. Do not re-add standard silent-install switches, such as **quiet** or **norestart**, unless explicitly required.</p>
</blockquote>

!['Your Additional Arguments' section](/_images/image-(4425).png "&#x27;Your Additional Arguments&#x27; section")

You can insert supported variables such as `%CurrentDir%` by using the **Insert Variable** option. Variables are expanded at runtime and will still appear as variables in the preview.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Although this setting can be used to apply a transform file by using **TRANSFORMS=xxx.mst** and adding the MST as an extra file through the [Add Pre/Post Scripts](add-pre-post-scripts.md) option, we recommend using the dedicated [Manage MST File](manage-mst-file.md) right-click option instead.&#x20;</p>
<p>The transform option handles MST files correctly and is much simpler than bundling and referencing the transform manually through pre- and post-script actions.</p>
</blockquote>

### Parameter Precedence for MSI Installers

If the installer is an MSI and you specify a property that already exists in the default command line, the last occurrence of that property takes precedence. This means your custom value overrides the default value provided by Publisher.

For example, if PMPC includes `AllUsers=1` in the default command line and you add `AllUsers=2` in the **Your Additional Arguments** field, the installer will use `AllUsers=2`.

This behavior allows you to override existing MSI properties without modifying the default command line.

### Examples and Special Variables

The **Examples and Special Variables** section helps you build custom command line arguments and shows the variables you can use.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>This section is for information only and cannot be edited.</p>
</blockquote>

!['Examples and Special Variables' section](/_images/image-(4426).png "&#x27;Examples and Special Variables&#x27; section")

The **Examples** area shows sample installer parameters that can be appended to the default silent command line. Examples include:

```
PID=12345-54321
/LANG=EN-US
INSTALLDIR="%ProgramFiles%\MyApp"
```

In addition to standard Windows environment variables (such as `%ProgramFiles%` and `%TEMP%`), the following Publisher-specific variables are available:

<table><thead><tr><th width="164" valign="top">Variable</th><th valign="top">Resolves to the...</th></tr></thead><tbody><tr><td valign="top">%CurrentDir%</td><td valign="top"><p>Full path where the installer is executed. The value of <code>%CurrentDir%</code> depends on the publishing platform. </p><p></p><p>For example, it may differ when the update is installed through WSUS, ConfigMgr, or Intune.</p><p></p><p>The path shown in the dialog is an example and may not match the exact runtime location in every scenario.</p></td></tr><tr><td valign="top">%VendorName%</td><td valign="top">Vendor name of the product right-clicked to modify the command line.</td></tr><tr><td valign="top">%ProductName%</td><td valign="top">Product name of the product that was right-clicked.</td></tr><tr><td valign="top">%Version%</td><td valign="top">Version of the specific update being published for that product.</td></tr></tbody></table>

These variables are resolved dynamically based on the selected product and update at runtime. They allow you to create reusable and version-aware command line arguments without needing to hard-code product-specific values.

## Final Command Line Preview

The **Final Command Line Preview** section shows how the complete command line will look once your additional arguments are appended. Variables are not expanded in this view and are displayed as variables.

!['Final Command Line Preview' section](/_images/image-(4427).png "&#x27;Final Command Line Preview&#x27; section")
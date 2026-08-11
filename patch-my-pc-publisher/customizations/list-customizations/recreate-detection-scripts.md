# Recreate Detection Scripts option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_\
_Available on tab: ConfigMgr Apps, Intune Apps, Intune Updates_

The **Recreate Detection Scripts** right-click option in Patch My PC (PMPC) Publisher forces Publisher to regenerate the PowerShell detection script for the selected application or applications.

This is primarily used when a code-signing certificate has changed. Existing detection scripts remain signed with the previous certificate, which can cause validation or trust issues.

Recreating the detection script ensures a new script is generated and signed using the current certificate.

Recreating the detection script can also be useful when you want applications to receive improvements made to the detection logic.

Publisher periodically enhances detection scripts to improve reliability, logging, and compatibility. Using this option allows applications to receive the latest detection method even if the vendor has not released a new version.

{% hint style="info" %}
**Note**

When used for products on the **Intune Apps** or **Intune Updates** tabs, the Win32 application requirement script and the detection script are automatically regenerated and updated.
{% endhint %}

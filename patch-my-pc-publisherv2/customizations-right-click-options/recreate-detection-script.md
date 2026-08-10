# Recreate Detection Script

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_
\
_Available on tab: ConfigMgr Apps, Intune Apps, Intune Updates_

The **Recreate Detection Script** option forces the Publisher to regenerate the PowerShell detection script for the selected application or applications.

![Recreate Detection Script](/_images/image-(98).png "Recreate Detection Script")

This option is primarily used when a code-signing certificate has changed. Existing detection scripts remain signed with the previous certificate, which can cause validation or trust issues. Recreating the detection script ensures a new script is generated and signed using the current certificate.

Recreating the detection script can also be useful when you want applications to receive improvements made to the detection logic. The Publisher periodically enhances detection scripts to improve reliability, logging, and compatibility. Using this option allows applications to receive the latest detection method even if the vendor has not released a new version.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>When this option is used for products on the Intune Apps or Intune Updates tabs, the Win32 application requirement script, as well as the detection script, is regenerated and updated automatically.</p>
</blockquote>
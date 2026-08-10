# Manage Installation Logging

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_
\
_Available on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

The **Manage Installation Logging** option enables _additional_ client side logging during product installation to assist with troubleshooting failures or unexpected behavior.

When enabled, the Publisher configures the installer to generate a Patch My PC installation log and, when supported, the vendor’s native installation log. These logs are created during product installation on the client device and can be collected for diagnostic purposes.

![Manage Installation Logging](/_images/image-(128).png "Manage Installation Logging")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Some vendor installers can generate their own installation logs, most commonly MSI based installers. The **Manage Installation Logging** option facilitates Patch My PC ScriptRunner, which manages the installation, to pass the appropriate logging parameters to the installer so that additional vendor specific logs are created. These logs are useful for client side troubleshooting when an installation fails.</p>
<p>This option only affects vendor logging behavior. The Patch My PC ScriptRunner logs are created regardless of whether this option is enabled.</p>
<p>More information on log files and locations can be found <a href="https://docs.patchmypc.com/get-help/log-reference-guide">https://docs.patchmypc.com/get-help/log-reference-guide</a>.</p>
</blockquote>

The Manage Installation Logging window provides the following settings.

![Logging Options](/_images/image-(129).png "Logging Options")

## **Folder path**

Specifies the location where client side installation logs are written. The default log location depends on the product installation scenario:

* Products installed from **ConfigMgr and WSUS** store logs in `C:\Windows\CCM\Logs\PatchMyPCInstallLogs`
* Products installed from **Intune** store logs in `%ProgramData%\PatchMyPCInstallLogs`

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>User-based installations write logs to folders within the user profile. More information on log files and locations can be found <a href="https://docs.patchmypc.com/get-help/log-reference-guidehttps://docs.patchmypc.com/get-help/log-reference-guide">https://docs.patchmypc.com/get-help/log-reference-guide</a>.</p>
</blockquote>

## **Enable verbose logging for MSI installation**

Enables verbose logging for MSI based installers that support this mode to capture additional detail.

## **Prefix the log with the computer name**

Adds the device name to the beginning of the log file name to simplify identification when collecting logs from multiple devices.

## **In case of installation failure, copy the log file to this secondary folder**

Creates a second copy of the installation log when the product fails to install and writes it to the specified path. The device must be able to access this location at install time and have permission to write to it. If the path is an SMB share, the installation context must have write access.
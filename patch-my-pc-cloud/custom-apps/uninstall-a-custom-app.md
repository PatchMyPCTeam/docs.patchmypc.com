# Uninstall a Custom App

_Applies to: Patch My PC Cloud Custom Apps_

The Custom Apps Uninstall feature of Patch My PC (PMPC) is designed to simplify the uninstallation of custom applications. It works by leveraging specific uninstall strings found in the Windows registry.

### QuietUninstallString&#x20;

If available, this is prioritized as it typically specifies a silent or automated uninstall command.

### UninstallString

If no **QuietUninstallString** is found, it falls back to the general uninstall command.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The **UninstallString** may not always support silent operations and could display prompts or dialogs requiring user input. When the uninstallation is triggered in the SYSTEM context, this interaction occurs in session 0, potentially causing the process to fail while waiting for input.</p>
</blockquote>

### **Limitations**

Custom Apps uninstallation supports MSI's for ConfigMgr and both MSI's and EXE's for Intune. We are planning to add additional customizations and support in a future release.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you are using our On-Premises Publisher, pre and post script functionality for uninstalling EXE-based Custom Apps for both ConfigMgr and Intune is currently unavailable.</p>
</blockquote>
---
description: >-
  Download the latest version of the Patch My PC Publisher and walk through the
  installation.
---

# Download and Install

_Applies to: On-premises Publisher_

## Download the Publisher MSI Installer <a href="#download-the-publisher-msi-installer" id="download-the-publisher-msi-installer"></a>

{% embed url="https://patchmypc.com/msi" %}
Download Patch My PC Publisher
{% endembed %}

## Run the Installation

Start the installation by double-clicking the downloaded MSI.&#x20;

<blockquote class="wp-block-quote">
<p>Depending on user account control settings, you may need to run an elevated command prompt and launch the MSI from the command prompt.</p>
</blockquote>

### Welcome Screen

Once the installation starts you'll be greeted by the welcome screen in our installer wizard, click **Next**.

![Select next to continue past the welcome screen](/_images/image-(1077 "Select next to continue past the welcome screen").png>)

### End-User License Agreement

Read the End-User License Agreement. After that, select **I accept the terms in the License Agreement** and click **Next**.

![End-User License Agreement](/_images/image-(1253 "End-User License Agreement").png>)

### Disable Microsoft Intune Standalone Mode

Ensure the option **Enable Microsoft Intune standalone mode** is **not selected**. Enabling this will disable any prerequisite checks for integration with WSUS/ConfigMgr and also hide options for publishing to WSUS/ConfigMgr after installation.

This option is for customers who intend to publish only to Microsoft Intune.&#x20;

Click **Next**.

![Option for Microsoft Intune standalone mode](/_images/image-(1216 "Option for Microsoft Intune standalone mode").png>)

### Select Installation Folder

By default the Publisher is installed in **C:\Program Files\Patch My PC\Patch My PC Publishing Service**.\
\
This location is where we store all of the product's configuration information.&#x20;

![Select the folder where the service should be installed](/_images/image-(1066 "Select the folder where the service should be installed").png>)

### Ready To Install

Click **Install**.

![Select install to start the installation.](/_images/image-(1174 "Select install to start the installation.").png>)

![](/_images/image-(1217).png>)

### Completed

Once the Publisher has finished installing, click **Finish** to close the installation wizard.&#x20;

<blockquote class="wp-block-quote">
<p>By default, the "**Launch Patch My PC Publishing Service**" is enabled - this will launch the Publisher when you click **Finish**.</p>
</blockquote>

![](/_images/image-(1198).png>)
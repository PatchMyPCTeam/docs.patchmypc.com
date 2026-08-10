---
description: >-
  You've got the requirements, now lets go over where you can download the
  newest version of the Product, and walk through the installation.
---

# Download and Install

_Applies to: On-premises Publisher_

## Downloading the Newest Version

You can always download the latest MSI installer of the publishing service using the following URL:&#x20;

[https://patchmypc.com/publishingservice-download](https://patchmypc.com/scupcatalog/downloads/publishingservice/PatchMyPC-Publishing-Service.msi)

![This is how the MSI should look once downloaded](/_images/image-(1854 "This is how the MSI should look once downloaded").png>)

## Run the Installation

Start the installation by double clicking the downloaded MSI.&#x20;

<blockquote class="wp-block-quote">
<p>Depending on user account control settings, you may need to run an elevated command prompt and launch the MSI from the command prompt.</p>
</blockquote>

### Welcome Screen

Once the installation starts you'll be greeted by the welcome screen in our installer wizard, click next.

![Select next to continue past the welcome screen.](/_images/image-(1779 "Select next to continue past the welcome screen.").png>)

### End-User License Agreement

The next step will be to accept the EULA. Make sure you select the "I accept the terms in the Agreement" and hit next.

![EULA Terms](/_images/image-(1955 "EULA Terms").png>)

### Enable Intune Standalone Mode

When installing the product we provide an option called Intune Standalone mode. If you do **NOT** intend to use the product with Configuration Manager, ensure the option is checked and select next.

![](/_images/image-(1791).png>)

### Select Installation Folder

By default, we install the publisher service in \
\
**C:\Program Files\Patch My PC\Patch My PC Publishing Service\\**\
\
This location is where we store all of the products configuration information.&#x20;

![Select the folder where the service should be installed](/_images/image-(1768 "Select the folder where the service should be installed").png>)

### Ready To Install

You are now ready to install the product! Click Install, and grab a drink of water.

![Select install to start the installation.](/_images/image-(1876 "Select install to start the installation.").png>)

![Enjoy a glass of water, while we do the work.](/_images/image-(1919 "Enjoy a glass of water, while we do the work.").png>)

### Completed

Once the publisher has finished installing, just hit the finish button to close the install wizard.&#x20;

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>By default, the **Launch Patch My PC Publishing Service** checkbox is checked, meaning when you click **Finish**, Publisher will open automatically.</p>
</blockquote>

![](/_images/image-(1900).png>)
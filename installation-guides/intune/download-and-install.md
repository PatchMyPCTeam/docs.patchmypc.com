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

![This is how the MSI should look once downloaded](<../../.gitbook/assets/image (1854).png>)

## Run the Installation

Start the installation by double clicking the downloaded MSI.&#x20;

{% hint style="info" %}
Depending on user account control settings, you may need to run an elevated command prompt and launch the MSI from the command prompt.
{% endhint %}

### Welcome Screen

Once the installation starts you'll be greeted by the welcome screen in our installer wizard, click next.

![Select next to continue past the welcome screen.](<../../.gitbook/assets/image (1779).png>)

### End-User License Agreement

The next step will be to accept the EULA. Make sure you select the "I accept the terms in the Agreement" and hit next.

![EULA Terms](<../../.gitbook/assets/image (1955).png>)

### Enable Intune Standalone Mode

When installing the product we provide an option called Intune Standalone mode. If you do **NOT** intend to use the product with Configuration Manager, ensure the option is checked and select next.

![](<../../.gitbook/assets/image (1791).png>)

### Select Installation Folder

By default, we install the publisher service in \
\
**C:\Program Files\Patch My PC\Patch My PC Publishing Service\\**\
\
This location is where we store all of the products configuration information.&#x20;

![Select the folder where the service should be installed](<../../.gitbook/assets/image (1768).png>)

### Ready To Install

You are now ready to install the product! Click Install, and grab a drink of water.

![Select install to start the installation.](<../../.gitbook/assets/image (1876).png>)

![Enjoy a glass of water, while we do the work.](<../../.gitbook/assets/image (1919).png>)

### Completed

Once the publisher has finished installing, just hit the finish button to close the install wizard.&#x20;

{% hint style="info" %}
**Note**

By default, the **Launch Patch My PC Publishing Service** checkbox is checked, meaning when you click **Finish**, Publisher will open automatically.
{% endhint %}

![](<../../.gitbook/assets/image (1900).png>)

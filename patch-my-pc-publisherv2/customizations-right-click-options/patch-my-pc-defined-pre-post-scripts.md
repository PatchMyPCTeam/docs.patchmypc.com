# Patch My PC Defined Pre/Post Scripts

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: Product_\
_Available on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

Patch My PC defined pre and post scripts are provided for specific products that cannot fully manage certain scenarios on their own. A common example is software that is unable to remove older versions during an upgrade, such as Oracle Java.

<figure><img src="../../.gitbook/assets/image (4003).png" alt="Patch My PC Defined Pre/Post Scripts" width="495"><figcaption></figcaption></figure>

These scripts are downloaded and bundled automatically with the application or update when it is published.

## Required Scripts

Required Scripts are enforced and cannot be modified or disabled. They are always executed as part of the installation or update to ensure the application installs correctly.

## Recommended Scripts

Recommended Scripts are optional. They are included with the application or update but can be disabled if you prefer not to use them.

<figure><img src="../../.gitbook/assets/image (4004).png" alt="Recommended Scripts" width="563"><figcaption></figcaption></figure>

### Review the Recommended Script

To view the Patch My PC recommended script:

1. Click the **Patch My PC Defined Pre/Post Scripts** right-click customization option for the product in the product tree.
2. Click **View** to open the script in a browser and review its contents.
3. Review the Description field to understand what the script does and when it runs.

{% hint style="info" %}
**Note**

Recommended scripts are hosted by Patch My PC and are referenced by URL. They are not editable from the Publisher UI.
{% endhint %}

### Configure Script Behavior

The following options control how the recommended script behaves.

* **Don’t attempt software update if the pre script returns an exit code other than 0 or 3010**  \
  When enabled, the installation or update stops if the recommended script fails. This option is enabled by default and ensures the deployment does not continue if required cleanup actions cannot be completed.
* **Disable the Patch My PC recommended pre update script for this product**  \
  When enabled, the recommended script is skipped for this product. This option is available only for recommended scripts and does not apply to required scripts.

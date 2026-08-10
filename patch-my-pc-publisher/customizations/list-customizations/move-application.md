# Move Application option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: Vendor, Product_\
_Available on tab: ConfigMgr Apps_

{% hint style="danger" %}
**Important**

This article has not been updated for Version 3.x. Once it has, this banner will be removed.
{% endhint %}

The **Move Application** right-click option in Patch My PC (PMPC) Publisher allows you to control where ConfigMgr applications created by the Publisher are stored within the ConfigMgr console.

Instead of leaving newly created applications in the default Applications root node, this setting automatically moves them into a folder structure that better aligns with how you organize and manage software.

<figure><img src="../../../.gitbook/assets/image (104).png" alt="ConfigMgr Application Folders" width="563"><figcaption></figcaption></figure>

## Override Behavior

This option will override the global [Move applications to a specific console folder](../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/application-creation-options.md#move-applications-to-a-specific-console-folder) ConfigMgr setting. This lets you group apps in a way that makes sense for your environment, for example, placing all Google products in a **Google** folder, or isolating test applications in a separate folder structure.

### Configure a Custom Folder

When using this right-click option, the **Select Console Folder** dialog allows you to choose where newly created ConfigMgr applications should be placed after publishing.

<figure><img src="../../../.gitbook/assets/image (103).png" alt="Select a console folder" width="450"><figcaption></figcaption></figure>

1. Right-click the **Vendor** or **Product** you want to configure.
2. Select **Move the application to a custom folder**.
3. In the **Select Console Folder** window:
   * Browse the existing folder structure under **Applications**.
   * Select the target folder where applications should be moved.
4. (Optional) To create a new folder:
   * Enter a folder name in the **Create New Folder** field.
   * Click **Create Folder**.
5. Click **OK** to save the selection.

Use the **Refresh** button to reload the folder list observed in the ConfigMgr console.

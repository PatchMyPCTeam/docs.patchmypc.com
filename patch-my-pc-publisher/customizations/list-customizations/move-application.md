# Move Application option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

The **Move Application** right-click option in Patch My PC (PMPC) Publisher allows you to control where Microsoft Configuration Manager (ConfigMgr) applications created by Publisher are stored within the ConfigMgr console.

Instead of leaving newly created applications in the default **Applications** root node, this setting automatically moves them into a folder structure that better aligns with how you organize and manage software.

<figure><img src="../../../.gitbook/assets/image (104).png" alt="ConfigMgr Application Folders" width="563"><figcaption></figcaption></figure>

## Override Behavior

This option will override the global [Move applications to a specific console folder](../../manage/configmgr-apps-tab/base-install-options/application-creation-options.md#move-applications-to-a-specific-console-folder) ConfigMgr setting. This lets you group apps in a way that makes sense for your environment, for example, placing all Google products in a **Google** folder, or isolating test applications in a separate folder structure.

### To configure a Custom Folder

1. Right-click the relevant item and select **Move Application**. The list of available security scopes is retrieved directly from your ConfigMgr environment.
2. On the **Select Console Folder** screen, browse the existing folder structure under **Applications**.

<figure><img src="../../../.gitbook/assets/image (963).png" alt="&#x27;Select Console Folder&#x27; screen" width="450"><figcaption></figcaption></figure>

3. Select the target folder where applications should be moved to, ensuring the **Selected Folder** field shows the correct location.
4. Optionally, to create a new folder, type the name of the new folder in the **Create New Folder** field
5. Click **OK**.

Use the **Refresh** button to reload the folder list displayed in the ConfigMgr console.

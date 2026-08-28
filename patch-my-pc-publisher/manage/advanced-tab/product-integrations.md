# Product Integrations section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Product Integrations** section on the **Advanced** tab of Patch My PC (PMPC) Publisher is used to limit the Publisher to Intune-only functionality. These settings hide the ConfigMgr and WSUS-related publishing features from the user interface.

<figure><img src="../../../.gitbook/assets/image (741).png" alt="&#x27;Product Integrations&#x27; section" width="563"><figcaption></figcaption></figure>

The following options are available:

* **Disable the ConfigMgr Apps tab**\
  When enabled, the ConfigMgr Apps tab is hidden. Publishing applications to ConfigMgr is no longer available from the Publisher interface.
* **Disable the Updates tab**\
  When enabled, the Updates tab is hidden. Publishing software updates to WSUS is no longer available from the Publisher interface.

## **Installation Consideration**

These options are automatically enabled if **Enable Microsoft Intune standalone mode** was selected during installation of the Publisher.

<figure><img src="../../../.gitbook/assets/image (177).png" alt="Enable Microsoft Intune standalone mode" width="371"><figcaption></figcaption></figure>

Intune standalone mode is not permanent. The ConfigMgr Apps tab and the Updates tab can be re-enabled at any time by clearing the corresponding options in the Advanced tab of the Publisher.

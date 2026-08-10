# Overview of the WSUS Updates tab in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **WSUS Updates** tab of Patch My PC (PMPC) Publisher is where you select which third-party updates to publish to Microsoft Windows Server Update Services (WSUS). Products enabled here determine which third-party updates Publisher will publish and maintain within your environment.

![Updates Tab Overview](/_images/image-(425).png)

For ConfigMgr customers, updates selected on this tab are published to WSUS and can then be synchronized into ConfigMgr when Publisher is installed on the Software Update Point (SUP). This allows third-party updates to be deployed and reported on in the same way as Microsoft updates.

Third-party updates synchronized from WSUS to ConfigMgr during a SUP sync will appear in the **Software Library | All Software Updates** node in the ConfigMgr console.

![Updates appear in the All Software Updates view](/_images/image-(426).png)

Additional behavior related to update publishing can be configured using the [**Options**](../../../patch-my-pc-publisherv2/administration/updates/options/) button on the Updates tab.
# Overview

_Applies to: Patch My PC Publisher V2.x_

The Updates tab is where you select which third-party updates should be published to WSUS. Products enabled here determine which third-party updates the Publisher will publish and maintain within your environment.

<figure><img src="../../../.gitbook/assets/image (425).png" alt="Updates Tab Overview" width="563"><figcaption></figcaption></figure>

For ConfigMgr customers, updates selected on this tab are published to WSUS and can then be synchronized into ConfigMgr when Publisher is installed on the Software Update Point (SUP). This allows third-party updates to be deployed and reported on in the same way as Microsoft updates.

Third-party updates synchronized from WSUS to ConfigMgr during a SUP sync will appear in the **Software Library > All Software Updates** node in the ConfigMgr console.

<figure><img src="../../../.gitbook/assets/image (426).png" alt="Updates appear in the All Software Updates view" width="563"><figcaption></figcaption></figure>

Additional behavior related to update publishing can be configured using the [**Options**](options/) button on the Updates tab.

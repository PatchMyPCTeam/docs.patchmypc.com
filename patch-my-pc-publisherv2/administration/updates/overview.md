# Overview

_Applies to: Patch My PC Publisher V2.x_

The Updates tab is where you select which third-party updates should be published to WSUS. Products enabled here determine which third-party updates the Publisher will publish and maintain within your environment.

![Updates Tab Overview](/_images/image-(425 "Updates Tab Overview") (1).png>)

For ConfigMgr customers, updates selected on this tab are published to WSUS and can then be synchronized into ConfigMgr when Publisher is installed on the Software Update Point (SUP). This allows third-party updates to be deployed and reported on in the same way as Microsoft updates.

Third-party updates synchronized from WSUS to ConfigMgr during a SUP sync will appear in the **Software Library > All Software Updates** node in the ConfigMgr console.

![Updates appear in the All Software Updates view](/_images/image-(426 "Updates appear in the All Software Updates view") (1).png>)

Additional behavior related to update publishing can be configured using the [**Options**](options/) button on the Updates tab.
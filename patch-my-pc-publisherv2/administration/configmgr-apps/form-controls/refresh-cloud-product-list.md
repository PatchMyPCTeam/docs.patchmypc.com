# Refresh Cloud Product List

_Applies to: Patch My PC Publisher V2.x_

## ![](/_images/image-(505).png>) Overview

The **Refresh Cloud Product List** form control refreshes the list of custom products displayed in the **All Custom Products** [product tree](../product-tree.md). This list includes applications that were created as [Custom Apps in a Patch My PC Cloud company](https://docs.patchmypc.com/patch-my-pc-cloud/custom-apps) and synchronized to the Publisher.

The Publisher calls the Patch My PC Cloud Catalog API to retrieve the current list of supported custom products. The returned data is processed and used to update the **All Custom Products** tree on the ConfigMgr Apps tab, ensuring the console reflects any newly created, modified, or removed custom products in the cloud.

The refresh capability requires that the cloud connection is already configured and enabled on the [Cloud](../../cloud.md) tab.
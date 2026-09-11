# Query button in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Query** button on the **Scan Intune** tab of Patch My PC (PMPC) Publisher performs an interactive scan using the current configuration defined on the screen and any applied filters.

<figure><img src="../../../../.gitbook/assets/image.png" alt="&#x27;Query&#x27; button" width="563"><figcaption></figcaption></figure>

When you click **Query**, Publisher queries the obtained Intune report and displays the results. The products shown reflect:

* What applications detected in the Intune report match products in the PMPC catalog.
* The device count for each product.

{% hint style="info" %}
**Note**

The device count value shown for each product match is clickable. Selecting it displays a detailed view of the devices and application versions where the product was detected, allowing you to validate inventory results before enabling or publishing the product.
{% endhint %}

The **Query** button does not enable or publish products by itself; it simply retrieves and displays the results based on the current settings, allowing you to review and validate findings before taking further action.

<figure><img src="../../../../.gitbook/assets/image (4086).png" alt="Query Results" width="563"><figcaption></figcaption></figure>

Selecting products from this list is equivalent to manually selecting the same products in the [Product Tree](../../../fundamentals/product-tree/working.md) either on the **Intune Apps** or **Intune Updates** tabs. When you check a product here, it enables that product for publishing in the same way as selecting it directly in the Product Tree.

{% hint style="danger" %}
**Important**

Because there is no universal standard for how vendors name apps, inventory results cannot always distinguish between multiple variants of the same product. For example, if **7-Zip (x64)** is detected in the Intune report, Publisher cannot reliably determine whether the MSI or EXE installer was originally used, so both variants may be shown as matches. This ensures coverage while acknowledging the limitations of vendor-provided inventory data.
{% endhint %}

### Count

The value shown in the **Count** column shown for each matched product is clickable. Clicking a count opens the **Devices with Application** screen listing the devices where the product was detected, along with the reported app version on each device.

<figure><img src="../../../../.gitbook/assets/image (4151).png" alt="Clicking device count value" width="450"><figcaption></figcaption></figure>

This detailed view allows you to review inventory results and verify product presence and version distribution before enabling or publishing the product.

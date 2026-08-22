# Query button in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Query** button in Patch My PC (PMPC) Publisher performs an interactive scan using the current configuration defined in the form and any filters that have been applied.

When clicked, the Publisher queries the obtained Intune report and displays the results in the list below. The products shown reflect:

* What applications detected in the Intune report matches products in the Patch My PC catalog.
* The device count for each product

{% hint style="info" %}
**Note**

The device count value shown for each product matched is clickable. Selecting it displays a detailed view of the devices and application versions where the product was detected, allowing you to validate inventory results before enabling or publishing the product.
{% endhint %}

The Query button does not enable or publish products by itself, it simply retrieves and displays the results based on the current settings, allowing you to review and validate findings before taking further action.

<figure><img src="../../../../.gitbook/assets/image (4086).png" alt="Query Results" width="563"><figcaption></figcaption></figure>

Selecting products from this list is equivalent to manually selecting the same products in the [Product Tree](../../../fundamentals/product-tree/working.md) either on the Intune Apps tab or Intune Updates tab. When you check a product here, it enables that product for publishing in the same way as selecting it directly in the product tree.

{% hint style="danger" %}
**Important**

Because there is no universal standard for how vendors name applications, inventory results cannot always distinguish between multiple variants of the same product. For example, if 7-Zip (x64) is detected in the Intune report, Publisher cannot reliably determine whether the MSI or EXE installer was originally used, so both variants may be shown as matches. This ensures coverage while acknowledging the limitations of vendor-provided inventory data.
{% endhint %}

### Count

The Count value shown for each matched product is clickable. Selecting the count opens a detailed view that lists the devices where the product was detected, along with the reported application version on each device.

<figure><img src="../../../../.gitbook/assets/image (4151).png" alt="Clicking device count value" width="450"><figcaption></figcaption></figure>

This detailed view allows you to review inventory results and verify product presence and version distribution before enabling or publishing the product.

Clicking Export CSV will generated CSV file includes the following columns:

* **Device Name**\
  The name of the device where the product was detected.
* **Product Name**\
  The application name as reported in inventory.
* **Product Version**\
  The version of the application detected on the device.

# Switch to Full Content/Metadata Only option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Products, Vendor, Product_\
_Available on tab: WSUS Updates_

The [Switch to Full Content](switch-full-content-metadata-only.md#switch-to-full-content) and [Switch to Metadata Only](switch-full-content-metadata-only.md#switch-to-metadata-only) options in Patch My PC (PMPC) Publisher can be used to configure how you want software updates to be published to Microsoft WSUS.

<figure><img src="../../../.gitbook/assets/image (4732).png" alt="&#x27;Switch to Full Content&#x27; and &#x27;Switch to Metadata Only&#x27; options"><figcaption></figcaption></figure>

## Switch to Full Content

Selecting the **Switch to Full Content** option publishes both the update metadata and the update binaries to WSUS.

This option is required when you want ConfigMgr or WSUS to download, distribute, and deploy the update to devices.

## Switch to Metadata Only

Selecting the **Switch to Metadata Only** option publishes the update metadata to WSUS without the installer binaries.

When the **Switch to Metadata Only** option is selected, **(Metadata)** is appended to the end of the product name.

<figure><img src="../../../.gitbook/assets/image (4791).png" alt="&#x27;(Metadata)&#x27; appended to the end of the product name showing &#x27;Switch to Metadata Only&#x27; option is selected for" width="283"><figcaption></figcaption></figure>

Devices can scan against the metadata, which means update compliance and applicability information is still visible in ConfigMgr. However, because the update binaries are not published, WSUS cannot deploy the update to devices.

This option is commonly used to evaluate the impact and requirements of updates across the environment before making them deployable.

{% hint style="info" %}
**Note**

If you select the **Switch to Metadata Only** option and later decide the binaries for that update should be published, you can change that specific update to the **Switch to Full Content** option. On the next sync, Publisher will download the binaries and publish the update with full content automatically.
{% endhint %}

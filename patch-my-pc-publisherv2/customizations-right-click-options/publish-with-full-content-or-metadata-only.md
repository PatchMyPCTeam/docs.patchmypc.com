# Publish with Full-content or Metadata Only

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: All Products, Vendor, Product_\
_&#x41;vailable on tab: Updates_

## Overview

The **Publish with Full-content or Metadata Only** option can be used to configure how you want software updates to be published to WSUS.

![Publishing with Full-content or Metadata Only](/_images/image-(160).png)

## Full Content

Full Content publishes both the update metadata and the update binaries to WSUS.

This option is required when you want ConfigMgr or WSUS to download, distribute, and deploy the update to devices.

## Metadata Only

Metadata Only publishes the update metadata to WSUS without the installer binaries.

Devices can scan against the metadata, which means update compliance and applicability information is still visible in Configuration Manager. However, because the update binaries are not published, WSUS cannot deploy the update to devices.

This option is commonly used to evaluate the impact and requirements of updates across the environment before making them deployable.

> \*\*Note\*\*
>
> If you select the metdata only option, and later decide the binaries for that update should be published, you can change that specific update to Full Content. On the next sync, the Publisher will download the binaries and publish the update with full content automatically.
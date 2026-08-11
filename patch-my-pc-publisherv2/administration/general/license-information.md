# License Information

_Applies to: Patch My PC Publisher V2.x_

## Overview

When the Publisher is launched for the first time, you will be prompted to enter a license key.&#x20;

<figure><img src="../../../.gitbook/assets/image (410).png" alt="" width="545"><figcaption></figcaption></figure>

If you have purchased a license, or if you have requested a free 30-day trial, you will receive an email containing your 20-character license key, which can be entered into the **License Key** field on the **General** tab in the Publisher, to activate the appropriate functionality.

If you do not currently have a license key, you have 2 options:

* Enable Limited Trial Mode, which allows you to evaluate Publisher with a restricted set of products.
* [Request a free 30-day trial](https://patchmypc.com/free-trial) from our website to have your license key emailed to you.

Once a valid license or trial key is entered, Publisher will unlock the corresponding features and allow you to proceed with configuration, customization and publishing.

<figure><img src="../../../.gitbook/assets/image (70).png" alt="Subscription validation succeeded" width="300"><figcaption></figcaption></figure>

If validation fails, the dialog indicates that the key could not be verified and typically suggests checking either the license value or [network connectivity](../../publisher-requirements/core-requirements.md#network).

<figure><img src="../../../.gitbook/assets/image (69).png" alt="License Validation Failed" width="425"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If you started your trial through Patch My PC Cloud, your license key can also be retrieved directly from the Cloud portal by navigating to **Settings > Subscription**, and clicking on the obfiscated license key.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (411).png" alt="" width="563"><figcaption></figcaption></figure>

## Limited Trial Mode

If you do not yet have a license or trial key, the Publisher can be used in Limited Trial Mode. This allows you to evaluate Publisher functionality using a predefined set of products.

<figure><img src="../../../.gitbook/assets/image (71).png" alt="Limited Trial Mode" width="545"><figcaption></figcaption></figure>

### How to enable Limited Trial Mode

1. Launch the Publisher.
2. Navigate to **General > License Information**.
3. Select **Enable limited trial mode**.
4. When prompted, confirm that you want to switch to **Trial Catalog Mode**.

{% hint style="warning" %}
**Important**

Enabling Trial Mode will overwrite any product selections previously made in non-trial mode.
{% endhint %}

Once enabled, the Publisher will automatically populate the product catalog with a limited set of applications that are available for evaluation.

### Products Available in Limited Trial Mode

Limited Trial Mode includes a curated selection of commonly used third-party applications, allowing you to test publishing workflows without requiring a license key.

The following products are available in Limited Trial Mode:

* **Amazon Corretto**
  * Amazon Corretto 8 (x64)
  * Amazon Corretto 8 (x86)
* **Devolutions**
  * Remote Desktop Manager (MSI-x64)
* **Microsoft**
  * Microsoft Power BI Desktop (x64)
* **Mozilla**
  * Mozilla Firefox (x64 en-US)
  * Mozilla Firefox (x86 en-US)
* **VideoLAN**
  * VLC Media Player (x64) – EXE Install
  * VLC Media Player (x64) – MSI Install
  * VLC Media Player (x86) – EXE Install
  * VLC Media Player (x86) – MSI Install
* **Zoom**
  * Zoom Workplace (MSI-x64)
  * Zoom Workplace (MSI-x86)

<figure><img src="../../../.gitbook/assets/image (413).png" alt="Limited Trial Mode available products" width="545"><figcaption></figcaption></figure>

## Subscription Information

This section displays details about your current Patch My PC license, including the subscription tier, license validity period, and the number of devices covered. This information helps confirm that Publisher is correctly licensed for your environment and that your device count aligns with your deployment scope.

<figure><img src="../../../.gitbook/assets/image (414).png" alt="" width="545"><figcaption></figcaption></figure>

* **Subscription level**\
  Indicates the Patch My PC license tier currently applied (for example, _Enterprise Premium_). The subscription level determines the features, products, and capabilities available within Publisher. The [available subscription](https://patchmypc.com/pricing/) levels are:
  * Enterprise Premium
  * Enterprise Plus
  * Enterprise (Enterprise Patch)
* **Expiration date**\
  Shows the date on which the current license or trial expires. Publisher will continue to function normally until this date. Once the license expires, new applications and updates will no longer be published. Any applications and updates that were published prior to the expiration will remain available and unaffected. To avoid interruptions, renewal or trial extension should be planned ahead of the expiration date.
* **Licensed device count**\
  Displays the maximum number of devices covered by the license. This should align with the number of managed devices that will _receive_ applications or updates published by Publisher, which may differ from the total number of managed devices in your environment.

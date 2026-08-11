# Discover Intune Apps and Updates using Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

{% hint style="danger" %}
**Important**

This article has not been updated for Version 3.x. Once it has, this banner will be removed.
{% endhint %}

This page provides guidance on how to discover applications in your environment or manually select products for publishing as Intune apps and Intune updates using the Patch My PC (PMPC) Publisher.

When integrated with Intune, you can scan your tenant to identify supported third party applications that are already discovered. You can also manually browse and select products directly from the Publisher catalog.

After completing the steps in this section, you will be able to enable and publish third party applications and updates to Intune that align with your organization’s requirements.

Difference Between Intune Apps and Intune Updates


Products on both the Intune Apps and Intune Updates tabs are published as Win32 apps and use the same core detection method to determine installation state. The key difference is how applicability is handled.

Intune Apps are designed for initial installation and lifecycle management. They are generally applicable to any targeted device unless restricted by assignment filters or requirements.

Intune Updates, while still Win32 apps, include an additional requirement script. This script evaluates whether an older version of the application is already installed on the device. The update Win32 app is only considered applicable if a previous version is detected. This approach ensures that updates target existing installations rather than installing new applications.

Because Intune does not have a native compliance evaluation model like WSUS, this requirement script based logic is used to simulate update applicability while remaining fully integrated with the native Intune Win32 application model.

Discovering and Selecting Applications


You can enable applications and updates for publishing in one of two ways:

* [Scan Intune for supported products using the Scan Intune for Supported Products wizard](discover-intune-apps-updates.md#scan-intune-for-supported-products-using-the-scan-intune-for-supported-products-wizard).
* [Manually browse and select products directly from the product tree on the Intune Apps and Intune Updates tabs](discover-intune-apps-updates.md#manually-browse-and-select-products-directly-from-the-product-tree-on-the-intune-apps-and-intune-upd).

### Scan Intune for supported products using the Scan Intune for Supported Products wizard

The [Scan Wizard](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/form-controls/scan-intune-for-supported-products.md) is generally a recommended starting point. It leverages Intune Discovered Apps data to identify supported third-party products currently present in your environment and compares those results against the Patch My PC catalog. This allows you to review what is installed today before enabling publishing.

<figure><img src="../../../.gitbook/assets/image (4161).png" alt="Scan Intune for SUpported Products" width="563"><figcaption></figcaption></figure>

After running a scan, review the results carefully. The device count and version information help validate inventory accuracy and determine publishing priority. Exporting the results to CSV can assist with internal review, change control discussions, or phased rollout planning.

A common and effective approach is to begin conservatively. Enable a small number of familiar, low-impact applications to understand how Intune applications and updates are created by the Publisher. Many customers start with widely used utilities such as 7-Zip or Notepad++ to gain confidence in the workflow.

Once you are comfortable with how applications and updates are created and maintained, you can expand product selections or consider enabling [auto-publishing rules](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/form-controls/scan-intune-for-supported-products.md#auto-publishing-rules) to automate application lifecycle management over time to create new applications and updates based on discovery thresholds.

### Manually browse and select products directly from the product tree on the Intune Apps and Intune Updates tabs

Applications and updates can also be enabled manually by selecting products directly from the [product tree](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md) on the [Intune Apps and Intune Updates](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/) tabs.

Manual selection remains a valid and flexible option, especially when you want to proactively publish applications that may not yet appear in the inventory returned by the scan results.

<figure><img src="../../../.gitbook/assets/image (4162).png" alt="Manual Product Selection" width="545"><figcaption></figcaption></figure>

You can expand vendors to browse available products or use the [Search](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/form-controls/search-products.md) form control to quickly locate a specific application by name.

When selecting _applications_, we recommend to standardize on a single installer variant whenever multiple options are available. For example, some products may provide:

* MSI and EXE variants
* x86 and x64 architectures
* ARM64 variants

In most environments, it is recommended to standardize on a single architecture and installer type, such as MSI (x64), unless there is a specific requirement for an alternative variant.\
\
When selecting _updates_, it is often appropriate to enable multiple update variants if they exist in your estate. For example, if both x86 and x64 variants are detected, publishing updates for both ensures all devices remain compliant while you work toward long term standardization.

As a best practice, begin by enabling a small number of familiar, low-impact applications to understand how Intune applications and updates are created by the Publisher. Many customers start with widely used utilities such as 7-Zip or Notepad++ to gain confidence in the workflow.

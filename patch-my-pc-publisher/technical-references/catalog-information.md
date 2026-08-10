# Catalog Information for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

## Product Naming in the Patch My PC Catalog

Product names in the Patch My PC (PMPC) catalog include additional descriptors (such as **MSI**, **EXE**, **x86**, **x64**, **ARM**, **MSP**, and **Latest**) to clearly communicate the installer type, architecture, and update behavior. These indicators help you select the most appropriate variant for your environment and deployment strategy.

Product names follow a consistent pattern to describe the installer and platform at a glance. For example:

<p align="center"><strong>FileMaker Pro 2024 Update (MSP-x64)</strong></p>

This indicates a FileMaker Pro update delivered as an MSP installer for 64-bit systems, while **Clevershare (EXE-x86)** indicates a 32-bit executable installer.

If no architecture is specified in the product name, this typically means the vendor only provides a single supported architecture for that product.

{% hint style="info" %}
**Note**

If no architecture is shown in the product name, you can confirm the exact installer file and architecture by right-clicking the product and selecting [Show Package Info](../customizations/list-customizations/show-package-info.md), which displays the precise installer being used.
{% endhint %}

## Full Content vs Metadata (WSUS Updates tab only)

On the **WSUS Updates** tab, the Product Tree indicates how an update has been configured using the [Switch to Full Content/Metadata Only](../customizations/list-customizations/switch-full-content-metadata-only.md) right-click option.

By default, updates are configured to publish with **Full Content**, meaning the installer binaries will be published to WSUS.

If an update has been configured to publish with **Metadata Only**, then **(Metadata)** is appended to the end of the product name, and only the metadata will be published to WSUS.

<figure><img src="../../.gitbook/assets/image (4791).png" alt="&#x27;(Metadata)&#x27; appended to the end of the product name showing &#x27;Switch to Metadata Only&#x27; option is selected for" width="283"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**&#x20;

See [Switch to Full Content/Metadata Only](../customizations/list-customizations/switch-full-content-metadata-only.md) for more details on this right-click option.
{% endhint %}

### Latest

Some products include **Latest** in the name to indicate dynamic version tracking rather than a fixed release.

For example, **Citrix Workspace LTSR (Latest)** represents the most current major LTSR build published in the PMPC catalog. As newer versions are added to the catalog, the **Latest** entry automatically advances without requiring changes to product selection.

Naming pattern:\
Product Name (Latest) (Installer Type–Architecture)\*

Example:

* Citrix Workspace LTSR (Latest)

<figure><img src="../../.gitbook/assets/image (4793).png" alt="Naming Convention - Latest" width="281"><figcaption></figcaption></figure>

If strict version control is required, select a product entry that includes an explicit major version number instead of **Latest**.

{% hint style="info" %}
**Note**

When a product entry does not include (Installer Type-Architecture) in the name, it can be assumed that the vendor only offers a single variant for that product.
{% endhint %}

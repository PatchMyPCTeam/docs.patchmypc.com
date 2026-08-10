# Catalog Information

_Applies to: Patch My PC Publisher V2.x_

## Product Naming in the Patch My PC Catalog

Product names in the Patch My PC catalog include additional descriptors (such as MSI, EXE, x86, x64, ARM, MSP, and Latest) to clearly communicate installer type, architecture, and update behavior. These indicators help you select the most appropriate variant for your environment and deployment strategy.

Product names follow a consistent pattern to describe the installer and platform at a glance. For example, **FileMaker Pro 2024 Update (MSP-x64)** indicates a FileMaker Pro update delivered as an MSP installer for 64-bit systems, while Clevershare (EXE-x86) indicates a 32-bit executable installer.

Some products include **Latest** in the name to indicate dynamic version tracking. For example, **Citrix Workspace LTSR (Latest)** represents the most current major LTSR build published in the Patch My PC catalog and will automatically advance as newer LTSR major versions are released.

If no architecture is specified in the product name, this typically means the vendor only provides a single supported architecture for that product.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>The **(Full Content)** or **(Metadata)** additional naming suffix only appears in the product tree on the [Updates tab](../administration/updates/overview.md).</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If no architecture is shown in the product name, you can confirm the exact installer file and architecture by using **right-click > Show package info**, which displays the precise installer being used.</p>
</blockquote>

### Full Content vs Metadata (Updates Tab Only)

The product name suffix for (Full Content) or (Metradata) shown in the product tree, on the updates tab, reflects how the update is configured via right-click customization. When an update is set to publish with **Full Content**, the product name includes (Full Content) to indicate that the installer binaries will be published to WSUS. If the update is configured as Metadata only, the name is updated to reflect **Metadata** instead. This naming helps you quickly see how each update will be published at a glance.

![Naming Convention - Full Content / Metadata](/_images/image-(525).png "Naming Convention - Full Content / Metadata")

For more details on changing the default (Full Content) to (Metadata), see [Publishing with Full-content or Metadata Only](../customizations-right-click-options/publish-with-full-content-or-metadata-only.md).

### Latest

Some products include **Latest** as part of the product name to indicate dynamic version tracking rather than a fixed release.

Naming pattern:\
Product Name (Latest) (Installer Type–Architecture)\*

Example:

* Citrix Workspace LTSR (Latest)

![Naming Convention - Latest](/_images/image-(526).png "Naming Convention - Latest")

In these cases, Latest means the product will always align to the most recent major version published within that product line (such as the newest LTSR build). As newer versions are added to the catalog, the Latest entry automatically advances without requiring changes to product selection.

If strict version control is required, select a product entry that includes an explicit major version number instead of Latest.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>When a product entry does not include (Installer Type-Architecture) in the name, it can  be assumed that the vendor only offers a single variant for that product.</p>
</blockquote>
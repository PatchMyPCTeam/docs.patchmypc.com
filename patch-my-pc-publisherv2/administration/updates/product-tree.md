# Product Tree

_Applies to: Patch My PC Publisher V2.x_

## Overview

The product tree is where you choose which updates the Publisher should publish, and keep up to date, in your environment. It’s a hierarchical view that lets you enable updates at different levels of granularity, from all products down to individual products.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>For more detail on product naming conventions in the product tree, refer to [Catalog Information](../../publisher-reference/catalog-information.md).</p>
</blockquote>

## Product Tree Structure

The product tree can be expanded or collapsed to three main levels:

![Product tree structure](/_images/image-(427).png "Product tree structure")

1. **All Products**
   * The root of the tree.
   * Right-clicking this node exposes [customization (right-click) options](../../customizations-right-click-options/) that apply globally to all vendors and products.
2. **Vendor Level** (for example, _Adobe Systems, Inc._)
   * Expanding a vendor shows all supported products from that publisher.
   * Selecting a vendor indicates you want the Publisher to manage updates for _all supported products under that vendor_ (subject to explicit exclusions or customizations).
3. **Product Level** (for example, _Adobe Acrobat Reader DC Continuous (x64)_)
   * This is the most granular level.
   * Selecting an individual product means the Publisher will manage updates only for that specific product.

### What selecting a checkbox means

When you **check a box** at any level in the product tree, you are telling the Publisher:

> "I want you to publish and keep the latest version of this product up to date during the next sync cycle"

* Publisher does **not** immediately publish content when you tick a box.
* The selection is evaluated during the **next sync**, at which point:
  * New updates are published (if available).
  * Content is prepared according to your previous customizations.
  * Superseded updates are handled.

The checkbox states behave as follows:

* Checked (✔) – All products under that node are selected.
* Dash (–) – A partial selection exists (some child products selected, others not).
* Unchecked (☐) – No products under that node are selected.

This visual feedback allows you to quickly understand whether you are managing a single product, a subset of products, or an entire vendor, and gives you precise control over how broadly or narrowly updates are published.

#### Example

In the example below, **8x8 Quality Management (MSI-x86)(Full Content)** demonstrates a single product selection. Only 8x8 Quality Management is checked. The 8x8 vendor checkbox shows a dash (indeterminate state) rather than a full checkmark. This indicates that the Publisher will manage updates for that specific product only, and no other products from the 8x8 vendor will be published at the next Publisher sync.

In contrast, "Adobe Systems, Inc." demonstrates a vendor-level selection. The Adobe vendor checkbox shows a full checkmark rather than a dash (indeterminate state). This indicates that all products under the Adobe vendor are selected.

![Product Tree selection granularity](/_images/image-(428).png "Product Tree selection granularity")

## Which Products should I Select?

### All Products Level

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>It’s **not recommended** to select All Products for publishing in most environments. The Patch My PC catalog contains far more products than are typically installed in any single organization, and selecting _everything_ can lead to unnecessary publishing, storage consumption, and administrative overhead.</p>
</blockquote>

There is only one scenario when selecting All Products might be useful **but only** if you combine it with the [right-click customization option](../../customizations-right-click-options/) to publish metadata-only (not full content).

In this mode:

* Only update metadata is published (no installers or binaries).
* WSUS / ConfigMgr can report compliance data.
* You can see exactly which third-party updates are applicable in your environment.

This allows you to make informed decisions later about which products should be switched to Full Content publishing.

### Vendor Level

Selecting a vendor on the Updates tab is acceptable when you are confident that the vendor has broad coverage in your environment. For example, organizations with widespread Adobe usage may reasonably choose to select the Adobe vendor rather than managing each product individually.&#x20;

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Products marked with **Latest** in the update name will always update a client to the **vendor’s latest major version**.</p>
</blockquote>

#### (Latest) Version Consideration

In the example below, selecting **Cisco Jabber Latest (MSI-x86)(Full Content)** means devices targeted with this update that are running **Jabber 14.x** will be upgraded to **15.x** automatically

* This may be undesirable if:
  * Your organization has not validated the new major version
  * The upgrade introduces breaking changes
  * Compatibility with other systems is not yet confirmed

![Vendor level selection consideration](/_images/image-(429).png "Vendor level selection consideration")

In this scenario, selecting individual major versions (for example, Cisco Jabber 14) at the [product level](product-tree.md#product-level-recommended) provides significantly more control over update behavior and helps avoid unintended major version upgrades. If your environment standardizes on Jabber 14.x, selecting a Latest product would eventually move devices to Jabber 15.x once it becomes the vendor’s current release, which may not be desirable due to compatibility, change control, or user impact considerations.&#x20;

For this reason, product-level selection is often the safer and more predictable approach, especially for applications where major upgrades introduce functional changes or require additional validation.

### Product Level (Recommended)

It's recommend to start conservatively with product selection for your publishing intent:

1. Begin with **a small number of familiar, well-understood products.**
2. Observe update behavior, detection, deployment, and user impact.
3. Gradually expand product or vendor selections as confidence grows.

This phased approach reduces risk, improves predictability, and helps ensure that third-party patching aligns with your organization’s operational and change-management practices.

### Discovery

If you’re unsure which products exist in your environment, which makes manual product selection difficult, the Scan Wizard is often the best starting point.

In ConfigMgr environments, the Scan Wizard leverages hardware inventory data from ConfigMgr clients which provides accurate visibility into installed third-party software. More details on the Scan Wizard and be found on the [Form Controls](form-controls/) page.

In WSUS-only environments, where hardware inventory data is not available, metadata-only publishing remains the recommended method for identifying applicable updates. More details on metadata-only publishing can be found on the [Customizations (Right-Click Options)](../../customizations-right-click-options/) and [Publisher References](../../publisher-reference/catalog-information.md#full-content-vs-metadata-updates-tab-only) pages.

## Iconography

Within the Publisher, the product tree uses visual indicators to highlight when additional attention or configuration is required before an app or update can be published successfully. These icons are designed to make potential blockers obvious at a glance.

### ![](/_images/image-(430).png>) **Manage Conflicting Processes**

A blue cross icon indicates that the application has **conflicting running processes** that must be handled during installation or upgrade. The appliction being upgraded on the client must be **closed** for a successful install, upgrade, or repair.

When a product that contains conflicting processes is selected, the **Manage Conflicting Processes** [customization](../../customizations-right-click-options/) option is automatically enabled. By default, this is set to **Skip installation when conflicting processes are in use**, ensuring that updates do not fail or forcibly interrupt users if the application is currently running. This default provides a safe and predictable upgrade path and can be adjusted if a different behavior is required, like prompting the user to close the open application before the update installation begins.

### ![](/_images/image-(431).png>) **Customer-Provided Installer Required**

The blue download arrow means that **Publisher cannot automatically download the installer binary** from the vendor and customer action is required.

This typically occurs when:

* The vendor hosts the installer behind a customer login or support portal.
* The installer must be manually downloaded and extracted before it can be used.

In these scenarios, the customer must supply the installer using one of the supported customization options.

For step-by-step guidance, refer to:

* [Customizations](../../customizations-right-click-options/)
* [Advanced > Local Content Repository](../advanced/)

These pages explains how to store and reference customer-provided binaries so the Publisher can consume them during publishing.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>This feature is also referred to as "Binary free apps" and leverages the "Local Content Repository".</p>
</blockquote>
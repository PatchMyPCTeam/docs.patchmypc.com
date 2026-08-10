# Overview of the Product Tree in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The _Product Tree_ in Patch My PC (PMPC) Publisher is where you choose which products and updates the Publisher should publish and update for each supported management platform

It is a hierarchical view that lets you enable updates at different levels of granularity, from all products for a vendor down to individual products.

> \*\*Tip\*\*
>
> For more details on product naming conventions in the product tree, refer to \[Catalog Information]\(../../technical-references/catalog-information.md).

> \*\*Note\*\*
>
> The majority of user interface elements are the same across all supported management platforms. However, there are some specifics which are documented in the relevant section.

## Product Tree Structure

The Product Tree can be expanded or collapsed to three main levels:

![Product Tree Structure](../../../.gitbook/assets/image-\(4516\).png)

1. **All Vendors**
   * The root of the tree.
   * Right-clicking this node exposes [customization (right-click) options](../../customizations/overview.md) that apply globally to all vendors and products.
2. **Vendor Level** (for example, _3CX Ltd._)
   * Expanding a vendor shows all supported products from that vendor.
   * Selecting a vendor indicates that you want Publisher to manage updates for all _supported products under that vendor_ (subject to explicit exclusions or customizations).
3. **Product Level** (for example, _3CXPhone for Windows (MSI-x86)_)
   * This is the most granular level.
   * Selecting an individual product means Publisher will manage updates only for that specific product.

## What selecting a checkbox means

When you check a box at any level in the Product Tree, you are telling Publisher:

> "_I want you to publish and keep the latest version of this product up to date during the next sync cycle._"

However:

* Publisher does **not** immediately publish content when you check a box.
* The selection is evaluated during the **next sync**, at which point:
  * New updates are published (if available).
  * Content is prepared according to your previous customizations.
  * Superseded updates are handled.

The checkbox states behave as follows:

* Checked (✔) – All products under that node are selected.
* Colored square (!\[Colored square]\(/\_images/image-(4515 "Colored square").png>)) – A partial selection exists (some child products selected, others not).
* Unchecked (☐) – No products under that node are selected.

This visual feedback allows you to quickly understand whether you are managing a single product, a subset of products, or an entire vendor, and gives you precise control over how broadly or narrowly updates are published.

### Example

In the example below, only the **3CXPhone for Windows (MSI-x86)** checkbox is checked, showing a single product selection. The **3CX Ltd** checkbox shows a colored square (indeterminate state) rather than a full checkmark. This indicates that Publisher will manage updates for that specific product only, and no other products from the **3CX Ltd** vendor will be published at the next Publisher sync.

![Product level selection](../../../.gitbook/assets/image-\(4747\).png)

In contrast, **8x8, Inc.** demonstrates a vendor-level selection. The **8x8, Inc.** checkbox shows a full checkmark rather than a colored square (indeterminate state). This indicates that all products under the **8x8, Inc.** vendor are selected.

![Vendor level example](../../../.gitbook/assets/image-\(4748\).png)

## Which Products should I select?

### All Vendors Level

> \*\*Important\*\*
>
> We do not recommend selecting \*\*All Vendors\*\* for publishing in most environments. The Patch My PC catalog contains far more products than are typically installed in any single organization, and selecting \_everything\_ can lead to unnecessary publishing, storage consumption, and administrative overhead.

The only scenario for selecting **All Vendors** is if you combine it with the [right-click customization option](../../customizations/) to publish metadata-only (not full content).

In this mode:

* Only update metadata is published (no installers or binaries).
* Microsoft WSUS/ConfigMgr can report compliance data.
* You can see exactly which third-party updates are applicable in your environment.

This allows you to make informed decisions later about which products to switch to Full Content publishing.

### Vendor Level

Selecting a vendor is acceptable when you are confident that the vendor has broad coverage in your environment. For example, organizations with widespread Adobe usage may reasonably choose to select the Adobe vendor rather than managing each product individually.

> \*\*Important\*\*
>
> Products marked with \*\*Latest\*\* in the update name will always update a computer to the vendor’s latest major version.

#### (Latest) Version Consideration

In the example below, selecting **Cisco Jabber Latest (MSI-x86)** means devices targeted with this update that are running **Jabber 14.x** will be upgraded to **15.x** automatically

This may be undesirable if:

* Your organization has not validated the new major version
* The upgrade introduces breaking changes
* Compatibility with other systems is not yet confirmed.

![(Latest) Version Consideration](../../../.gitbook/assets/image-\(4519\).png)

In this scenario, selecting individual major versions (for example, Cisco Jabber 14) at the [product level](overview.md#product-level-recommended) provides significantly more control over update behavior and helps prevent unintended major-version upgrades.

If your environment standardizes on Jabber 14.x, selecting a **Latest** product would eventually move devices to Jabber 15.x once it becomes the vendor’s current release, which may not be desirable due to compatibility, change control, or user impact considerations.

For this reason, product-level selection is often the safer and more predictable approach, especially for applications where major upgrades introduce functional changes or require additional validation.

### Product Level (Recommended)

We recommend you start conservatively with product selection for your publishing intent:

1. Begin with a small number of familiar, well-understood products.
2. Observe update behavior, detection, deployment, and user impact.
3. Gradually expand product or vendor selections as confidence grows.

This phased approach reduces risk, improves predictability, and helps ensure that third-party patching aligns with your organization’s operational and change-management practices.

### Discovery

If you’re unsure which products exist in your environment, which makes manual product selection difficult, the _Scan ConfigMgr_ feature is often the best starting point.

In ConfigMgr environments, the Scan ConfigMgr feature leverages hardware inventory data from ConfigMgr clients, which provides accurate visibility into installed third-party software.

> \*\*Note\*\*
>
> See \[Scan ConfigMgr]\(../../manage/configmgr-apps-tab/scan-configmgr.md) for information on the Scan ConfigMgr feature.

In WSUS-only environments, where hardware inventory data is not available, metadata-only publishing remains the recommended method for identifying applicable updates.

> \*\*Note\*\*
>
> See \[Customizations (Right-Click Options)]\(../../customizations/) and \[Catalog]\(../../technical-references/catalog-information.md#full-content-vs-metadata-updates-tab-only) for more details on metadata-only publishing.

## Iconography

Publisher's Product Tree uses visual indicators to highlight when additional attention or configuration is required before an app or update can be published successfully. These icons are designed to make potential blockers obvious at a glance.

### !\[Manage Conflicting Processes]\(/\_images/image-(4520 "Manage Conflicting Processes").png>) **Manage Conflicting Processes**

A blue cross icon indicates that the application has processes running that conflict with the installation, upgrade, or repair of the application.

To handle these processes, the application in question must be closed.

When a product containing conflicting processes is selected, the [Manage Conflicting Processes](../../customizations/list-customizations/manage-conflicting-processes/overview-guidance.md) customization option is automatically enabled. By default, this is set to **Skip installation when conflicting processes are in use**, which ensures updates do not fail or forcibly interrupt users if the application is currently running. This default also provides a safe and predictable upgrade path and can be adjusted if different behavior is required, such as prompting the user to close the open application before the update installation begins.

### &#x20;Dependencies

The blue _chain_ icon indicates that the product has one or more dependencies. Right-clicking on the product and selecting **Show Dependencies** opens a window showing the relevant product(s).

![Show dependencies](../../../.gitbook/assets/image-\(4525\).png)

### !\[Customer-Provided Installer Required]\(/\_images/image-(4522 "Customer-Provided Installer Required").png>) **Customer-Provided Installer Required**

The blue download arrow means Publisher cannot automatically download the installer binary from the vendor and customer intervention is required.

This typically occurs when:

* The vendor hosts the installer behind a customer login or support portal.
* The installer must be manually downloaded and extracted before it can be used.

In these scenarios, the customer must supply the installer using one of the supported customization options.

For step-by-step guidance, refer to:

* [Customizations](../../customizations/)
* [Advanced | Staged Content Repository](../../manage/advanced-tab/staged-content-repository.md)

These pages explain how to store and reference customer-provided binaries so Publisher can consume them during publishing.

> \*\*Note\*\*
>
> This feature is also referred to as \*\*Binary Free apps\*\* and leverages the \[Staged Content Repository]\(../../manage/advanced-tab/staged-content-repository.md).

> \*\*Tip\*\*
>
> Once you have selected an item in the Product Tree, you can further customize it by using the right-click options available. See \[Overview of Customizations]\(../../customizations/overview.md) for more details.

# Working with the Product Tree in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The _Product Tree_ in Patch My PC (PMPC) Publisher can be found on the following tabs:

* WSUS Updates
* ConfigMgr Apps
* Intune Apps
* Intune Updates

It works fundamentally the same regardless of the tab you are working with and includes the following:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><a href="working.md#power-button">Power Button</a></td><td valign="top"><a href="working.md#view-button">View Button</a></td><td valign="top"><a href="working.md#settings-button">Settings Button</a></td></tr><tr><td valign="top"><a href="working.md#product-tabs">Product Tabs</a></td><td valign="top"><a href="working.md#filter-field">Filter Field</a></td><td valign="top"><a href="working.md#refresh-button">Refresh Button</a></td></tr><tr><td valign="top"><a href="working.md#product-counts">Product Counts</a></td><td valign="top"><a href="working.md#group-product-variants-button">Group Product Variants Button</a></td><td valign="top"><a href="working.md#product-statistics">Product Statistics</a></td></tr><tr><td valign="top"><a href="working.md#all-vendors-button">All Vendors Button</a></td><td valign="top"><a href="working.md#copy-products-button">Copy Products Button</a></td><td valign="top"><a href="working.md#expand-all-tree-nodes-button">Expand All Tree Nodes Button</a></td></tr><tr><td valign="top"><a href="working.md#filters-button">Filters Button</a></td><td valign="top"></td><td valign="top"></td></tr></tbody></table>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Any platform-specific differences are detailed in the _Product Tree_ article for that platform.</p>
</blockquote>

## ![Power button ](/_images/image-(4574 "Power button ").png>) Power Button

The _Power_ button controls whether products and updates are enabled for the selected management platform, with <mark style="color:red;">Red</mark> indicating the management platform is disabled and <mark style="color:$success;">Green</mark> indicating it is enabled.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>By default, the publishing of all apps and updates is disabled.</p>
</blockquote>

## View Button

The _View_ button lets you switch the view of the Product Tree between _Grid View_ (![Grid view](/_images/image-(4581 "Grid view").png>)) and _Tree View_ (![Tree View](/_images/image-(4580 "Tree View").png>)).

This is an example of the Product Tree shown in _Grid View_.

![Product Tree in Grid View](/_images/image-(4567).png "Product Tree in Grid View")

This is an example of the Product Tree shown in _Tree View_.

![Product Tree in Tree View.](/_images/image-(4568).png "Product Tree in Tree View.")

### Grid View Versus Tree View

There are several benefits to working with the Product Tree in Grid View:

* [Grouping variants](working.md#grouping-variants)
* [Alphabetical slider](working.md#alphabetical-slider)

#### Grouping variants

The greatest benefit of viewing the Product Tree in Grid view is that it allows you to group all product variants into a single card using the [Group Product Variants](working.md#group-product-variants-button) button (only available in Grid view).

#### Alphabetical slider

The alphabetical slider lets you either go directly to all products in the catalog beginning with a certain letter, or navigate the catalog using the arrow controls.

![Alphabetical slider](/_images/image-(3).png "Alphabetical slider")



## ![Settings button](/_images/image-(4579 "Settings button").png>) Settings Button

Clicking the _Settings_ button takes you to the corresponding tab where you can configure additional options.

<table><thead><tr><th width="374" valign="top">Clicking Settings for...</th><th valign="top">Takes you to...</th></tr></thead><tbody><tr><td valign="top">WSUS Updates</td><td valign="top">WSUS Options</td></tr><tr><td valign="top">ConfigMgr Apps</td><td valign="top">Base Install Options</td></tr><tr><td valign="top">intune Apps</td><td valign="top">Intune Options</td></tr><tr><td valign="top">Intune Updates</td><td valign="top">Intune Options</td></tr></tbody></table>

## Product Tabs

Above the Product Tree, you will see the following two tab&#x73;**\***:

* **Catalog Products -** Contains all of the products in the Patch My PC catalog.
* **Custom Products -** Used to manage custom application creation and behavior for[ Custom Apps created in Patch My PC Cloud](https://docs.patchmypc.com/patch-my-pc-cloud/custom-apps).

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>**\*** The **Custom Products** tab is unavailable on the **WSUS Updates** tab.</p>
</blockquote>

Having these as separate tabs allows you to easily configure and manage the products you want to manage in your environment.

## Filter Field

Using the **Filter** field, you can easily filter the Product Tree to only show matching results.

![using the 'Filter' field](/_images/image-(4).png "using the &#x27;Filter&#x27; field")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Using the **Filter** field in conjunction with the [Filters Button](working.md#filters-button) allows you to easily locate the products you wish to manage with Publisher.</p>
</blockquote>

## ![Refresh button](/_images/image-(4582 "Refresh button").png>) Refresh Button

The _Refresh_ button manually refreshes the Product Tree to pick up any changes such as a new product being added to our public catalog or if you add a custom product.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The Product Tree does not auto-refresh in Publisher until you either click the Refresh button or exit and reload Publisher.</p>
</blockquote>

## Product Counts

The _Product Counts_ indicator shows:

* **Selected -** The number of products you have selected in the Product Tree.
* **Filter -** The number of products selected, based on any filters you have applied. The initial number shown is the number of products filtered by the management platform you have selected (e.g., WSUS Updates, ConfigMgr apps, etc.). Then, as you apply additional [Filters](working.md#filters-button), this number updates accordingly.&#x20;

## Group Product Variants Button

The _Group Product Variants_ button (Grid View only) allows you to group all product variants into a single card.

This is an example of the Grid View without variant grouping. Notice how each product variant is shown on a separate card.

![Grid View without variant grouping](/_images/image-(4569).png "Grid View without variant grouping")

Contrast this to Grid View with variant grouping enabled, and you'll notice each product only has a single card, but the total number of variants is shown.

![Grid View with variant grouping enabled](/_images/image-(4571).png "Grid View with variant grouping enabled")

Clicking the down arrow on the product's card shows more details for each variant.

![Displaying variant information](/_images/image-(4572).png "Displaying variant information")

## ![Product Statistics](/_images/image-(4556 "Product Statistics").png>) Product Statistics

The _Product Statistics_ button toggles on the _Stats View_ underneath the Product Tree, where the green stats are installers, and the others are groups of our right-click options.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [List of Product Statistics](../../technical-references/list-product-statistics.md) for a list of available statistics and their purpose.</p>
</blockquote>

![Product Statistics enabled](/_images/image-(4557).png "Product Statistics enabled")

Clicking any stat filters the catalog to display only items that match the selected stat.

## All Vendors Button

The _Group Product Variants_ button (Grid View only), shows all of the [customization (right-click) options](../../customizations/overview.md) that apply globally to all vendors and products. This is the same as right-clicking the root node of the Product Tree when it is in Tree View.

![All Vendors button](/_images/image-(4583).png "All Vendors button")



## Copy Products Button

The _Copy Products_ button synchronizes product selections and/or customizations to other tabs. This option is intended to provide a quick and consistent way to align application management behavior with update publishing selections while preserving the standard inheritance behavior of the product tree.

## Expand All Tree Nodes Button

The _Expand All Tree Nodes_ button (Tree View only) will either expand or collapse the Product Tree if it is being viewed in Tree View.

!['Expand All Tree Nodes' button](/_images/image-(4584).png "&#x27;Expand All Tree Nodes&#x27; button")

## ![Filter option](/_images/image-(4558 "Filter option").png>) Filters Button

The Product Tree includes optional filters to make it easier to sort and work with products and their settings.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Using the **Filter Button** field in conjunction with the [Filter](working.md#filter-field) field allows you to easily locate the products you wish to manage with Publisher.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Filters can also be used in combination with [Product Statistics](working.md#product-statistics) to give you even more powerful capabilities.</p>
</blockquote>

To apply a filter(s):

1. Click the filter button to enable it.

![Clicking the 'Filter' button to enable it.](/_images/image-(4559).png "Clicking the &#x27;Filter&#x27; button to enable it.")

2. Click the required filter(s) to filter the Product Tree as required.

![Clicking the required filter(s) to filter the Product Tree as required.](/_images/image-(4560).png "Clicking the required filter(s) to filter the Product Tree as required.")

The Product Tree will update according to the filters selected and shows the **Active** text to indicate filters have been applied to the Product Tree.

![Filters Product Tree](/_images/image-(4561).png "Filters Product Tree")

### Saving Filters

If you use the filtering capabilities frequently, you can save different filter combinations so you don't have to recreate them each time you filter the Product Tree in a specific way.

To save a set of filters:

1. Apply the required filters.
2. Under the **Saved Filters** section, click the save icon.

![Clicking the save icon](/_images/image-(4564).png "Clicking the save icon")

3. On the **Save Filter Preset** screen, enter a name for this configuration and click **OK**

![Enter name for the filter set](/_images/image-(4565).png "Enter name for the filter set")

The saved filter set appears in the **Saved Filters** section.

![Saved Filter](/_images/image-(4566).png "Saved Filter")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>To apply a previously saved filter set, simply select it from the **Saved Filters** dropdown, and it will be automatically loaded and applied.</p>
</blockquote>

### Clear All Filters

Clicking **Clear All Filters** in either the **Filters** sidebar or Product Statistics (at the bottom of the screen if enabled), will clear any filters and stats you have configured.
# Manage Categories

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_
\
_Available on tab: ConfigMgr Apps, Intune Apps, Intune Updates_

Manage Categories allows you to define which categories are assigned to applications and updates published by the Publisher.

![Manage Categories](/_images/image-(4046).png "Manage Categories")

Categories are used to organize applications into meaningful groupings such as Browsers, Departments, or Development Tools. Assigning categories helps administrators manage large application catalogs and improves the user experience when browsing for software in the ConfigMgr Software Center or the Intune Company Portal.

The list of available categories is pulled directly from the selected management platform. Existing categories are displayed automatically, and new categories can be created by selecting the **+** button. Categories created in this way are added to the underlying platform and then become available for selection.

In ConfigMgr, categories are configured directly on applications in the console and can be scoped to User Categories or Device Categories.

![ConfigMgr Categories](/_images/image-(4048).png "ConfigMgr Categories")

In Intune, application categories are managed in the Intune admin center and are used to organize apps in the Company Portal.

![Intune Categories](/_images/image-(4047).png "Intune Categories")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Categories are applied to newly created applications and updates during publishing. For existing applications and updates, categories are added during the next Publisher synchronization, but previously assigned categories are not removed.&#x20;</p>
<p>The Publisher always ensures that the currently configured categories are present for newly created content.</p>
</blockquote>
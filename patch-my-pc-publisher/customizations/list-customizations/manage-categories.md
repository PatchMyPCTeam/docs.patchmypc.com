# Manage Categories option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps, Intune Apps, Intune Updates_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Manage Categories** right-click option in Patch My PC (PMPC) Publisher allows you to define which categories are assigned to applications and updates published by Publisher.

Categories are used to organize applications into meaningful groupings such as Browsers, Departments, or Development Tools. Assigning categories helps administrators manage large application catalogs and improves the user experience when browsing for software in the ConfigMgr Software Center or the Intune Company Portal.

The list of available categories is pulled directly from the selected management platform. Existing categories are displayed automatically, and new categories can be created by selecting the **+** button. Categories created in this way are added to the underlying platform and then become available for selection.

In ConfigMgr, categories are configured directly on applications in the console and can be scoped to User Categories or Device Categories.

![ConfigMgr Categories](/_images/image-(4048).png)

In Intune, application categories are managed in the Intune admin center and are used to organize apps in the Company Portal.

![Intune Categories](/_images/image-(4047).png)

> \*\*Note\*\*
>
> Categories are applied to newly created applications and updates during publishing. For existing applications and updates, categories are added during the next Publisher synchronization, but previously assigned categories are not removed.
>
> The Publisher always ensures that the currently configured categories are present for newly created content.
# Manage Categories option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps, Intune Apps, Intune Updates_

The **Manage Categories** right-click option in Patch My PC (PMPC) Publisher allows you to define which categories are assigned to applications and updates published by Publisher.

_Categories_ organize applications into meaningful groupings such as **Browsers**, **Departments**, or **Development Tools**. Assigning categories helps administrators manage large application catalogs and improves the user experience when browsing for software in the ConfigMgr Software Center or Intune Company Portal.

The list of available categories is pulled directly from the selected management platform. Existing categories are displayed automatically, and you can create new categories by selecting the **+** button. Categories created in this way are added to the underlying platform and then become available for selection.

In ConfigMgr, you configure categories directly on applications in the console and can scope them to User Categories or Device Categories.

<figure><img src="../../../.gitbook/assets/image (4048).png" alt="ConfigMgr Categories" width="563"><figcaption></figcaption></figure>

In Intune, you manage application categories in the **Intune admin center**, where you use them to organize apps in the Company Portal.

<figure><img src="../../../.gitbook/assets/image (798).png" alt="Intune Categories" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Categories are applied to newly created applications and updates during publishing. For existing applications and updates, categories are added during the next Publisher synchronization, but previously assigned categories are not removed.

Publisher always ensures that newly created content includes the currently configured categories.
{% endhint %}

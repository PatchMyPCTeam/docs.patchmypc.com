---
description: >-
  Enabling and creating Intune Applications in the Patch My PC publishing
  service.
---

# Intune Apps

_Applies to: On-premises Publisher_

## Feature Enablement

To enable products to publish, check the "**Enable creation of Win32 applications in Microsoft Intune**" checkbox.

![Intune App Enablement](/_images/FeatureEnablement_IntuneApps-(1 "Intune App Enablement").png>)

Once the option is selected, you'll be able to enable other products. When first getting started with the product, it is recommended that you only **choose one or two products** to reduce the impact on the first sync and to validate your implementation quickly. We have found that **Notepad++** and **7-Zip** tend to be great initial use case tests.

> \*\*Tip\*\*: We recommend enabling \*\*Manage Conflicting Processes\*\* for \*\*Notepad++\*\*

{% embed url="https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications" %}

To find and enable these products, you can search the list of products using **Ctrl + F** or by clicking on the magnifying glass in the lower right corner.

![Select the search option](/_images/Search_IntuneApps-(1 "Select the search option").png>)

When you select the search button a dialogue will open, type in one of our example products and hit enter, or click OK.

![Search for product](/_images/SearchTerms-(1 "Search for product").png>)

Once you have found the product you want to patch, click the checkbox for your architecture choice and click **Apply**.

> \*\*Tip\*\*: You can right-click All Products, Vendors, or individual Products to apply custom installation options as described in the article below.

{% embed url="https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications" %}
Custom right-click options for customizing installation behavior
{% endembed %}

![Select and Enable a product](/_images/SelectAppAndApply_IntuneApps-(1 "Select and Enable a product").png>)

> If you hit \*\*OK\*\* instead of \*\*Apply\*\*, don't worry as the Publisher will close after saving the changes. You can just re-open and keep right on working.
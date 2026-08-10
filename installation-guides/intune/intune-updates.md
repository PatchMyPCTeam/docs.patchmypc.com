---
description: Enabling and creating Intune Updates in the Patch My PC publishing service.
---

# Intune Updates

_Applies to: On-premises Publisher_

## Feature Enablement&#x20;

To enable products to publish, check the "**Enable creation of Win32 updates in Microsoft Intune**" checkbox.

![Enable Intune Updates feature](/_images/FeatureEnablement_IntuneUpdates.png "Enable Intune Updates feature")

Once the option is selected, you'll be able to enable other products. When first getting started with the product, it is recommended that you only **choose one or two products** to reduce the impact on the first sync and to validate your implementation quickly. We have found that **Notepad++** and **7-Zip** tend to be great initial use case tests.

<blockquote class="wp-block-quote">
<p>**Tip**: We recommend enabling **Manage Conflicting Processes** for **Notepad++**</p>
</blockquote>

{% embed url="https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications" %}

To find and enable these products, you can search the list of products using **Ctrl + F** or by clicking on the magnifying glass in the lower right corner.&#x20;

![Select the search option](/_images/Search_IntuneUpdates.png "Select the search option")

When you select the search button a dialogue will open, type in one of our example products and hit enter, or click OK.

![Search for a product](/_images/SearchTerms.png "Search for a product")

Once you have found product you want to patch, click the checkbox for your architecture choice and click apply.

![Select the products and hit apply](/_images/SelectAppAndApply_IntuneUpdates.png "Select the products and hit apply")

<blockquote class="wp-block-quote">
<p>If you happen to hit **OK**  instead of **Apply**, don't worry the publisher will close after saving the changes. You can just re-open and keep right on working.</p>
</blockquote>

At this time you have completed the basic setup steps and are ready to continue to your first sync!
---
description: >-
  Let's get started by enabling a couple of updates to verify we can publish to
  WSUS.
---

# Updates (On-premises Publisher)

_Applies to: On-premises Publisher_

## Feature Enablement&#x20;

To enable products to publish, check the **Enable publishing of third-party updates** checkbox.

![](<../../_images/gitbook/image%20%281214).png>)

Once the option is selected, you'll be able to enable other products.&#x20;

{% hint style="success" %}
**Tip**: When first getting started with the product, it is recommended that you only **choose one or two products** to reduce the time of the first sync and to validate your implementation quickly. We have found that **Notepad++** and **7-Zip** tend to be great initial use case tests.
{% endhint %}

To find and enable these products, you can search the list of updates using **Ctrl + F** or by clicking on the magnifying glass in the lower right corner.&#x20;

![](<../../_images/gitbook/image%20%281099).png>)

When you select the search button a dialogue will open, type in one of our example products and hit enter, or click **OK**.

![](<../../_images/gitbook/image%20%281126).png>)

Once you have found the product you want to patch, click the checkbox for your preferred architecture choice and click **Apply**.

{% hint style="success" %}
**Tip**: You can right-click All Products, Vendors, or individual Products to **apply custom installation options** as described in the article below.
{% endhint %}

{% embed url="https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications" %}
Custom right-click options for customizing installation behavior
{% endembed %}

![](<../../_images/gitbook/image%20%281154).png>)

{% hint style="info" %}
If you happen to hit **OK**  instead of **Apply**, don't worry the publisher will close after saving the changes. You can just re-open and keep right on working.
{% endhint %}

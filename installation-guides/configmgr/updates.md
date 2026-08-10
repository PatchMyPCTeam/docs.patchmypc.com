---
description: >-
  Initial Updates configuration. It's always a good idea to start with the
  basics.
---

# Updates (On-premises Publisher)

_Applies to: On-premises Publisher_

## Feature Enablement&#x20;

To enable products to publish, check the **Enable publishing of third-party updates** checkbox.

![Feature enablement for updates](<../../.gitbook/assets/image (1771).png>)

Once the option is selected, you'll be able to enable other products.&#x20;

{% hint style="success" %}
**Tip**: When first getting started with the product, it is recommended that you only **choose one or two products** to reduce the time of the first sync and to validate your implementation quickly. We have found that **Notepad++** and **7-Zip** tend to be great initial use case tests.
{% endhint %}

To find and enable these products, you can search the list of updates using **Ctrl + F** or by clicking on the magnifying glass in the lower right corner.&#x20;

![Select the search icon](<../../.gitbook/assets/image (1892).png>)

When you select the search button a dialogue will open, type in one of our example products and hit enter, or click **OK**.

![Search box options for the Updates Tab](<../../.gitbook/assets/image (1867).png>)

Once you have found the product you want to patch, click the checkbox for your preferred architecture choice and click **Apply**.

{% hint style="success" %}
**Tip**: You can right-click All Products, Vendors, or individual Products to **apply custom installation options** as described in the article below.
{% endhint %}

{% embed url="https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications" %}
Custom right-click options for customizting installation behaivor
{% endembed %}

![Select a product and hit apply so save the configuration.](<../../.gitbook/assets/image (1973).png>)

{% hint style="info" %}
If you happen to hit **OK**  instead of **Apply**, don't worry the publisher will close after saving the changes. You can just re-open and keep right on working.
{% endhint %}

Next, you will need to enable the product in Configuration Manager to ensure the updates appear and become deployable via Configuration Manager. To do this first, you will need to complete a normal publisher sync. This will insert the updates into the WSUS database for each product selected. Once the updates are in the WSUS database, we will then need to pull them into ConfigMgr with a Software Update Point sync. You can run a publisher sync at any time from the sync schedule tab. Within that tab, there is an option to “**Trigger SCCM software update point sync when new third-party updates are published**”. With that option enabled, a Software Update Point sync will occur after the publisher sync. Alternatively, you can leave that box unchecked and run a SUP sync manually. Upon completion of the publisher and SUP sync a new product called '**Patch My PC**' will become available in the software update point configuration tab. To reach this tab you will need to navigate to sites, right click the primary or CAS, select configure site components and choose Software Update Point.



![Configure Software Update Point Tab](<../../.gitbook/assets/image (1793).png>)

{% hint style="info" %}
Note: If your SUP is remote, you will need to Configure the SMS Provider connection before running the publisher and SUP sync. This can be done under the Sync Schedule tab, by selecting “Configure SMS Provider connection..”.
{% endhint %}

Once this loads, select products and check the entire Patch My PC category.&#x20;

![Enable the patch my pc product category.](<../../.gitbook/assets/image (1831).png>)

Once enabled, the next software update point sync will pull in all updates created by Patch My PC.

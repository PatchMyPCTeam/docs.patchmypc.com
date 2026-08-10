---
description: >-
  Initial Updates configuration. It's always a good idea to start with the
  basics.
---

# Updates (On-premises Publisher)

_Applies to: On-premises Publisher_

## Feature Enablement&#x20;

To enable products to publish, check the **Enable publishing of third-party updates** checkbox.

![Feature enablement for updates](/_images/image-(1771 "Feature enablement for updates").png>)

Once the option is selected, you'll be able to enable other products.&#x20;

<blockquote class="wp-block-quote">
<p>**Tip**: When first getting started with the product, it is recommended that you only **choose one or two products** to reduce the time of the first sync and to validate your implementation quickly. We have found that **Notepad++** and **7-Zip** tend to be great initial use case tests.</p>
</blockquote>

To find and enable these products, you can search the list of updates using **Ctrl + F** or by clicking on the magnifying glass in the lower right corner.&#x20;

![Select the search icon](/_images/image-(1892 "Select the search icon").png>)

When you select the search button a dialogue will open, type in one of our example products and hit enter, or click **OK**.

![Search box options for the Updates Tab](/_images/image-(1867 "Search box options for the Updates Tab").png>)

Once you have found the product you want to patch, click the checkbox for your preferred architecture choice and click **Apply**.

<blockquote class="wp-block-quote">
<p>**Tip**: You can right-click All Products, Vendors, or individual Products to **apply custom installation options** as described in the article below.</p>
</blockquote>

{% embed url="https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications" %}
Custom right-click options for customizting installation behaivor
{% endembed %}

![Select a product and hit apply so save the configuration.](/_images/image-(1973 "Select a product and hit apply so save the configuration.").png>)

<blockquote class="wp-block-quote">
<p>If you happen to hit **OK**  instead of **Apply**, don't worry the publisher will close after saving the changes. You can just re-open and keep right on working.</p>
</blockquote>

Next, you will need to enable the product in Configuration Manager to ensure the updates appear and become deployable via Configuration Manager. To do this first, you will need to complete a normal publisher sync. This will insert the updates into the WSUS database for each product selected. Once the updates are in the WSUS database, we will then need to pull them into ConfigMgr with a Software Update Point sync. You can run a publisher sync at any time from the sync schedule tab. Within that tab, there is an option to “**Trigger SCCM software update point sync when new third-party updates are published**”. With that option enabled, a Software Update Point sync will occur after the publisher sync. Alternatively, you can leave that box unchecked and run a SUP sync manually. Upon completion of the publisher and SUP sync a new product called '**Patch My PC**' will become available in the software update point configuration tab. To reach this tab you will need to navigate to sites, right click the primary or CAS, select configure site components and choose Software Update Point.



![Configure Software Update Point Tab](/_images/image-(1793 "Configure Software Update Point Tab").png>)

<blockquote class="wp-block-quote">
<p>Note: If your SUP is remote, you will need to Configure the SMS Provider connection before running the publisher and SUP sync. This can be done under the Sync Schedule tab, by selecting “Configure SMS Provider connection..”.</p>
</blockquote>

Once this loads, select products and check the entire Patch My PC category.&#x20;

![Enable the patch my pc product category.](/_images/image-(1831 "Enable the patch my pc product category.").png>)

Once enabled, the next software update point sync will pull in all updates created by Patch My PC.
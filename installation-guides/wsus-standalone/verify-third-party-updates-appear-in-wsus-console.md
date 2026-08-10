---
description: >-
  Next, we want to verify that the third-party updates appear in the WSUS
  Console.
---

# Verify Third-Party Updates Appear in WSUS Console

_Applies to: On-premises Publisher_

Any updates published after the WSUS Standalone option was enabled should appear directly in the WSUS console.

![](<../../.gitbook/assets/image (1835).png>)

{% hint style="info" %}
**Note:** If updates were published **before this setting was enabled**, they would **not appear in the WSUS console automatically**.

For updates published before WSUS Standalone mode was enabled, use the [**Modify Published Updates Wizard**](https://patchmypc.com/modify-published-third-party-updates-wizard) to make those updates appear in the WSUS console.
{% endhint %}

### Adding an Update View for Patch My PC Updates

We can also create a new **Update View** for Patch My PC updates. This will help with finding and managing updates from Patch My PC within WSUS.&#x20;

We'll walk through that process in the steps below:

* In WSUS right-click **Updates** and select **New Update View...**
* Under Step 1, select **Updates are for a specific product**
* Under Step 2, select **any product**
* In the **Choose Products** window, check the **All Products** box at the top to disable all products. Scroll down to the bottom of the list, enable the boxes for **Patch My PC** and **SCUP Updates,** and select **OK**
* For Step 3, specify a name, for example: **Patch My PC Updates,** and select **OK**
* Select **Patch My PC Updates**
* If needed, change **Approval** to **Any Except Declined** and **Status** to **Any**
* Hit **Refresh** and now you will see all of the Patch My PC Updates in that list&#x20;

![Creating an Update view for Patch My PC Updates](<../../.gitbook/assets/wsus standalone 4.gif>)

You can now deploy the third-party updates just like a Microsoft update **directly from the WSUS console**.

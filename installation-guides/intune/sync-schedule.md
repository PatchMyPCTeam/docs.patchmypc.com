---
description: >-
  Getting started with a Sync Schedule for the patch my pc publisher and
  understanding product timing.
---

# Sync Schedule

_Applies to: On-premises Publisher_

## Scheduling Daily Publish

By default, we recommend the Publisher sync runs on a daily basis. The sync schedule only controls **when updates or applications are published** to your environment. Keep in mind this will also affect assignment scheduling if you use the manage assignments feature.

{% hint style="success" %}
**Tip**: Generally, Patch My PC releases an update to the catalog **three to five times a week**. These updates are released usually posted by **4:00 PM Eastern Time**.
{% endhint %}

When Patch My PC releases these new updates, the **sync schedule is what automates the publication process**.&#x20;

You can also manually start the sync and publication process at any time by selecting the **Run Publishing Service Sync** option.

![Publishing Daily Sync Options](<../../.gitbook/assets/image (1825).png>)

### Intune Application Manager

After the sync, you can view the published products with the [Intune Application Manager.](https://patchmypc.com/intune-application-manager-utility) This feature will provide you with a live view of all Win32 apps currently in your Intune tenant.&#x20;

It can help you:

* **Export a list of your Intune Win32 apps to .csv**, so you can use our [**Power BI template**](https://patchmypc.com/power-bi-reports-for-microsoft-intune-third-party-updates) to report on third party patching in Intune
* **Manage live assignments** for all of your existing Win32 apps in Intune
* **Multi-select and delete** Intune Win32 apps or their assignments

The utility can be found within the Publisher in either the **Intune Apps** or **Intune Updates** tab, on the right-hand side as a cloud icon with a magnifying glass:

![](<../../.gitbook/assets/image (1824).png>)

Below is an example screenshot of what the utility looks like in a tenant with some Win32 apps. This is a **live view of all Win32 apps** currently in your tenant.

![](<../../.gitbook/assets/image (1827).png>)

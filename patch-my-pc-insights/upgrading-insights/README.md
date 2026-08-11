---
description: Details of the upgrade process
---

# Upgrading Insights

_Applies to: Patch My PC Advanced and Patch Insights_

### Enhanced upgrade

Prior to version 2.5.1, upgrading Advanced Insights was an entirely manual process. But from version 2.5.1, you will see a notification whenever an update is available. You can then perform the upgrade on the server where Advanced Insights is installed. For more information on this process, [see here](insights-updater.md)

### Manual update

To manually upgrade Advanced Insights, we need to re-run the installer using the latest version downloaded from [here](../download-and-install-insights/).&#x20;

{% hint style="info" %}
To upgrade silently please run AdvancedInsights.exe /q /l\*v %temp%\AdvInsights.log
{% endhint %}

When you run the installer, it will prompt for you to accept the license terms.

<figure><img src="../../.gitbook/assets/image (4341).png" alt="License T&#x26;Cs" width="563"><figcaption></figcaption></figure>

You will be presented with the upgrade summary page. There is also the option to change the certificate, network port or IIS application pool identity if required.

<figure><img src="../../.gitbook/assets/image (4342).png" alt="Upgrade summary page" width="563"><figcaption></figcaption></figure>

If upgrading from 1.0.x and 2.0.x versions of Advanced Insights, the upgrade summary page will also include summary information about the Advanced Insights SQL DB migration to SQLite.

See section: [upgrading-to-advanced-insights-2.1-and-later-from-1.0.x-and-2.0.x-versions.md](upgrading-to-advanced-insights-2.1-and-later-from-1.0.x-and-2.0.x-versions.md "mention")

If you wish to do so, click the **'View / Change Cert'** button will show additional information about any warnings being flagged.

<figure><img src="../../.gitbook/assets/image (4343).png" alt="Certificate properties" width="563"><figcaption></figcaption></figure>

Following this, click **Install** to start the upgrade process.

The upgrade success page is displayed upon completion.

<figure><img src="../../.gitbook/assets/image (4344).png" alt="Upgrade successful" width="563"><figcaption></figcaption></figure>

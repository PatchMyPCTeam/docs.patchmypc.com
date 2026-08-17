---
description: >-
  Advanced Insights & Patch Insights include a feature to manually check for new
  product updates.
---

# Insights Updater

{% hint style="warning" %}
Advanced Insights upgrade notifications are introduced in version 2.5.1 and later.
{% endhint %}

{% hint style="warning" %}
As specified in the [insights-network-requirements.md](../advanced-and-patch-insights-requirements-and-prerequisites/insights-network-requirements.md "mention") documentation, the Advanced Insights update checker component uses the following URLs:

* Update metedata and installer
  * [https://updateadvancedinsights.patchmypc.com/](https://updateadvancedinsights.patchmypc.com/)
* Updater certificate revocation check
  * [http://e7.c.lencr.org/26.crl](http://e7.c.lencr.org/26.crl)
{% endhint %}

## Update check

1. When an administrator role user logs into the Advanced Insight portal web page, if an update is available, the following notification will be displayed:
   1.  Web portal notification:

       1. ![](<../../.gitbook/assets/image (3445).png>)
       2.

       ```
       <figure><img src="../../.gitbook/assets/image (3446).png" alt=""><figcaption></figcaption></figure>
       ```

       3. Within the 'Administration' node, the Notifications page displays the update information ![](<../../.gitbook/assets/image (3447).png>)
       4.

       ```
       <figure><img src="../../.gitbook/assets/image (3449).png" alt=""><figcaption></figcaption></figure>
       ```

       5. The administrative user then needs to access the Windows Server OS where Advanced Insights is installed.
2.  When logging into the Windows Server OS where Advanced Insights is installed, the update check is performed silently, and if an update is available, the following prompt will be automatically displayed shortly after logging on: 1.

    ```
    <figure><img src="../../.gitbook/assets/image (611).png" alt=""><figcaption></figcaption></figure>
    ```

    2\. When clicking ‘Next’, the new Advanced Insights install (.exe) is downloaded and the upgrade dialog is automatically started:

<figure><img src="../../.gitbook/assets/image (4342).png" alt="Advanced Insights Upgrade" width="563"><figcaption></figcaption></figure>

The reminder of the Advanced Insights upgrade is manual. Continue with the upgrade routine by following the onscreen dialog prompt.

## Manual update check

1.  When logged onto the Windows Server OS where Advanced Insights is installed, to check for Advanced Insights update manually, double click the ‘Advanced Insights Update Check’ shortcut to run the update check.

    <figure><img src="../../.gitbook/assets/image (3455).png" alt=""><figcaption></figcaption></figure>
2.  If an update is available for Advanced Insights, the following prompt is displayed:

    <figure><img src="../../.gitbook/assets/image (611).png" alt=""><figcaption></figcaption></figure>

    1. As described in the automated check section, after clicking ‘Next’ the remainder of the upgrade routine is manual.
    2.  If no update is available, the following prompt is displayed:

        <figure><img src="../../.gitbook/assets/image (3457).png" alt=""><figcaption></figcaption></figure>

## Updater components

The Advanced Insights update check components are stored under the program install directory e.g. _C:\Program Files (x86)\Advanced Insights\Api\Updater_

<figure><img src="../../.gitbook/assets/image (3458).png" alt=""><figcaption></figcaption></figure>

For the automated silent check during logon to the Advanced Insights Windows Server OS, the _'AdvInsightsUpdateCheck.exe_' is called using a registry run key. This key is created during the install of Advanced Insights.

<figure><img src="../../.gitbook/assets/image (3459).png" alt=""><figcaption></figcaption></figure>

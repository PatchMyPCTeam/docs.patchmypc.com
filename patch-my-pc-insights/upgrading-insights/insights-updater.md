---
description: >-
  Advanced Insights & Patch Insights include a feature to manually check for new
  product updates.
---

# Insights Updater

<blockquote class="wp-block-quote">
<p>Advanced Insights upgrade notifications are introduced in version 2.5.1 and later.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>As specified in the [insights-network-requirements.md](../advanced-and-patch-insights-requirements-and-prerequisites/insights-network-requirements.md "mention") documentation, the Advanced Insights update checker component uses the following URLs:</p>
<p>* Update metedata and installer</p>
<p>* <a href="https://updateadvancedinsights.patchmypc.com/">https://updateadvancedinsights.patchmypc.com/</a></p>
<p>* Updater certificate revocation check</p>
<p>* <a href="http://e7.c.lencr.org/26.crl">http://e7.c.lencr.org/26.crl</a></p>
</blockquote>

## Update check

1. When an administrator role user logs into the Advanced Insight portal web page, if an update is available, the following notification will be displayed:
   1. Web portal notification:&#x20;
      1. ![](/_images/image-(3445).png>)
      2.

          ![](/_images/image-(3446).png)


      3. Within the 'Administration' node, the Notifications page displays the update information ![](/_images/image-(3447).png>)
      4.

          ![](/_images/image-(3449).png)


      5. The administrative user then needs to access the Windows Server OS where Advanced Insights is installed.
2. When logging into the Windows Server OS where Advanced Insights is installed, the update check is performed silently, and if an update is available, the following prompt will be automatically displayed shortly after logging on:
   1.

       ![](/_images/image-(611).png)


   2. When clicking ‘Next’, the new Advanced Insights install (.exe) is downloaded and the upgrade dialog is automatically started:

![Advanced Insights Upgrade](/_images/image-(4346).png "Advanced Insights Upgrade")

The reminder of the Advanced Insights upgrade is manual. Continue with the upgrade routine by following the onscreen dialog prompt.

## Manual update check

1.  When logged onto the Windows Server OS where Advanced Insights is installed, to check for Advanced Insights update manually, double click the ‘Advanced Insights Update Check’ shortcut to run the update check.

    ![](/_images/image-(3455).png)


2.  If an update is available for Advanced Insights, the following prompt is displayed:

    ![](/_images/image-(613).png)



    1. As described in the automated check section, after clicking ‘Next’ the remainder of the upgrade routine is manual.
    2.  If no update is available, the following prompt is displayed:

        ![](/_images/image-(3457).png)

## Updater components

The Advanced Insights update check components are stored under the program install directory e.g. _C:\Program Files (x86)\Advanced Insights\Api\Updater_

![](/_images/image-(3458).png)

For the automated silent check during logon to the Advanced Insights Windows Server OS, the _'AdvInsightsUpdateCheck.exe_' is called using a registry run key. This key is created during the install of Advanced Insights.

![](/_images/image-(3459).png)
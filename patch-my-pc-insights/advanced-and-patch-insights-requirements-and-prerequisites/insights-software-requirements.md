---
description: Server OS, SQL and Dependencies
---

# Insights Software Requirements

_Applies to: Patch My PC Advanced and Patch Insights_

### Server Operating System Requirements <a href="#server-operating-system-requirements" id="server-operating-system-requirements"></a>

* Windows Server 2016 and later
* 1.5 GB of free disk space
* Minimum 1 CPU Core
* Minimum 8 GB RAM

{% hint style="info" %}
CPU and RAM requirements are a minimum for Advanced Insights only and do not consider any other IIS Web sites or Apps running on the same instance.
{% endhint %}

### Windows Server Components and Features <a href="#windows-server-components-and-features" id="windows-server-components-and-features"></a>

* Internet Information Services (IIS)
* WebSockets (will be added automatically by the installer if missing)

{% hint style="info" %}
To install IIS on your server outside of the installer you can run this PowerShell command:

Install-WindowsFeature -name Web-Server -IncludeManagementTools
{% endhint %}

{% hint style="danger" %}
For an existing IIS Server - 'OPTIONS' HTTP Verb **must not be BLOCKED at server level.**
{% endhint %}

The following is an example of 'OPTIONS' HTTP Verb **'Not allowed'** This configuration will prevent the Advanced Insights install from completing successfully.

<figure><img src="../../.gitbook/assets/vmconnect_OBXSaNs8bz.png" alt=""><figcaption><p>IIS Admin Console</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/vmconnect_4TA8FfVlNk.png" alt=""><figcaption><p>'OPTIONS' HTTP Verb eq. False</p></figcaption></figure>

{% hint style="info" %}
If 'OPTIONS' HTTP verb is present at the IIS Server level and **'Allowed'** value set to **'False',** remove this item and re-run the Advanced Insights installer.

The installer will configure 'OPTIONS' HTTP verb at the <mark style="color:yellow;">**site level**</mark> for 'Advanced Insights Api' IIS site object.
{% endhint %}

### Additional Software Components <a href="#additional-software-components-all-will-be-added-automatically-by-the-installer-if-missing" id="additional-software-components-all-will-be-added-automatically-by-the-installer-if-missing"></a>

* IIS CORS Module 1.0
* ASP.NET Core Hosting Bundle 8.0
* SQL Server ODBC Driver 17.6 (minimum)
* IIS URL Rewrite 2.1

{% hint style="info" %}
The Advanced Insights installer will automatically install additional software if needed.
{% endhint %}

### Configuration Manager SQL Server

* Configuration manager SQL Database must be SQL Server 2016 SP1 or later. We strongly recommend ensuring the latest cumulative update is applied to your SQL Server.
* Database Compatibility Mode must be at least 130 for the Threat Analytics dashboard to load. You will see a warning if this is not met.

{% hint style="info" %}
If you experience performance degradation in the ConfigMgr Console or Advanced Insights when running the default recommended Compatibility Mode level for your version of SQL Server, reassess whether you may have to change the level to **110**.\
\
Microsoft have further reading on this here [https://learn.microsoft.com/en-us/troubleshoot/mem/configmgr/alerts-reports-queries/sql-query-times-out-or-console-slow-performance](https://learn.microsoft.com/en-us/troubleshoot/mem/configmgr/alerts-reports-queries/sql-query-times-out-or-console-slow-performance)
{% endhint %}

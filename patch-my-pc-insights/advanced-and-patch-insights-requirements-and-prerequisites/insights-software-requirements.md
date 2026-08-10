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

> CPU and RAM requirements are a minimum for Advanced Insights only and do not consider any other IIS Web sites or Apps running on the same instance.

### Windows Server Components and Features <a href="#windows-server-components-and-features" id="windows-server-components-and-features"></a>

* Internet Information Services (IIS)
* WebSockets (will be added automatically by the installer if missing)

> To install IIS on your server outside of the installer you can run this PowerShell command:
>
> Install-WindowsFeature -name Web-Server -IncludeManagementTools

> For an existing IIS Server - 'OPTIONS' HTTP Verb \*\*must not be BLOCKED at server level.\*\*

The following is an example of 'OPTIONS' HTTP Verb **'Not allowed'** This configuration will prevent the Advanced Insights install from completing successfully.

![](<../../.gitbook/assets/vmconnect_OBXSaNs8bz (1).png>)

![](<../../.gitbook/assets/vmconnect_4TA8FfVlNk (1).png>)

> If 'OPTIONS' HTTP verb is present at the IIS Server level and \*\*'Allowed'\*\* value set to \*\*'False',\*\* remove this item and re-run the Advanced Insights installer.
>
> The installer will configure 'OPTIONS' HTTP verb at the <mark style="color:yellow;">\*\*site level\*\*</mark> for 'Advanced Insights Api' IIS site object.

### Additional Software Components <a href="#additional-software-components-all-will-be-added-automatically-by-the-installer-if-missing" id="additional-software-components-all-will-be-added-automatically-by-the-installer-if-missing"></a>

* IIS CORS Module 1.0
* ASP.NET Core Hosting Bundle 8.0
* SQL Server ODBC Driver 17.6 (minimum)
* IIS URL Rewrite 2.1

> The Advanced Insights installer will automatically install additional software if needed.

### Configuration Manager SQL Server

* Configuration manager SQL Database must be SQL Server 2016 SP1 or later. We strongly recommend ensuring the latest cumulative update is applied to your SQL Server.
* Database Compatibility Mode must be at least 130 for the Threat Analytics dashboard to load. You will see a warning if this is not met.

> If you experience performance degradation in the ConfigMgr Console or Advanced Insights when running the default recommended Compatibility Mode level for your version of SQL Server, reassess whether you may have to change the level to \*\*110\*\*.\\
>
> \\
>
> Microsoft have further reading on this here [https://learn.microsoft.com/en-us/troubleshoot/mem/configmgr/alerts-reports-queries/sql-query-times-out-or-console-slow-performance](https://learn.microsoft.com/en-us/troubleshoot/mem/configmgr/alerts-reports-queries/sql-query-times-out-or-console-slow-performance)

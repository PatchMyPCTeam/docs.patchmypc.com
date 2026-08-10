# Advanced Insights Log Collector

_Applies to: Patch My PC Advanced Insights_

Sometimes we need you to provide log files, including information about your Advanced Insights instance. We have two ways for you to collect logs, either that the Advanced Insights Application or by manually running the logs collector on the server.&#x20;

### Via Advanced Insights

<blockquote class="wp-block-quote">
<p>This functionality was introduced in version 2.6.3. If you do not see it, please upgrade to a later version of the application.&#x20;</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>If you run Advanced Insights with a different user other than the default Local System, you may encounter issues with generating logs based on the privileges the account has.&#x20;</p>
</blockquote>

To collect logs via Advanced Insights, as the Admin or a user with Admin privileges, navigate to Administration -> Settings.&#x20;

You will see on the first tab, at the bottom there is a button to "Export Debug File". Click the button, there will a wait whilst logs are collected. Once the logs are collected, a download will be initiated with a zip containing all the logs required. If for any reason this fails or you receive no download, please try the server approach outlined below.&#x20;

![](/_images/image-(4526).png)

### Via Server hosting Advanced Insights

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The Advanced Insights Log Collector is located at:</p>
<p>_`%Advanced Insights Install Directory%`_`\Api\LogCollector\AdvancedInsightsLogDiag.exe`</p>
<p>For example:</p>
<p>`C:\Program Files (x86)\Advanced Insights\Api\LogCollector\AdvancedInsightsLogDiag.exe` <br></p>
<p>You can also specify the output directory as well, using the -o parameter</p>
<p>For example:</p>
<p>`C:\Program Files (x86)\Advanced Insights\Api\LogCollector\AdvancedInsightsLogDiag.exe -o "C:\Temp"`&#x20;</p>
</blockquote>



<blockquote class="wp-block-quote">
<p>The Log Collector can be executed manually and is also used within the Advanced Insights installer. Once the log collection process is completed, a zip file is created on the desktop (or location specified with the -o parameter) called:</p>
<p>**AdvancedInsights\_Diag\_xxxxxxxx\_xxxxxx.zip**</p>
<p>This ZIP should be shared with Patch My PC technical support.</p>
<p>_Example output:_</p>
</blockquote>

![](/_images/image-(2628).png "Advanced Insights log collection output.")

**This page provides details about what information the AdvancedInsightsLogDiag.exe collects.**

### Advanced Insights data and installation logs

The contents of the following directory are collected, which consist of the 'AdvancedInsightsApi.log' and any 'AdvInsights\_Verx.x.x.zip' installer logs.

C:\ProgramData\AdvancedInsights\Logs

![](/_images/image-(2626).png "Advanced Insights default logging directory")

### Windows Application Event Log

The Windows Application Event log data is collected and output into 'Application\_EventLog.log' with a filter applied for the following event sources:

* ".NET Runtime"&#x20;
* "Advanced Insights"
* "MsiInstaller" - if required to diagnose install problems, the filter will include&#x20;

### Advanced Insights SQLite db

The 'ConfigManagerLocation' and 'ConfigManagerDatabase' value are collected from the Advanced Insights SQLite database file located at:

**'C:\ProgramData\AdvancedInsights\Data\Api\AdvancedInsightsConfig.db'**

### SQL Server information

The following information is queried from the SQL Server instance where the Configuration Manager database is located:\
\
**SQL Master db:**

* Configuration Manager database name
* &#x20;Configuration Manager databaste state (ONLINE/OFFLINE)
* Configuration Manager database compatibility level
* Configuration Manager database .mdf file path
* Configuration Manager database file size
* Configuration Manager database log file .ldf path
* Configuration Manager database log file size
* SQL Server version
* SQL Server Product Level
* SQL Server Edition
* SQL Server Engine Edition
* SQL Server Product build
* SQL Server Product Major version
* SQL Server Product minor version
* SQL Server Product update version
* SQL Server Installed updates
* SQL Server remote query timeout value
* SQL Server maximum degree of parallelism value
* SQL Server Minimum size of server memory (MB)
* SQL Server Maximum size of server memory (MB)

**Configuration Manager SQL database:**

* Advanced Insights Inventory Extensions class names and data counts.
* Advanced Insights Inventory Extensions Configuration Manager application information. For    example 'Name', 'created date', 'version', 'number of deployments'.
* Configuration Manager database level SQL configured properties:
  * MAXDOP
  * LEGACY\_CARDINALITY\_ESTIMATION
  * PARAMETER\_SNIFFING
  * QUERY\_OPTIMIZER\_HOTFIXES
* TempDB database configuration and file setup

**Performance**

* Execution Statistics for PMPC queries - stored in the file CM\_SQL\_query\_output.json

### Windows Server IIS information

* Information related to the Advanced Insights IIS websites and application pools are collected.
* Advanced Insights Api
* Advanced Insights Frontend
* Website name
* HTTPS bindings included the current SSL certificate properties

### Windows Server information

* The version of Advanced Insight currently installed.
* The install date of Advanced Insights.
* The install path of Advanced Insights.
* The install source of Advanced Insights.
* Server CPU properties.
* Installed Server RAM
* Server disks including total size and free space
* Windows OS version
* Check for Server pending restart.
* List Windows updates installed in the last 30 days.
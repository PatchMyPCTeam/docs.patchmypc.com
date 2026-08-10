# Log Reference Guide for Patch My PC Products

_Applies to: All Patch My PC Products_

Sometimes we need you to provide log files for troubleshooting. This guide will help you locate the log files for Patch My PC (PMPC) products and usage scenarios.

* [Product Specific Logs](log-reference-guide.md#product-specific-logs)
* [Scenario Specific Logs](log-reference-guide.md#scenario-specific-logs)

> \*\*Note\*\*
>
> See \[Enable Debug Logging for Publisher]\(log-reference-guide.md#enable-debug-logging-for-publisher) for details on how to enable debug logging for Publisher, which can help troubleshoot Publisher-related issues.

### Product Specific Logs

This section includes details on the logs for Patch My PC (PMPC) products, which can help you troubleshoot issues and are typically requested by our support team.

* [Client](log-reference-guide.md#client)
* [Insights for ConfigMgr](log-reference-guide.md#insights-for-configmgr)
* [Publisher](log-reference-guide.md#publisher)

#### Client

**PatchMyPC\_Client\_Installer\_msi.log** is the primary log to use when troubleshooting installation of the PMPC Client and can be found at:

`C:\Windows\Temp\PatchMyPC_Client_Installer_msi.log`

**Client.log**

**Client.log** logs routine client operations and can be found at:

`C:\ProgramData\PatchMyPC\Logs\Client.log`

#### Insights for ConfigMgr

The Insights installer will automatically create an installation log at:

`%temp%\AdvInsights.log`

Additionally, a copy (.zip) of the install log is placed into the following folder:

`C:\ProgramData\AdvancedInsights\Logs\Installer`

Advanced Insights Inventory Extension client logs cn be found at:

`%ProgramData%\PatchMyPC\Logs\InventoryExtensions.log`

> This log was previously saved to `%WinDir%\CCM\Logs\PMPCInventory.log`

#### Publisher

**PatchMyPC.log** is the primary log file for the Publisher and is often required for troubleshooting by support. The file name and location are:

```
%PatchMyPCInstallDirectory%\PatchMyPC.log
%PatchMyPCInstallDirectory%\PatchMyPC.lo_
```

**Settings.xml**

**Settings.xml** stores all Publisher settings and is also used for [Backup and Restore](https://patchmypc.com/backup-and-restore-publisher-settings). The file name and location are:

```
%PatchMyPCInstallDirectory%\Settings.xml
```

### Scenario Specific Logs

Use this section to help you identify the logs our support team may request for each of the following scenarios:

* [Applications - Fails to Create/Update Intune Applications Using Publisher](log-reference-guide.md#applications-fails-to-create-update-intune-applications-using-publisher)
* [Applications - Failing to Create/Update SCCM Applications Using Publisher](log-reference-guide.md#applications-failing-to-create-update-sccm-applications-using-publisher)
* [Download Stuck at 0% / Waiting to install / Preparing to download](log-reference-guide.md#download-stuck-at-0-waiting-to-install-preparing-to-download)
* [Intune Apps/Updates Failing to Install on Client Devices](log-reference-guide.md#intune-apps-updates-failing-to-install-on-client-devices)
* [SCCM Applications Failing to Install on Client Devices](log-reference-guide.md#sccm-applications-failing-to-install-on-client-devices)
* [SCCM Automatic Deployment Rule Failing for Third-Party Updates](log-reference-guide.md#sccm-automatic-deployment-rule-failing-for-third-party-updates)
* [Software Updates - Failing to Publish Updates Using SCCM In-Console Publishing](log-reference-guide.md#software-updates-failing-to-publish-updates-using-sccm-in-console-publishing)
* [Software Updates - Failing to Publish Updates to WSUS Using Publisher](log-reference-guide.md#software-updates-failing-to-publish-updates-to-wsus-using-publisher)
* [Third-Party Software Updates Failing to Install on Client Devices](log-reference-guide.md#third-party-software-updates-failing-to-install-on-client-devices)
* [Updates Failing to Download to a Deployment Package using SCCM Console](log-reference-guide.md#updates-failing-to-download-to-a-deployment-package-using-sccm-console)

#### **Applications - Fails to Create/Update Intune Applications Using Publisher**

To troubleshoot issues with using PMPC Publisher to create apps in Intune, we need the following logs:

```
%PatchMyPCInstallDirectory%\PatchMyPC.log
%PatchMyPCInstallDirectory%\PatchMyPC.lo_
%PatchMyPCInstallDirectory%\Settings.xml
%PatchMyPCInstallDirectory%\PatchMyPC-DownloadHistory.csv
%PatchMyPCInstallDirectory%\PatchMyPC-PublishingHistory.csv
```

#### **Applications - Failing to Create/Update SCCM Applications Using Publisher**

To troubleshoot issues with using PMPC Publisher to create applications in SCCM, we need the following logs:

```
%PatchMyPCInstallDirectory%\PatchMyPC.log
%PatchMyPCInstallDirectory%\PatchMyPC.lo_
%PatchMyPCInstallDirectory%\Settings.xml
%PatchMyPCInstallDirectory%\PatchMyPC-DownloadHistory.csv
%PatchMyPCInstallDirectory%\PatchMyPC-PublishingHistory.csv
%SCCMInstallFolder%\Logs\SMSProv*.log
```

#### **Download Stuck at 0% / Waiting to install / Preparing to download**

To troubleshoot update installation errors on a client, we need the following client logs:

```
%WinDir%\CCM\Logs\CAS*.log
%WinDir%\CCM\Logs\CIAgent.*log
%WinDir%\CCM\Logs\ClientLocation*.log
%WinDir%\CCM\Logs\CMBITSManager*.log
%WinDir%\CCM\Logs\ContentTransferManager*.log
%WinDir%\CCM\Logs\DataTransferService*.log
%WinDir%\CCM\Logs\LocationServices.log*.log
%WinDir%\CCM\Logs\StateMessage.log
%WinDir%\CCM\Logs\UpdatesDeployment*.log
%WinDir%\CCM\Logs\UpdatesHandler*.log
%WinDir%\CCM\Logs\UpdatesStore*.log
%WinDir%\CCM\Logs\PatchMyPC-ScriptRunner.log (If exist)
```

#### **Intune Apps/Updates Failing to Install on Client Devices**

To troubleshoot issues with Intune apps installing on a client, we need the following client logs:

```
%ProgramData%\PatchMyPCIntuneLogs\PatchMyPC-ScriptRunner.log
%ProgramData%\PatchMyPCIntuneLogs\PatchMyPC-SoftwareDetectionScript.log
%ProgramData%\PatchMyPCIntuneLogs\PatchMyPC-SoftwareUpdateDetectionScript.log
```

> \*\*Important\*\*
>
> For user-based apps, the logs mentioned above will reside in the following locations:
>
> \* \*\*%LocalAppData%\PatchMyPCIntuneLogs\PatchMyPC-Scriptrunner.log\*\*
>
> \* \*\*%Temp%\PatchMyPC-SoftwareDetectionScript.log\*\*
>
> \* \*\*%Temp%\PatchMyPC-SoftwareUpdateDetectionScript.log\*\*

> \*\*Note\*\*
>
> These logs were previously stored under \*\*ProgramData\*\*, but the locations were changed due to a permission issue on shared devices. Log files created under \*\*ProgramData\*\* could only be written to by the original owner, which caused \*\*Access Denied\*\* log errors when other users installed user-based apps on the same device.

```
%ProgramData%\Microsoft\IntuneManagementExtension\Logs\AgentExecutor.log
%ProgramData%\Microsoft\IntuneManagementExtension\Logs\IntuneManagementExtension.log
%ProgramData%\Microsoft\IntuneManagementExtension\Logs\Win32AppInventory.log
%ProgramData%\Microsoft\IntuneManagementExtension\Logs\AppWorkload.log
```

> \*\*Note\*\*
>
> Some Patch My PC log files listed above may be found in \*\*%WinDir%\CCM\*\* folder if that folder exists.

#### **SCCM Applications Failing to Install on Client Devices**

To troubleshoot SCCM application installation errors on a client, we need the following client logs:

```
%WinDir%\CCM\Logs\AppDiscovery*.log
%WinDir%\CCM\Logs\AppEnforce*.log
%WinDir%\CCM\Logs\AppIntentEval*.log
%WinDir%\CCM\Logs\CAS*.log
%WinDir%\CCM\Logs\CIAgent.*log
%WinDir%\CCM\Logs\DataTransferService*.log
%WinDir%\CCM\Logs\PatchMyPC-ScriptRunner.log
%WinDir%\CCM\Logs\PatchMyPC-SoftwareDetectionScript.log
%WinDir%\CCM\Logs\StateMessage.log
```

#### **SCCM Automatic Deployment Rule Failing for Third-Party Updates**

To troubleshoot automatic deployment rules failing for third-party updates, we need the following server logs:

```
C:\Program Files\Microsoft Configuration Manager
PatchDownloader.log*

```

> \*\*Important\*\*
>
> In the example above, we have assumed the main SCCM installation directory is:\\
>
> \*\*C:\Program Files\Microsoft Configuration Manager\*\*
>
> Also, the location of the \*\*PatchDownloader.log\*\* can vary, as detailed in the [Log files by functionality](https://learn.microsoft.com/en-us/intune/configmgr/core/plan-design/hierarchy/log-files#BKMK_FunctionLogs) section of the [Log file reference](https://learn.microsoft.com/en-us/intune/configmgr/core/plan-design/hierarchy/log-files) article. For example, it could be in one of the following locations:
>
> \* \*\*C:\Program Files\SMS\\\_CCM\Logs\PatchDownloader\\\*.log\*\* (most common location)
>
> \* \*\*C:\Program Files\Microsoft Configuration Manager\Logs\PatchDownloader\\\*.log\*\*
>
> \* \*\*%WinDir%\CCM\Logs\*\*

> \*\*Tip\*\*
>
> If you are unable to locate the \*\*PatchDownloader.log\*\* check the following Registry key on the Site Server, which will tell you where it is:
>
> \`HKLM\SOFTWARE\Microsoft\CCM\Logging\\@Global:LogDirectory\`

#### **Software Updates - Failing to Publish Updates Using SCCM In-Console Publishing**

To troubleshoot SCCM in-console publishing, we need the following log files from the SUP/WSUS server where the service is installed:

```
%SiteSystemLogsFolder%\SMS_ISVUPDATES_SYNCAGENT*.log
%SiteServerLogsFolder%\wsyncmgr*.log
%SiteServerLogsFolder%\WCM*.log
```

> \*\*Note\*\*
>
> We may require the following log, which should only be sent to us if requested due to its large size:
>
> \`\`\`
>
> %ProgramFiles%\Update Services\LogFiles\SoftwareDistribution.log
>
> \`\`\`

#### **Software Updates - Failing to Publish Updates to WSUS Using Publisher**

To troubleshoot publish third-party updates to WSUS PMPC Publisher, we need the following log files from the SUP/WSUS server where the service is installed:

```
%PatchMyPCInstallDirectory%\PatchMyPC.log
%PatchMyPCInstallDirectory%\PatchMyPC.lo_
%PatchMyPCInstallDirectory%\Settings.xml
%PatchMyPCInstallDirectory%\PatchMyPC-DownloadHistory.csv
%PatchMyPCInstallDirectory%\PatchMyPC-PublishingHistory.csv
%SiteServerLogsFolder%\wsyncmgr*.log
%SiteServerLogsFolder%\WCM*.log
```

> \*\*Note\*\*
>
> We may require the following log, which should only be sent to us if requested due to its large size:
>
> \`\`\`
>
> %ProgramFiles%\Update Services\LogFiles\SoftwareDistribution.log
>
> \`\`\`

#### **Third-Party Software Updates Failing to Install on Client Devices**

To troubleshoot update installation errors on a client, we need the following client logs:

```
%WinDir%\CCM\Logs\CAS*.log
%WinDir%\CCM\Logs\DeltaDownload*.log
%WinDir%\CCM\Logs\ScanAgent*.log
%WinDir%\CCM\Logs\StateMessage.log
%WinDir%\CCM\Logs\UpdatesDeployment*.log
%WinDir%\CCM\Logs\UpdatesHandler*.log
%WinDir%\CCM\Logs\UpdatesStore*.log
%WinDir%\CCM\Logs\DataTransferService*.log
%WinDir%\CCM\Logs\WUAHandler*.log
%WinDir%\CCM\Logs\PatchMyPC-ScriptRunner.log (If exist)
%WinDir%\WindowsUpdate.log
```

> \*\*Note\*\*
>
> On Windows 8.1 and later you need to run [\*\*Get-WindowsUpdateLog\*\*](https://docs.microsoft.com/en-us/powershell/module/windowsupdate/get-windowsupdatelog?view=win10-ps) in PowerShell.

#### **Updates Failing to Download to a Deployment Package using SCCM Console**

To troubleshoot updates failing to download into a deployment package from the SCCM console, we need the following log from the machine running the SCCM console:

```
%temp%\PatchDownloader*.log
```

> \*\*Note\*\*
>
> If you are using an RDP session, the \*\*patchdownloader.log\*\* may be in a numbered sub-folder in your \*\*Users\*\* \*\*%temp%\*\* folder.

### **Enable Debug Logging for Publisher**

Enabling Debug logging in Publisher is often helpful for troubleshooting publishing-related issues.

To enable Debug logging:

1. Open Publisher.
2. On the **General** tab, under the **Logging Options** section, select **Debug**

![Selecting 'Debug' under the 'Logging Options' section](/_images/image-(3831).png)

3. Click **Save and Close** to close the Publisher.
4. Open **Services.msc**
5. Locate the **PatchMyPCService** service, then click **Restart** to restart the service.

![Locating the 'PatchMyPCService' service and restarting it](/_images/image-(3832).png)

Debug Logging for Publisher is now enabled.

Once you have completed troubleshooting, you should disable Debug logging by repeating this process, but selecting **Information** from the **Logging Level** dropdown in Publisher.
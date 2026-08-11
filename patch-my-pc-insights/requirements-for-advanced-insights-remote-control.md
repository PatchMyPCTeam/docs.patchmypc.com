---
description: >-
  Technical requirements to enable Remote Control from the Advanced Insights
  Device Details pane. (this is not relevant for Patch Insights).
---

# Requirements for Advanced Insights Remote Control

_Applies to: Patch My PC Advanced Insights_

> Quick start for Remote Control:
>
> 1\. Create a folder on your machine C:\AdvInsRemoteControl
>
> 2\. Copy C:\Program Files (x86)\Advanced Insights\Api\Installers\AdvInsRemoteControl.exe file from your Advanced Insights installation into this folder (needs to be unzipped)
>
> 3\. Copy CmRcViewer.exe RdpCoreSccm.dll and the relevant locale folder into the C:\AdvInsRemote Control folder too.
>
> 4\. Run AdvInsRemoteControl.exe from Windows Explorer to register it
>
> 5\. You can now invoke remote control from the Advanced Insights portal

To launch the Configuration Manager remote control action from the client actions menu in Advanced Insights the user must have some files from the Configuration Manager console install directory and an Advanced Insights utility. If the ConfigMgr console is installed on the user’s computer then no additional configuration is required.

### Files and Folders

To run the ConfigMgr remote control agent we need a copy of:

* CmRcViewer.exe
* RdpCoreSccm.dll
* the relevant locale folder for the RC Tools, for example 00000409

All of these are copied from \\\SiteServerName\SMS\__ABC_\AdminConsole\bin\i386

On each Advanced Insight user’s computer, copy these files and folder to a location accessible by the user, for example C:\CMTools or %AppData%\CMRCtools.

We also need a copy of the Advanced Insights utility AdvInsRemoteControl.exe stored in the same location. The user is prompted to download and run this from the Advanced Insights portal the first time they try to use remote control if the app has not already been executed.

![](../.gitbook/assets/image-\(1785\).png)

### The AdvInsRemoteControl.exe file

AdvInsRemoteControl.exe is included with the installation of Advanced Insights in the folder C:\Program Files (x86)\Advanced Insights\Api\Installers. It is a DotNet Core application which handles calling the Configuration Manager Remote Control utility from the Advanced Insights website. On first run AdvInsRemoteControl.exe registers itself in the Registry as a class type under `Computer\HKEY_CURRENT_USER\Software\Classes\cmrc`

This allows the Advanced Insights website to invoke the ConfigMgr Remote Control agent when required. If you delete or move the AdvInsRemoteControl.exe you can reregister it simply by running it again from Windows Explorer.

The application will check for the correct Configuration Manger files and folders when it runs and will alert you to any configuration errors.

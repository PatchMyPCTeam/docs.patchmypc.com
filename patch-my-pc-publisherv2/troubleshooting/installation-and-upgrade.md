# Installation and Upgrade

_Applies to: Patch My PC Publisher V2.x_

## Overview

This section provides guidance for troubleshooting issues that may occur during installation or upgrade of the Publisher. It covers common scenarios related to missing prerequisites, unavailable installation sources, and environment configuration problems.

The topics in this section focus on identifying and resolving issues such as missing MSI files, Windows Installer errors, and missing components including the WSUS API and Configuration Manager SDK. These troubleshooting steps help ensure a successful installation or upgrade of the Publisher.

## The Publisher Fails to Upgrade

At the end of a [sync](../administration/sync-schedule.md), if a new version of the Publisher is available, the Publisher attempts to install the update by default. When this occurs, the following entry appears in the PatchMyPC.log file at the end of the sync.

```
Starting self-update, the command line is: MsiExec.exe /i C:\WINDOWS\TEMP\PatchMyPC-Publishing-Service.msi /qn /log C:\WINDOWS\TEMP\PatchMyPC-Publishing-Service_Upgrade.log
```

![](../../.gitbook/assets/image-\(4232\).png)

> \*\*Note\*\*
>
> If you see errors such as "\_An error occurred with the SignalR connection\_" logged around the time illustrated above, this is normal while some services stop and start again during the update process.

If a failure occurs during the self update process and [Alerts](../administration/alerts/) are configured, a notification is generated. The notification will appear similar to the screenshots shown below

![](../../.gitbook/assets/image-\(4233\).png)

![](../../.gitbook/assets/image-\(4234\).png)

To understand the root cause of the upgrade failure, it is recommended to inspect the log file indicated in PatchMyPC.log produced by the .msi installer:

* **C:\WINDOWS\TEMP\PatchMyPC-Publishing-Service\_Upgrade.log**

See [Error 1714](installation-and-upgrade.md#error-1714.-the-older-version-of-patch-my-pc-publishing-service-cannot-be-removed.-contact-your-tech) for more detail on the common causes for upgrade failures.

### Error 1714/1612 - The older version of Patch My PC Publishing Service cannot be removed

When searching up for the value `return value 3` from the bottom of the **PatchMyPC-Publishing-Service\_Upgrade.log** log file, you might see log lines similar to the following:

```
Action start 05:37:07: RemoveExistingProducts.
CustomAction  returned actual error code 1612 (note this may not be 100% accurate if translation happened inside sandbox)
[05:37:07:238]: /_images/Product-Patch-My-PC-Publishing-Service-Error-1714-The-older-version-of-Patch-My-PC-Publishing-Service-cannot-be-removed-Contact-your-technical-support-group-System-Error-1612
Error 1714. The older version of Patch My PC Publishing Service cannot be removed.  Contact your technical support group.  System Error 1612.
```

When you attempt to manually install the update by downloading and running the [latest .msi](https://patchmypc.com/msi), you receive a dialogue similar to the below:

![](../../.gitbook/assets/image-\(4235\).png)

The 1612 error code is usually thrown when the original installation media for the currently installed application is no longer available on the system - something has deleted it. Typically, .msi software caches itself to **C:\Windows\installer** and the original .msi file is critical for any application update, repair, or uninstall.

The Windows Installer service first looks the .msi of the currently installed version in **C:\Windows\installer** and also its last known install location - the self-updater is downloaded and launched from **C:\Windows\temp**.

> \*\*Tip\*\*
>
> You can read more about system error code 1612 in the following knowledge base article: [System Error 1612 – The installation source for this product is not available.](https://patchmypc.com/kb/system-error-1612-installation-source/)

If you encounter this issue, you can resolve it by recaching the missing .msi file:

1. Download the .msi file for the current version you have installed
2. Recache the .msi file using the below command:

```
msiexec /fvomus "C:\path\to\PatchMyPC-Publishing-Service.msi" /qn
```

3. Attempt the update again and it should now be successful

We do not currently publicly host the installers for older versions of the Publisher, so it is advised to open a [technical support case](https://patchmypc.com/technical-support/) requesting a copy for the version you need.

After resolving the issue, it is strongly recommend you investigate any clean up scripts or other automations which may be deleting files from **C:\Windows\installer** to prevent the issue from happening again.

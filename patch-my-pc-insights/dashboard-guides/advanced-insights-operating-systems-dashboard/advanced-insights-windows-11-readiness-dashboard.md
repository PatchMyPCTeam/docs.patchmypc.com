---
description: Windows 11 Upgrade Readiness for Windows 10 Client Devices
---

# Advanced Insights "Windows 11 Readiness" Dashboard

_Applies to: Patch My PC Advanced Insights_

![](/_images/image-(4751).png)

On the top bar of this page we are showing:

* Windows 11 - Count of all Windows 10 and 11 client devices that are inventoried as Windows 11
* Unappraised - Count of all Windows 10 client devices missing Windows 11 upgrade appraisal data
* Ready for Upgrade - Count for all managed Windows 10 client devices that can be immediately upgraded to Windows 11
* Cannot Upgrade - Count of all managed Windows 10 client devices that cannot be upgraded to Windows 11

The donut chart for OS Upgrade Readiness and Cannot Upgrade Reason you have a properties which you can toggle between the different versions of Windows 11. On these two donut charts you also have the ability to view the chart data and export from the cog icon.

![](/_images/image-(4752).png)

![](/_images/image-(4753).png)

The last chart on the left is the Windows 11 Upgrade Readiness Issues chart where you can see the reasons for why the devices are unable to upgrade to Windows 11.

![](/_images/image-(2854).png)

The Reasons column have the following conditions which are flagged if a device is marked as unable to upgrade (Red) to Windows 11:

* If a system doesn't support TPM 2.0 (RedReason=Tpm)
* If the system isn't Secure Boot Capable (RedReason=UefiSecureBoot)
* If the system has less than 4 GB of RAM (RedReason=Memory)
* If the system doesn't have 2 processor cores (RedReason=CPU)
* If the CPU doesn't support 1 ghz and higher speed (RedReason=CPU)
* If the CPU doesn't support the Windows 11 approved CPU generation (RedReason=CpuFms)
* If the system is in SMode and not a home (core) sku (RedReason=SModeState)
* If the system drive size is < 64 Gb (RedReason=SystemDriveSize)

> This information is listed on [https://learn.microsoft.com/en-us/mem/configmgr/osd/deploy-use/manage-windows-11-readiness-dashboard](https://learn.microsoft.com/en-us/mem/configmgr/osd/deploy-use/manage-windows-11-readiness-dashboard)
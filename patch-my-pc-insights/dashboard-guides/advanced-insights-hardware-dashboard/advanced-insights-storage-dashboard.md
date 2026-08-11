---
description: Storage device data collected by Advanced Insights in your environment
---

# Advanced Insights "Storage" Dashboard

_Applies to: Patch My PC Advanced Insights_

{% hint style="info" %}
This dashboard requires deployment of the [Advanced Insights Inventory Extensions](../../advanced-insights-inventory-extensions/)
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (2233).png" alt=""><figcaption><p>Storage dashboard</p></figcaption></figure>

This dashboard hosts two primary tables.&#x20;

### Disks and Logical Partitions

The top table lists physical disk, the partitions defined on that disk and the logical drives created on that partition. For example:

<figure><img src="../../../.gitbook/assets/image (2236).png" alt=""><figcaption></figcaption></figure>

Here, a a machine has five physical disks, Disk #0 has three partitions, but only one of these partitions has a logical drive with a drive letter (C:) defined (the "missing" partitions in this instance are the Windows Recovery Partition and the EFI System Partition). That partition is allocated 232.3GB of a 232.9GB disk (\~100% of the drive) and the logical disk is 232.3GB in size with 168.2GB free space, i.e. it is 27.6% used.

### Physical Storage Device Health

The storage health statistics are gathered from Windows S.M.A.R.T. (Self-Monitoring, Analysis and Reporting Technology) tools.&#x20;

<figure><img src="../../../.gitbook/assets/image (2237).png" alt=""><figcaption><p>Device Health table</p></figcaption></figure>

Each disk presents the data it supports (not all disks report PowerOn statistics, or temperature,  these are listed where available). We can see the wear statistic reported by SMART. The higher the wear percentage, the more likely it is that the disk will fail.

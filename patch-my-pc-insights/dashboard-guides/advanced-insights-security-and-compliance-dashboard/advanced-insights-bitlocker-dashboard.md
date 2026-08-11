---
description: >-
  BitLocker Drive Encryption data when integrated and managed by Endpoint
  Configuration Manager
---

# Advanced Insights "BitLocker" Dashboard

_Applies to: Patch My PC Advanced Insights_

> The BitLocker dashboard requires the following hardware inventory classes to be enabled:
>
> \* BitLocker (Win32\\\_EncryptableVolume)
>
> \* BitLocker Encryption Details (Win32\\\_BitLockerEncryptionDetails)
>
> \* BitLocker Policy (Win32Reg\\\_MBAMPolicy)
>
> \* TPM (Win32\\\_TPM)

For full functionality of this dashboard, MBAM should be integrated with ConfigMgr as outlined in this document:[https://learn.microsoft.com/en-us/mem/configmgr/protect/deploy-use/bitlocker/deploy-management-agent](https://learn.microsoft.com/en-us/mem/configmgr/protect/deploy-use/bitlocker/deploy-management-agent)

This will ensure the BitLocker Unmanaged and Recovery at Risk statistics are populated.

The top row of statistics help to identify where configuration errors may be causing compliance issues.

![](/_images/image-(2692).png)

The first statistic, "BitLocker Unmanaged" shows Computers which have a BitLocker Encrypted Operating System Drive but are not under the control of a Configuration Manager or integrated MBAM Agent Management Policy. These devices may not conform to the required standard and will not report compliance.

Recovery at risk lists computers which have a BitLocker Encrypted Operating System Drive but have not yet escrowed a recovery key into the Configuration Manager database. You may be unable to access these devices in the event of a BitLocker Recovery prompt.

Inactive TPM portable devices lists laptops machines which do not show an activated TPM chip.

Non-Compliant Computers shows BitLocker Encrypted computers which do not conform to the BitLocker policies set in your environment. Clicking through will show the compliance conflicts:

![](/_images/image-(2693).png)

The row of donut charts show the BitLocker status for all workstation clients (off, on, suspended or unknown). We show the BitLocker Cipher in use by the clients (this requires the MBAM integration listed above). We show the TPM version of the clients and the TPM Status (Activated, Enabled, Unknown). TPM "Enabled" is ready for activation by the OS, but is not currently in use.
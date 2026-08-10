# Example Email Alerts sent by Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

If [email notifications](../manage/alerts-tab/email-alerts-tab/email-notification-configuration/) have configured for Patch My PC (PMPC) Publisher, the email sent at the end of the sync will include the following details for all Published products:

* Update/Application **Title** (Links to release notes)
* **Time** of Publishing
* **Size** of binary
* Update **Classification**
* Update **Severity Level**
* **CVE’s** (Links to CVE-ID on [https://cve.mitre.org/](https://cve.mitre.org/))

In the example below, you can see an email alert where both **WSUS updates** and **ConfigMgr applications** were published successfully.

![Email notification for WSUS updates and ConfigMgr applications](/_images/image-(3878).png)

For products published to **Intune**, the email includes the following additional information

* Intune Tenant friendly name
* Intune assignments set during Publishing.

![Email notification for Intune applications](/_images/image-(3879).png)
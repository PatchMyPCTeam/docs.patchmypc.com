---
description: This guide will walk through enabling Standalone WSUS Mode in the Publisher.
---

# Enable Standalone WSUS Mode

_Applies to: On-premises Publisher_

To enable standalone WSUS mode, go to the **Updates** tab and select **Options**. In the **WSUS options** window check the box **Make updates appear in the WSUS console. This option isn’t needed if using Configuration Manager.**

![](/_images/image-(1944).png>)

If your WSUS database is using a **Windows Internal Database** (WID), the **database connection options will be read-only**.

When using a **SQL Server for the WSUS database**, you will need to choose either to connect to the database using the **SYSTEM account** or define a user name and password using **SQL authentication**.

![](/_images/image-(1920).png>)

For more information on the minimum permissions required, please visit [our KB article](https://patchmypc.com/configuring-standalone-wsus-mode).
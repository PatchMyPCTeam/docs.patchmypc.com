---
description: Change the Advanced Insights IIS application pool identity.
---

# Modify Insights IIS App Pool Identity

_Applies to: Patch My PC Advanced Insights_

This section describes the steps required to change the IIS Application pool identity used for an existing Advanced Insights deployment.

> The ability to change the IIS application pool identity using the modify feature is supported in version 2.4.1 and later.

> Review the IIS Application pool identity details here: \[advanced-insights-iis-application-pool-identity.md]\(../advanced-insights-iis-application-pool-identity.md "mention")

In the configuration modification page, select the checkbox for **'IIS Application Pool Identity'** then click **'Change Identity'**:

![Clicking 'Change identity'](../../.gitbook/assets/image-\(4355\).png)

Select 'Local System' or to set a custom identity using an Active Directory account, select 'Specific User':

In this example we will set a custom identity using an Active Directory account. After entering the account username and password, (The domain value should already be pre-populated by the installer) the 'Check Credentials' button can be used to validate the account credentials entered.

Click OK

The confirmation page is then displayed. Click close to exit the installer.

This completes the steps required to modify the IIS Application Pool identity.

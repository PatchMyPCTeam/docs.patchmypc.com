# Insights Custom Client Actions

_Applies to: Patch My PC Advanced Insights_

> Advanced Insights must be granted the correct permissions to your SMS Provider for these actions to work. See \[Configuration Manager Permissions]\(../insights-configuration-manager-permission-requirements.md).

Clients with the Inventory Extensions MSI installed will support the use of our custom client actions:

![](/_images/ClientActions-(1).png>)

### ⚙ Script Approval

If you see this message when using any of the custom client actions:

![](/_images/image-(1670).png)

This means you have the "Additional Script Approver" setting enabled in ConfigMgr. To approve our script, please follow these steps:

![](/_images/script-approval.png)

1. Open your ConfigMgr Console
2. Go to Software Library > Scripts
3. Right click and approve the "Advanced Insights Client Actions" script

### Custom Action Descriptions

* Notify - Sends a message box to all users logged in on the client, this message includes the<br>
* Install Updates - Installs all updates which are advertised to the device which are targeted as available or required. This is the same action as pressing Install All in the Software Center.
* Repair Client - Executes the ccmrepair.exe
* Clear CCM Cache - Clears all ccmcache items on the client (including persistent cache)
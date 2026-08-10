# Manage Return Codes option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Manage Return Codes** right-click option in Patch My PC (PMPC) Publisher lets you control how installer exit codes are interpreted for a product in Publisher.

Each Return Code can be mapped to a specific code type to influence how the installation result is reported and how restart behavior is handled on the client.

This feature is commonly used to suppress reboot behavior or to ensure that non-standard success codes are correctly treated as successful installations.

> \*\*Important\*\*
>
> The management platform can also influence how devices respond to Return Codes, particularly regarding restart behavior.
>
> Review the relevant Microsoft documentation for [Intune](https://learn.microsoft.com/en-us/intune/intune-service/apps/apps-win32-app-management#set-win32-app-availability-and-notifications), [ConfigMgr](https://learn.microsoft.com/en-us/intune/configmgr/core/clients/deploy/device-restart-notifications), or [WSUS](https://learn.microsoft.com/en-us/windows/deployment/update/waas-restart) to ensure Return Codes and restart actions behave as expected in your environment.

## Return Code Mapping

Each Return Code returned by the installer is associated with a code type. The code type determines how Patch My PC ScriptRunner (which manages the installation) and the management platform interpret the result.

When you select the **Manage Return Codes** right-click option, the **Manage Return Codes** dialog appears, where you can manage Return Codes for the selected product.

![Manage Return Codes dialog](../../../.gitbook/assets/image-\(4769\).png)

The following Return Codes are commonly used by default:

<table><thead><tr><th width="128.77783203125" valign="top">Return Code</th><th width="123.77777099609375" valign="top">Code Type</th><th valign="top">Meaning</th></tr></thead><tbody><tr><td valign="top">0</td><td valign="top">Success</td><td valign="top">Installation completed successfully</td></tr><tr><td valign="top">1707</td><td valign="top">Success</td><td valign="top">Product is already installed or no action was required</td></tr><tr><td valign="top">3010</td><td valign="top">SoftReboot</td><td valign="top">Installation succeeded and a reboot is recommended</td></tr><tr><td valign="top">1641</td><td valign="top">HardReboot</td><td valign="top">Installation succeeded and triggered an immediate reboot</td></tr><tr><td valign="top">1618</td><td valign="top">Retry</td><td valign="top">Another installation is in progress and the deployment should retry</td></tr></tbody></table>

## Custom Return Codes

Some installers return non-standard exit codes, even when the installation succeeds. In these cases, you can add a custom Return Code and map it to **Success**.

For example, **Brave Browser** always exits with Return Code **19** on a successful installation.

As **19** is not treated as a success code by default, it can be mapped to **Success** so that the successful deployment is reported correctly.

To add a custom Return Code:

1. Locate the relevant product in the Product Tree.
2. Right-click it and select **Manage Return Codes**
3. On the **Manage Return Codes** dialog, click **Add**

![Clicking 'Add' on the 'Manage Return Codes' dialog](../../../.gitbook/assets/image-\(4770\).png)

4. In the **Return Code** field, enter the required Return Code (for example **19**), and if the **Code Type** should be anything other than **Success**, select the relevant value from the **Code Type** dropdown beside the new Return Code.

![Configuring the new Return Code](../../../.gitbook/assets/image-\(4771\).png)

5. Click **OK** to save your changes.

![Clicking 'OK' to save your changes](../../../.gitbook/assets/image-\(4773\).png)

The **Manage Return Codes** dialog updates to show the new Return Code.

!['Manage Return Codes' dialog showing the new Return Code](../../../.gitbook/assets/image-\(4774\).png)

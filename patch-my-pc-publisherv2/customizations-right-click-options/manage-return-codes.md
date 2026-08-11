# Manage Return Codes

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: Product_\
_Available on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

The **Manage Return Codes** option allows you to control how installer exit codes are interpreted for a product in the Publisher. Each return code can be mapped to a specific code type to influence how the installation result is reported and how restart behavior is handled on the client.

<figure><img src="../../.gitbook/assets/image (4017).png" alt="Manage Return Codes" width="455"><figcaption></figcaption></figure>

This feature is commonly used to suppress reboot behavior or to ensure that non standard success codes are correctly treated as successful installations.

{% hint style="warning" %}
**Important**

The management platform can also influence how devices respond to return codes, especially in relation to restart behaviour. Review the relevant documentation for [Intune](https://learn.microsoft.com/en-us/intune/intune-service/apps/apps-win32-app-management#set-win32-app-availability-and-notifications), [ConfigMgr](https://learn.microsoft.com/en-us/intune/configmgr/core/clients/deploy/device-restart-notifications) or [WSUS](https://learn.microsoft.com/en-us/windows/deployment/update/waas-restart) to ensure return codes and restart actions behave as expected in your environment.
{% endhint %}

## Return Code Mapping

Each return code returned by the installer is associated with a code type. The code type determines how the Patch My PC ScriptRunner, which managers the installation, and the management platform interpret the result.

<figure><img src="../../.gitbook/assets/image (4018).png" alt="Return Code Values" width="450"><figcaption></figcaption></figure>

The following return codes are commonly used by default:

| Return Code | Code Type  | Meaning                                                             |
| ----------- | ---------- | ------------------------------------------------------------------- |
| 0           | Success    | Installation completed successfully                                 |
| 1707        | Success    | Product is already installed or no action was required              |
| 3010        | SoftReboot | Installation succeeded and a reboot is recommended                  |
| 1641        | HardReboot | Installation succeeded and triggered an immediate reboot            |
| 1618        | Retry      | Another installation is in progress and the deployment should retry |

## Custom Return Codes

Some installers return non standard exit codes even when the installation succeeds. In these cases, you can add a custom return code and map it to Success.

For example, Brave Browser always exits with return code 19 on a successful installation. Because 19 is not treated as a success code by default, it is mapped to Success so the deployment is reported correctly.

<figure><img src="../../.gitbook/assets/image (4019).png" alt="Custom Return Codes" width="450"><figcaption></figcaption></figure>

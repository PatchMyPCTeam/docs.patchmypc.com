# Process Restart Prevention section of Manage Conflicting Processes in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

If the **Prevent the end-user from opening an application while the application is updating** checkbox is checked (under the **Process Restart Prevention** section of **Manage Conflicting Processes** section of Patch My PC (PMPC), the end user is prevented from reopening the application whilst it is updated.

This helps avoid scenarios where the application is closed for the update but immediately relaunched, which could cause the installation to fail or be delayed.

<figure><img src="../../../../.gitbook/assets/image (750).png" alt="&#x27;Process Restart Prevention&#x27; setting" width="501"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

This option is only available at the Product level and should be used for applications where restarting the process during installation is likely to interfere with a successful update.
{% endhint %}

{% hint style="danger" %}
**Important**

Checking the **Prevent the end-user from opening an application while the application is updating** checkbox is **not recommended** in most scenarios due to the potential for user disruption and residual system changes if the update process does not complete cleanly.

For some applications (such as Google Chrome), enabling this setting can prevent the application from updating. These applications rely on helper processes or self-update mechanisms that must be able to launch during the update process. Blocking the executable using Image File Execution Options can interfere with this behavior and cause the update to fail consistently.
{% endhint %}

## How Process Restart Prevention works

When the **Prevent the end-user from opening an application while the application is updating** checkbox is checked, Publisher uses the Windows Image File Execution Options feature to block the application from launching.

Publisher creates a temporary registry entry for the application executable under the Image File Execution Options path. If the user attempts to launch the application during the update, they may see a message such as:

> "An update is currently being installed on your computer. Please do not try to start the application"

or

> "The requested operation requires elevation"

<figure><img src="../../../../.gitbook/assets/image (3986).png" alt="Prevent the end user from opening an application" width="479"><figcaption></figcaption></figure>

## Potential Risks

If the ScriptRunner process is forcefully terminated or exits unexpectedly, the Image File Execution Options registry entries may not be cleaned up correctly.&#x20;

In that case, users may continue to see the blocking message even though no installation or update is running.

If this happens, you must remove the registry entry for the affected process manually.

Depending on the operating system architecture and the application being blocked, you may need to check one or both of the following registry paths:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options
HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion\Image File Execution Options
```

Look for subkeys named after the blocked executable, such as `notepad++.exe`.

<figure><img src="../../../../.gitbook/assets/image (3987).png" alt="Image File Execution Options registry entries" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

When Patch My PC ScriptRunner runs on a device, it checks for legacy Image File Execution Options entries created by previous Patch My PC update attempts that were not cleaned up correctly. If it detects these entries, ScriptRunner removes them automatically.

This cleanup occurs only when another Patch My PC application or update runs on the device. If no further Patch My PC deployments run, stale registry entries may remain.

For this reason, if users are blocked from launching an application due to leftover Image File Execution Options entries, a manual registry cleanup or [PowerShell-based Remediation Script](process-restart-prevention.md#powershell-based-remediation-script) is often required to immediately restore application access.
{% endhint %}

## **PowerShell-based Remediation Script**

If required, the following PowerShell script can be used to locate and remove all Image File Execution Options entries created by Patch My PC ScriptRunner for process blocking:

```powershell
Get-ChildItem "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options" -ea SilentlyContinue |
Where-Object {
    if ($_.Property -contains "Debugger") {
        ($_ | Get-ItemProperty).Debugger -like "*PreventStart*"
    }
} | Remove-Item -Force -Recurse;

Get-ChildItem "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options" -ea SilentlyContinue |
Where-Object {
    if ($_.Property -contains "Debugger") {
        ($_ | Get-ItemProperty).Debugger -like "*PreventStart*"
    }
} | Remove-Item -Force -Recurse;

```

# Common PSADT Techniques for Deployments in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

You can use PSAppDeployToolkit (PSADT) functions in the scripts of a Patch My PC (PMPC) Cloud deployment. This lets you do things the deployment wizard does not offer natively, such as showing an installation progress dialog, prompting the user, or copying files to every user profile.

This page explains how PSADT is loaded, how to add a PSADT script to a deployment, and gives copy-and-paste examples for common scenarios.

## How PSADT is loaded

You do not need to download, import, or upload the PSADT module yourself. PMPC Cloud detects PSADT functions in your script and bundles the toolkit with the deployment.

When you type or paste a PSADT function into the script editor:

* The **Script Format** field changes from **.ps1** to **.ps1** plus the PSADT logo.
* A warning appears confirming that PSADT functions were detected.



<figure><img src="../../../.gitbook/assets/image (1660).png" alt="PSADT Function Detected" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Devices that receive the deployment must have .NET Framework 4.7.2 or greater installed.
{% endhint %}

* The **Enable PSADT Module** checkbox is enabled, which uploads the PSADT Toolkit to Intune when the deployment is created.

<figure><img src="../../../.gitbook/assets/image (1661).png" alt="PSADT Module Enabled" width="563"><figcaption></figcaption></figure>

PSADT v3 and v4 functions are both supported. The examples on this page use v4 functions, which start with the `ADT` prefix, for example `Show-ADTInstallationProgress`.

## Add a PSADT Script to a Deployment

1. Either [deploy](../deploy-app/) or edit an existing deployment for the relevant app.
2. Navigate to the **Configurations** tab.
3. Click **Add** beside **Additional Tools**, then select the **Scripts** tool.
4. Click **Add** beside **Pre-Install** or **Post-Install**.
5. Enter a **Script Name**.
6. Leave **Script Format** set to **.ps1**.
7. Paste an example from below into the script editor. The **Script Format** field changes to **.ps1** plus the PSADT logo, and a warning confirms that PSADT functions were detected.
8. If the scenario requires it, check the **Run the pre-update script before performing any auto-close or skip process checks** checkbox.
9. Click **Save**.

See [Configure Scripts in a Patch My PC Cloud Deployment](../deploy-app/configurations-tab/additional-tools/scripts/) for every option in the **Scripts** tool.

## Scenarios

Use this table to find the scenario you need and where to add its script. "Run before process checks" refers to the **Run the pre-update script before performing any auto-close or skip process checks** checkbox on a Pre-Install script.

<table data-search="false"><thead><tr><th valign="top">Scenario</th><th valign="top">Add as</th><th valign="top">Run before process checks</th></tr></thead><tbody><tr><td valign="top"><a href="common-psadt-techniques.md#show-an-installation-progress-dialog">Show an installation progress dialog</a></td><td valign="top">Pre-Install</td><td valign="top">No</td></tr><tr><td valign="top"><a href="common-psadt-techniques.md#show-a-message-when-the-installation-completes">Show a message when the installation completes</a></td><td valign="top">Post-Install</td><td valign="top">Not applicable</td></tr><tr><td valign="top"><a href="common-psadt-techniques.md#show-a-restart-prompt">Show a restart prompt</a></td><td valign="top">Post-Install</td><td valign="top">Not applicable</td></tr><tr><td valign="top"><a href="common-psadt-techniques.md#copy-files-to-all-user-profiles">Copy files to all user profiles</a></td><td valign="top">Post-Install</td><td valign="top">Not applicable</td></tr><tr><td valign="top"><a href="common-psadt-techniques.md#set-a-registry-value-for-all-users">Set a registry value for all users</a></td><td valign="top">Post-Install</td><td valign="top">Not applicable</td></tr><tr><td valign="top"><a href="common-psadt-techniques.md#allow-users-to-move-the-dialog">Allow users to move the conflicting process dialog</a></td><td valign="top">Pre-Install</td><td valign="top">Yes</td></tr><tr><td valign="top"><a href="common-psadt-techniques.md#change-the-dialog-accent-color">Change the dialog accent color</a></td><td valign="top">Pre-Install</td><td valign="top">Yes</td></tr><tr><td valign="top"><a href="common-psadt-techniques.md#show-a-custom-message">Show a custom message on the conflicting process dialog</a></td><td valign="top">Pre-Install</td><td valign="top">Yes</td></tr><tr><td valign="top"><a href="common-psadt-techniques.md#relaunch-apps-that-were-closed-for-the-installation">Relaunch apps that were closed for the installation</a></td><td valign="top">Pre-Install and Post-Install</td><td valign="top">Yes</td></tr><tr><td valign="top"><a href="common-psadt-techniques.md#prompt-for-and-validate-a-license-key">Prompt for and validate a license key</a></td><td valign="top">Pre-Install</td><td valign="top">No</td></tr></tbody></table>

### User Dialogs

#### Show an Installation Progress Dialog

Shows a progress dialog to the user while the app installs.

**Add as:** Pre-Install

```powershell
Show-ADTInstallationProgress
```

The progress dialog closes automatically when the deployment ends. You only need to close it yourself if you want to show another dialog afterward. To do that, add this line to the top of a Post-Install script:

```powershell
Close-ADTInstallationProgress
```

#### Show a Message When the Installation Completes

Shows a prompt with an **OK** button after the app installs. `-NoWait` lets the deployment finish without waiting for the user, and `-Timeout 600` closes the prompt after 10 minutes.

**Add as:** Post-Install

```powershell
Show-ADTInstallationPrompt -Message 'Installation complete!' -ButtonRightText 'OK' -NoWait -Timeout 600
```

#### Show a Restart Prompt

Prompts the user to restart the device after the app installs. Use one of the two options below.

**Add as:** Post-Install

```powershell
# Restart prompt with no countdown
Show-ADTInstallationRestartPrompt -NoCountdown

# Restart prompt with a one-hour countdown
Show-ADTInstallationRestartPrompt -CountdownSeconds 3600
```

### User Profiles

#### Copy Files to All User Profiles

Copies a file or folder into every user profile on the device. Upload the files as **Extra Files** in the same deployment, then reference them with `$PSScriptRoot`.

**Add as:** Pre-Install or Post-Install

```powershell
# Copy a file to AppData\Roaming\MyApp in every user profile
Copy-ADTFileToUserProfiles -Path "$PSScriptRoot\config.txt" -Destination 'AppData\Roaming\MyApp'

# Copy a folder recursively to AppData\Local in every user profile
Copy-ADTFileToUserProfiles -Path "$PSScriptRoot\MyApp" -BasePath LocalAppData -Recurse

# Copy a document to a MyApp folder under each user's Documents folder
Copy-ADTFileToUserProfiles -Path "$PSScriptRoot\Document.docx" -Destination 'MyApp' -BasePath Documents
```

{% hint style="info" %}
**Note**

`-Destination` is relative to `-BasePath`. If you do not set `-BasePath`, the destination is relative to the root of each user profile.
{% endhint %}

#### Set a Registry Value for All Users

Writes a value to the `HKEY_CURRENT_USER` hive of every user profile on the device. Keep `-SID $_.SID` on each registry command inside the script block so that it targets each user in turn.

**Add as:** Pre-Install or Post-Install

```powershell
Invoke-ADTAllUsersRegistryAction {
    Set-ADTRegistryKey -LiteralPath 'HKCU\Software\MyApp' -Name 'AutoUpdate' -Value 0 -Type DWord -SID $_.SID
}
```

### Customize the Conflicting Process Dialog

These examples change how the manage conflicting processes dialog looks and behaves. They only take effect if the script runs before the dialog is shown.

{% hint style="info" %}
**Note**

For every example in this section, check the **Run the pre-update script before performing any auto-close or skip process checks** checkbox on the Pre-Install script.
{% endhint %}

#### Allow Users to Move the Dialog

Lets users drag the dialog to a different position on the screen.

**Add as:** Pre-Install

```powershell
$PSDefaultParameterValues['Show-ADTInstallationWelcome:AllowMove'] = $true
```

You can use `$PSDefaultParameterValues` in the same way to change the default value of other PSADT function parameters.

#### Change the Dialog Accent Color

Changes the accent color used by PSADT dialogs. The value is a hex color that includes the alpha channel. This example sets it to red.

**Add as:** Pre-Install

```powershell
(Get-ADTConfig).UI.FluentAccentColor = 0xFFFF0000
```

#### Show a Custom Message

Adds your own message to the dialog that asks users to close their apps.

**Add as:** Pre-Install

```powershell
(Get-ADTStringTable).CloseAppsPrompt.CustomMessage = 'Please close these apps so the update can be installed.'
$PSDefaultParameterValues['Show-ADTInstallationWelcome:CustomText'] = $true
```

### Advanced Examples

#### Relaunch Apps That Were Closed for the Installation

Records which apps the signed-in user had open before they were closed, then relaunches them after the app installs. This scenario needs two scripts.

**Step 1 - Add as:** Pre-Install, with the **Run the pre-update script before performing any auto-close or skip process checks** checkbox checked.

Replace `'notepad', 'pwsh'` with the process names you want to relaunch.

```powershell
$RunningProcesses = Get-ADTRunningProcesses 'notepad', 'pwsh' | Where-Object { $_.Username -eq $RunAsActiveUser.NTAccount }
```

**Step 2 - Add as:** Post-Install

This script selects one instance of each executable and relaunches it as the signed-in user, with its original arguments if it had any.

```powershell
if ($RunAsActiveUser) {
    $ProcessesToRelaunch = $RunningProcesses | Where-Object { $_.Username -eq $RunAsActiveUser.NTAccount } | Group-Object -Property FileName | ForEach-Object { $_.Group | Select-Object -First 1 }
    foreach ($Process in $ProcessesToRelaunch) {
        $ProcessArgs = @{
            FilePath = $Process.FileName
            NoWait   = $true
        }
        if ($null -ne $Process.Arguments) {
            $ProcessArgs.ArgumentList = $Process.Arguments
        }
        Start-ADTProcessAsUser @ProcessArgs -ErrorAction SilentlyContinue
    }
}
```

{% hint style="info" %}
**Note**

You may not always want to relaunch every app or reuse its original arguments. Adjust the filter and the `ArgumentList` logic to suit the app.
{% endhint %}

#### Prompt For and Validate a License Key

Asks the user for a license key if one is not already set, checks that it matches the expected format, and saves it to the registry. The user can select **Trial** to skip activation. The prompt repeats until the user enters a valid key or selects **Trial**.

**Add as:** Pre-Install

Replace the registry path, the placeholder text, and the validation pattern with values that match your app.

```powershell
$LicenseKey = $null
if (Get-ADTRegistryKey -LiteralPath 'HKLM\Software\MyApp' -Name 'LicenseKey') {
    Write-ADTLogEntry -Message 'MyApp is already installed, bypassing license prompt.'
}
else {
    Write-ADTLogEntry -Message 'MyApp is not installed, prompting for license key.'
    $LicenseText = 'XXXX-XXXX-XXXX-XXXX-XXXX'
    $ValidationMessage = $null
    do {
        $LicensePrompt = Show-ADTInstallationPrompt -RequestInput -Message "Please enter your license key or select Trial:$ValidationMessage" -DefaultValue $LicenseText -ButtonLeftText 'Activate' -ButtonRightText 'Trial'
        if ($LicensePrompt.Result -eq 'Activate') {
            $LicenseText = $LicensePrompt.Text.Trim()
            if ($LicenseText -ne 'XXXX-XXXX-XXXX-XXXX-XXXX' -and $LicenseText -match '^[A-Za-z0-9]{4}(-[A-Za-z0-9]{4}){4}$') {
                $LicenseKey = $LicenseText
                Write-ADTLogEntry 'Valid license key entered.'
                Set-ADTRegistryKey -LiteralPath 'HKLM\Software\MyApp' -Name 'LicenseKey' -Value $LicenseKey -Type String
            }
            else {
                $ValidationMessage = "`n`n[accent][italic]License key invalid[/italic][/accent]"
            }
        }
        else {
            Write-ADTLogEntry -Message 'Trial mode selected.'
        }
    } until ($LicensePrompt.Result -eq 'Trial' -or $LicenseKey)
}
```

{% hint style="info" %}
**Note**

This example needs a signed-in user to answer the prompt. Test how it behaves on a device with no user signed in before you assign the deployment as **Required**.
{% endhint %}

## Related Resources

* [Configure Scripts in a Patch My PC Cloud Deployment](../deploy-app/configurations-tab/additional-tools/scripts/)
* [Using Pre-Install Scripts in a Patch My PC Cloud Deployment](../deploy-app/configurations-tab/additional-tools/scripts/pre-install-scripts.md)
* [Use Patch My PC Scripts in a Patch My PC Cloud Deployment](use-pmpc-scripts.md)
* PSADT function reference:&#x20;
  * <a href="https://psappdeploytoolkit.com/docs/reference/functions/Show-ADTInstallationProgress" target="_blank">Show-ADTInstallationProgress</a>
  * <a href="https://psappdeploytoolkit.com/docs/reference/functions/Show-ADTInstallationPrompt" target="_blank">Show-ADTInstallationPrompt</a>
  * <a href="https://psappdeploytoolkit.com/docs/reference/functions/Show-ADTInstallationRestartPrompt" target="_blank">Show-ADTInstallationRestartPrompt</a>
  * <a href="https://psappdeploytoolkit.com/docs/reference/functions/Copy-ADTFileToUserProfiles" target="_blank">Copy-ADTFileToUserProfiles</a>
* <a href="https://psappdeploytoolkit.com/docs/getting-started/changes-in-v4" target="_blank">PSADT: Changes in v4</a>

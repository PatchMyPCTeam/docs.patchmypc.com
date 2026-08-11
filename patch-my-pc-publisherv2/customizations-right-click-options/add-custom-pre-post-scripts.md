# Add Custom Pre/Post Scripts

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: Product_\
_&#x41;vailable on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

The **Add Custom Pre/Post Scripts** option in the Publisher allows you to run your own scripts before or after an installation or an uninstallation. This includes pre install, post install, pre uninstall, and post uninstall scenarios.

![Add Custom Pre/Post Scripts](../../.gitbook/assets/image-\(3999\).png)

This feature provides flexibility for handling scenarios that are not supported by the installer alone. It allows you to perform preparation steps before an install or update, as well as cleanup or validation steps after completion.

Common use cases include uninstalling previous versions or different installer variants, such as removing an EXE based installation to standardize on an MSI deployment, removing conflicting or superseded software, and performing environment specific actions.

The feature also allows additional files and folders to be bundled with the application or update content, ensuring all required supporting files are available during installation.

Selecting this option opens the configuration dialog where scripts, arguments, and additional content can be defined.

![Custom Pre/Post Scripts and Files UI](../../.gitbook/assets/image-\(4000\).png)

The Add Custom Pre Post Scripts form defines how scripts and additional content are associated with an application or update. The options are available separately for Install and Uninstall.

## Install and Uninstall tabs

The Install tab controls the scripts that run during installation or update. The Uninstall tab controls the scripts that run during application removal.

Each tab is configured independently, allowing different pre and post scripts to be defined for install and uninstall scenarios.

Additional files and additional folders are shared between both tabs. All scripts, files, and folders defined in the form are packaged together into the same application or update content. The same bundled content is therefore available to both install and uninstall scripts.

## Pre/Post Script

Pre and Post scripts can be any of the following file types.

* .bat
* .ps1
* .vbs
* .exe
* .msi

The **Pre Script** field allows you to select a script that runs before the install or uninstall begins. This is commonly used for preparation tasks such as uninstalling previous versions, removing a different installer variant, or validating prerequisites.

The **Post Script** field allows you to select a script that runs after the install or uninstall completes. This is commonly used for cleanup, configuration, validation, or logging tasks.

The **Argument** field allows parameters to be passed to the selected script at runtime.

The **Insert Variable** links allow supported variables to be inserted directly into the Arguments field. These variables resolve at runtime and can be used to pass values such as vendor name, product name, version, package ID, and installer return code to the script.

Use the steps below to configure a pre script or post script:

### Select a Script

1. Locate the Pre Script or Post Script field.
2. Select **Browse** next to the field.
3. Browse to a supported script file and select it.
4. Click **OK** to populate the field.
5. Leave the field empty if no script is required for that phase.

### Script Arguments

1. Click inside the Argument field for the selected script.
2. Enter any required parameters.
3. Place the cursor where a variable is required.
4. Select the appropriate option under Insert Variable to add it to the field.

> \*\*Note\*\*
>
> Variables are expanded at runtime and provide application specific values to the script.

**Include Quotes in Arguments**\
If you need to include quotes in the Arguments field, escape the quotes with a backslash.

Example:

```
-String \"Hello world\"
```

**PowerShell Arrays**\
When passing multiple values to a PowerShell script, do not use traditional PowerShell array syntax in the Arguments field. Because PowerShell is launched from cmd.exe, syntax like `"Item1","Item2"` is not interpreted as a single array value.

Instead, pass a single delimited string and split it inside the script.

Example:

```powershell
-MyParameter "Item1,Item2,Item3"
```

![Parse a PowerShell array as a parameter](../../.gitbook/assets/image-\(4001\).png)

### Configure Pre Script Behavior

The **Don’t attempt software update if the pre script returns an exit code other than 0 or 3010** option can be checked if the deployment must stop when the pre script fails.

When this happens, Patch My PC ScriptRunner, which manages the installation process, stops and returns a specific exit code to the calling client such as the ConfigMgr client, the Windows Update Agent or the Intune Management Extension.\
\
There are 2 exit codes you may see when a pre script does not run successfully.

* Exit code `32768` is returned when a Patch My PC recommended pre install script fails. These scripts are provided by Patch My PC for certain products that, for example, cannot remove older versions on their own, such as Oracle Java. If the recommended script cannot run or does not exit cleanly, ScriptRunner stops the installation immediately and returns `32768`. This behaviour is always enforced for recommended scripts.
* Exit code `32767` is returned when a custom pre script, supplied by the you, fails and the checkbox for **Don’t attempt software update if the pre script returns an exit code other than 0 or 3010** is selected. If that option is not selected, ScriptRunner continues even if the customer script returns a non-zero exit code.

More information on ScriptRunner exit codes can be found at [https://patchmypc.com/kb/script-runner-exit-codes/](https://patchmypc.com/kb/script-runner-exit-codes/)

The **Run the pre update script before performing any auto close or skip process checks** option can be checked if the pre script must run before conflicting process handling. If you are using the [Manage Conflicting Processes](manage-conflicting-processes/) option and this box is enabled, the pre script runs before the process check.

> \*\*Important\*\*
>
> These 2 options apply only to pre scripts and have no effect on post scripts.

## Additional Files and Folders

The A**dditional files and Folders** sections allow you to bundle extra content with the application or update package. This content is included in the package even if no pre or post scripts are configured.

All files and folders added here are packaged together with the application and are downloaded to the local installation source directory on the client device at install or update time.

### **Additional files**

Use Additional files to include individual files that must be present during installation or uninstallation.

To add files:

1. Select Browse in the Additional files section.
2. Select one or more files.
3. Click **Open** to add the file(s) to the list.

Typical use cases include configuration files, license files, or other supporting resources required by the installer or scripts.

> \*\*Note\*\*
>
> To bundle an MST file with an MSI application, it is simpler to use the \[Add MST Transformation File]\(add-mst-transformation-file.md) customization option.

### **Additional folders**

Use Additional folders to include entire directories and their contents.

To add folders:

1. Select Browse in the Additional folders section.
2. Select a folder.
3. Click **Select Folder** to add the folder(s) to the list.

All files and subfolders within the selected directory are included in the package.

### **Packaging and availability**

Additional files and folders are shared between the Install and Uninstall tabs. The same bundled content is available to both install and uninstall scripts because all scripts and content are packaged together into a single application or update package.

All bundled files and folders are downloaded to the local installation source directory on the client device at runtime. Scripts and installers can reference this content using relative paths.

For example, a script can reference a bundled file or folder by using the local source directory path, such as:

```powershell
.\config.xml
.\SupportFiles\setup.ini
```

This allows scripts to source configuration files, or other supporting content directly from the packaged source without relying on external locations.

## Uninstall-Software.ps1

A commonly used approach for removing existing software before installation is to use the Uninstall Software community script provided by Patch My PC. This script is useful when you need to uninstall a previous version, remove a different installer variant, or clean up related software before deploying a standardized package.

The script is available from the Patch My PC Community Scripts repository [https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Uninstall/Pre-Uninstall/Uninstall-Software](https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Uninstall/Pre-Uninstall/Uninstall-Software)

### How to Configure the Script as a Pre Script

To configure Uninstall-Software.ps1 as a pre script:

1. Download **Uninstall-Software.ps1** from the community repository.
2. In the **Add Custom Pre/Post Scripts** form, select the Install or Uninstall tab as required.
3. Select **Browse** next to the Pre Post Script field.
4. Select **Uninstall-Software.ps1** and click **Open**.

### Configure the Script Arguments

The Uninstall Software community script supports parameters such as **DisplayName** to determine which application should be uninstalled. The script documentation in the repository shows examples written in native PowerShell syntax.

When configuring this script in the Publisher, the **Uninstall-Software.ps1** script file itself is selected in the Pre Script field. The Arguments field must contain only the parameters.

> \*\*Note\*\*
>
> Any quotation marks in the arguments must be escaped with a backslash.

The following example is shown in the script [README](https://github.com/PatchMyPCTeam/Community-Scripts/blob/main/Uninstall/Pre-Uninstall/Uninstall-Software/readme.md) and represents native PowerShell usage.

```powershell
Uninstall-Software.ps1 -DisplayName "Greenshot"
```

In the Publisher, configure the script as follows.

* Pre Script : `Uninstall-Software.ps1`
* Arguments : `-DisplayName \"Greenshot\"`

In this example, the script attempts to uninstall any installed application with a display name matching **Greenshot** before the main installation or uninstallation proceeds. Other parameters documented in the script [README](https://github.com/PatchMyPCTeam/Community-Scripts/blob/main/Uninstall/Pre-Uninstall/Uninstall-Software/readme.md) can also be used to perform more targeted uninstall

Advanced Configurations and Examples

The following knowledge base articles provide practical examples of how to leverage pre and post scripts or additional files when configuring applications and updates in the Publisher:

* [How to customize your TeamViewer App or Update](https://patchmypc.com/how-to-customize-teamviewer)
* [Advanced Application Configuration using Pre/Post Scripts](https://patchmypc.com/advanced-pre-post-scripts)
* [Pass Variables into Pre and Post Scripts](https://patchmypc.com/pass-variables-into-pre-and-post-scripts)

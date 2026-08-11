# Custom Apps "Configuration" tab

_Applies to: Patch My PC Cloud Custom Apps_

The **Configuration** tab is where you configure various properties for the Custom App.

> \*\*Note\*\*
>
> Mandatory fields are denoted by an asterisk ("<mark style="color:red;">\*\*\\\*\*\*</mark>").

## Install Context

The **Install Context** setting (if available) configures the context in which the app is installed, either **System** or **User**.

!['Install Context' setting](../../../.gitbook/assets/image-\(4210\).png)

## Architecture

The **Architecture** setting (if available) configures the app's architecture.

!['Architecture' setting](../../../.gitbook/assets/image-\(4211\).png)

> \*\*Note\*\*
>
> Detection uses this field to determine whether to look in the 32-bit or 64-bit registry keys:
>
> \`HKLM:\Software\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall\`
>
> or
>
> \`HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\`

## Version

In the **Version** field, enter the version number for this app.

!['Version' setting](../../../.gitbook/assets/image-\(4212\).png)

> \*\*Note\*\*
>
> The number entered in this field is the version of the app as shown in \*\*Add or remove programs\*\*.
>
> Detection uses this field to determine if the app is installed by looking for a matching \*\*DisplayVersion\*\* entry in the following registry key:
>
> \`HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\`

## Language

In the **Language** field, either type the language for this app or select it from the dropdown list.

!['Language' setting](../../../.gitbook/assets/image-\(4213\).png)

## Installed Apps Name

In the **Installed Apps Name** field, type the name of the app as it appears in **Add or remove programs**.

> \*\*Note\*\*
>
> Although this field is optional, if you selected \*\*Installation Script\*\* as the \*\*Installer Type\*\* on the \*\*File\*\* tab, you need to enter a value if you want to use the \*\*Patch My PC Default (Recommended)\*\* \[detection method]\(custom-apps-detection-rules-tab.md).
>
> If you plan to use a Custom detection method, then this field can be left empty.
>
> If you type a version number in this field we replace it with "\`%\`".

!['Installed Apps Name' setting](../../../.gitbook/assets/image-\(4214\).png)

> \*\*Note\*\*
>
> Detection uses this field to determine if the app is installed by looking for a matching \*\*DisplayName\*\* entry in the following registry key:
>
> \`HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\`
>
> As this field supports the \`%\` wildcard (matching any sequence of characters), limit your input to ASCII characters. If the \*\*Installed Apps Name\*\* contains non-ASCII characters or version numbers, consider replacing those with \`%\` to ensure proper matching.
>
> This will allow App Detection and Update Requirement rules to detect older versions of the app on your endpoints.

> \*\*Important\*\*
>
> As the \*\*Apps & Features Name\*\* is used to determine applicability and detection, using an overly generic name may cause Intune Updates to be detected as required on devices without the software installed.

## Conflicting processes

In the **Conflicting processes** field, type a comma-separated list of executables that may interfere with the installation of this app. This field populates the list for the [Manage Conflicting Processes](https://patchmypc.com/manage-conflicting-processes-when-updating-third-party-applications) right-click feature.

!['Conflicting processes' setting](../../../.gitbook/assets/image-\(4215\).png)

## Silent Install Parameters

In the **Silent Install Parameters** field, enter the command-line arguments (up to a maximum of 2,048 characters) used to install the app silently (i.e. the user is not aware of the installation occurring).

!['Silent Install Parameters' setting](../../../.gitbook/assets/image-\(4216\).png)

> \*\*Note\*\*
>
> Providing \`msiexec.exe /i\` for MSI installations is not required. Using \`/qn\` will be adequate for most MSI installations.
>
> Also, see \[Supported Variables in Publisher and PMPC Cloud]\(../../../patch-my-pc-product-reference/supported-variables.md) for a list of the variables we support in this field.

## MSI Product Code

In the **MSI Product Code** field, enter the MSI product code for this app, which is used for detection.

!['MSI Product Code' setting](../../../.gitbook/assets/image-\(3469\).png)

> \*\*Note\*\*
>
> This setting only applies to MSI installers.
>
> If the MSI Product Code for your installer does not update between versions, the Custom Apps Detection and Applicability rules will:
>
> \* Not detect any changes and no updates will not be installed.
>
> \* Detect the MSI app, even if an older version is installed.
>
> To work around this issue, change the MSI Product Code to all \*\*0\*\*'s (\`00000000-0000-0000-0000-0000\`) when creating the Custom App. This forces the detection and applicability scripts to fall back to DisplayName and DisplayVersion detection.

## Uninstall Command

There are two options for customizing the uninstall command:

* [Auto Discovered](custom-apps-configuration-tab.md#auto-discovered)
* [Use Custom](custom-apps-configuration-tab.md#use-custom)

> \*\*Note\*\*
>
> The \*\*Auto Discovered\*\* option is unavailable if the \*\*Installer Type\*\* on the \*\*File\*\* tab is configured as \*\*Installation Script\*\*.
>
> The \*\*Use Custom\*\* can only be used if the \*\*Installer Type\*\* for this app is configured for \*\*Installation Script\*\*.

### Auto Discovered

During uninstall, **PatchMyPC-Scriptrunner** scans the _Uninstall_ registry key and looks for a subkey that matches the application name.

* Once found, it uses the `QuietUninstallString` command from that subkey to perform the uninstall. If this String Value doesn't exist, then the information from `UninstallString` will be used.
* If no match is found, the process will exit with return code 65535 (see `PatchMyPC-ScriptRunner.log` for details).

If you specify **Additional Silent Uninstall Parameters**, these will be appended to the `UninstallString` - not to the main installation file.

### Use Custom

When selected, you can import or enter an uninstall script in the script editor.

> \*\*Note\*\*
>
> Currently, if you select the \*\*Use Custom\*\* option to add a script to publish with this app to ConfigMgr via the Publisher, the script itself is not published. We are aware of this and are working on a solution.

!['Use Custom' option](../../../.gitbook/assets/image-\(4312\).png)

## Requirements

The **Requirements** section allows you to configure custom optional requirements (including requirement rules) that must be met for the app to be deployed to the target audience.

This includes:

* [Standard Requirements](custom-apps-configuration-tab.md#standard-requirements)
* [OS Architecture Requirements](custom-apps-configuration-tab.md#os-architecture-requirements)
* [Additional Requirements Rules](custom-apps-configuration-tab.md#additional-requirements-rules)

![Requirements section](../../../.gitbook/assets/image-\(4254\).png)

> \*\*Note\*\*
>
> Configuring Requirements is optional.

### Standard Requirements

#### Minimum operating system

From the **Minimum operating system** dropdown, select the minimum operating system required by this app.

> \*\*Note\*\*
>
> The default \*\*Minimum operating system\*\* value is set to match the first value in the dropdown, which corresponds to the oldest version of Windows still supported by Microsoft. As Microsoft deprecates a Windows version, this value and the values in the dropdown list will automatically update to the oldest version still supported by Microsoft.

> \*\*Tip\*\*
>
> We recommend leaving the \*\*Minimum operating system\*\* dropdown at its default unless you need to configure a specific value. If an app/deployment is configured for a specific Windows version, when Microsoft retires that version, you will no longer be able to deploy the app unless you update this field to a supported Windows version.

#### Min RAM memory (MB)

Configure the minimum amount of RAM required to run this app.

#### Minimum CPU speed (MHz)

Configure the minimum CPU speed required to run this app.

#### Minimum number of logical processors

Configure the minimum number of logical processors required to run this app.

### OS Architecture Requirements

The _OS Architecture Requirements_ section lets you specify which operating system (OS) architectures the app can be deployed to.

By default, the relevant checkbox is checked based on the value configured in the **Architecture** field.

> \*\*Note\*\*
>
> For example, if \*\*Architecture\*\* is configured:
>
> \* As \*\*64-bit\*\*, the \*\*32-bit\*\* checkbox under \*\*OS Architecture Requirements\*\* will be unchecked and cannot be checked.
>
> \* As \*\*32-bit\*\*, the \*\*32-bit\*\* checkbox under \*\*OS Architecture Requirements\*\* will be checked and cannot be unchecked. As this is a 32-bit app, the \*\*64-bit\*\* checkbox is checked by default, but it can be checked.
>
> You also cannot uncheck the checkbox in the \*\*OS Architecture Requirements\*\* section that corresponds to the selected \*\*Architecture\*\*.
>
> The \*\*ARM\*\* checkbox in the \*\*OS Architecture Requirements\*\* section can always be checked/unchecked, regardless of the configured \*\*Architecture\*\*.

Configure the relevant settings as required.

### Additional Requirements Rules

Using the **Additional Requirements Rule** section, you can create up to 10 optional requirement rules based on the following:

* File
* Registry
* Script

To configure an Additional Requirement Rule:

1. Click **Add** in the **Additional Requirements Rules** section.

![Clicking ‘Add' in the ‘Additional Requirements Rules' section](../../../.gitbook/assets/image-\(4255\).png)

2. On the **Add Requirement Rule** screen, select the relevant type of rule from the **Rule Type** dropdown, then configure the required options as required.

![Selecting the required ‘Rule Type'](../../../.gitbook/assets/image-\(4251\).png)

> \*\*Note\*\*
>
> To configure a script-based Requirement Rule requires the PowerShell script to already exist.

<table><thead><tr><th width="112.888916015625" valign="top">Rule Type</th><th valign="top">Available Options</th></tr></thead><tbody><tr><td valign="top">File</td><td valign="top"><ul><li><strong>Path –</strong> The path to the folder you are checking for.</li><li><strong>File or Folder –</strong> The folder containing the file you are checking for.</li><li><strong>Property –</strong> Various options, such as whether the item exists or does not, the date it was created, modified, etc.</li></ul></td></tr><tr><td valign="top">Registry</td><td valign="top"><ul><li><strong>Key Path –</strong> The path to the Registry key.</li><li><strong>Value name (optional) –</strong> The name of a value contained within the specified Key Path that you want to check for.</li><li><strong>Registry key requirement –</strong> Various options, such as whether the key exists or does not, comparisons, etc.</li></ul></td></tr><tr><td valign="top">Script</td><td valign="top"><ul><li><strong>Script Name –</strong> The name of the script, which you can leave blank if you want to use the name of the script you are going to import.</li><li><strong>Import Script –</strong> Allows you to browse to an existing PowerShell script to import.</li></ul><p><mark style="color:blue;"><strong>NOTE</strong></mark><br>If the script is unsigned, you will see the <strong>Script was detected as unsigned</strong> warning.</p><ul><li><strong>Script –</strong> Shows the script’s content.</li></ul><p><mark style="color:blue;"><strong>NOTE</strong></mark><br>You cannot modify the script in the <strong>Script</strong> window.</p><ul><li><strong>Select output data type -</strong> Various options, such as type, version, etc.</li></ul></td></tr></tbody></table>

3. Configure the following additional options based on the type of rule you are creating.

<table><thead><tr><th width="140.6666259765625" valign="top">Rule Type</th><th valign="top">Additional Options</th></tr></thead><tbody><tr><td valign="top">File or Registry</td><td valign="top"><ul><li><strong>Associated with a 32-bit app on 64-bit clients –</strong> If enabled, allows the rule to expand any path environment variables in the 32-bit context on 64-bit endpoints.</li></ul></td></tr><tr><td valign="top">Script</td><td valign="top"><ul><li><strong>Run script as 32-bit process on 64-bit clients –</strong> If enabled, allows the script to be run in a 32-bit process on 64-bit clients. If disabled, the script runs in a 64-bit process on 64-bit clients and in a 32-bit process on 32-bit clients.</li><li><strong>Run this script using the logged on credentials -</strong> Run the script using the credentials signed in to the device.</li><li><strong>Enforce signature check –</strong> If enabled, verifies that the script is signed by a trusted publisher, allowing the script to run without warnings or prompts. The script will run unblocked. If disabled, will require the end user to confirm they are happy for the script to run, but without signature verification.</li></ul><p><mark style="color:blue;"><strong>NOTE</strong></mark><br>If the script imported is unsigned, you will be unable to enable this option.</p></td></tr></tbody></table>

> \*\*Note\*\*
>
> In terms of Scripts, in the current version:
>
> \* We only support PowerShell (.ps1) scripts
>
> \* You can only import a single script per Requirement Rule.
>
> \* We do not sign your scripts if we use them in one of our deployments. If this is a requirement, you will need to sign the scripts yourself.

4. Click **Add Rule** to add the requirement rule.

![Clicking ‘Add Rule' to add the requirement rule](../../../.gitbook/assets/image-\(4252\).png)

The rule is added to the list of requirement rules.

![Rule added to the list of requirement rules](../../../.gitbook/assets/image-\(4256\).png)

> \*\*Note\*\*
>
> You can:
>
> \* Edit a Requirements Rule by clicking the pencil icon beside the relevant rule, making the required changes, then clicking \*\*Save Rule\*\* to save the changes.
>
> \* Delete a Requirements Rule by clicking the red trash can beside the relevant rule to remove it from the list of rules.

5. Repeat the steps in this section to add any additional requirement rules.

## Return Codes

A _Return Code_ (also referred to as an _exit code_), is a numeric value a program, process or function passes back to the calling entity (such as the operating system or another program) to indicate the outcome of the operation.

If you do not want to modify the **Return Codes** for this app, go to [Next Steps](custom-apps-configuration-tab.md#next-steps).

> \*\*Note\*\*
>
> See the \[Return Codes (optional)]\(/broken/pages/FjVHPN2yhI29Pv745mcA) section of \[Deploy an App]\(../../deployments/deploy-app/) for details on managing the Return Codes for a Deployment.
>
> Also, if a Return Code defined in a Custom App has the same value but a different \*\*Code type\*\* to that defined in the deployment, the settings in the deployment take precedence.

### Add A New Return Code

If you do not want to add a new Return Code, proceed to [Edit a Return Code](custom-apps-configuration-tab.md#edit-a-return-code).

![Adding a new Return Code](../../../.gitbook/assets/image-\(3327\).png)

To add a new Return Code for this Custom App, enter the numerical value in the **Return Code** field, select its meaning from the **Code type** dropdown, then click **Add**.

> \*\*Note\*\*
>
> A Return Code must be a unique integer up to 10 digits long. You can add as many Return codes as your app supports. In the current release, you cannot edit or specify your own Code type as these are managed in Intune.

The new Return Code is added to the list.

![New Return Code added to the list.](../../../.gitbook/assets/image-\(3328\).png)

### Edit a Return Code

If you do not want to edit a Return Code, go to [Delete a Return Code](custom-apps-configuration-tab.md#delete-a-return-code).

![Clicking the pencil icon beside a Return Code to edit it.](../../../.gitbook/assets/image-\(3329\).png)

To edit a Return Code, click the pencil icon beside it, then choose the correct **Code type** for this Return Code from the dropdown list.

![Choosing the correct 'Code type' from the dropdown list](../../../.gitbook/assets/image-\(3330\).png)

Next, click the green tick to save your changes.

![Clicking the green tick](../../../.gitbook/assets/image-\(3331\).png)

The **Code type** field is updated.

!['Code type' field updated.](../../../.gitbook/assets/image-\(3332\).png)

### Delete a Return Code

If you do not want to delete a Return Code, go to [Next Steps](custom-apps-configuration-tab.md#next-steps).

![Deleting a Return Code](../../../.gitbook/assets/image-\(3333\).png)

To delete a Return Code, click the red trash can beside the relevant code.

The code is deleted from the list.

![Code deleted from the list](../../../.gitbook/assets/image-\(3334\).png)

## App Info

The **App Info** section enables you to define default values for items that will be included in the app’s metadata when it is packaged to Intune. Any values set for the following items will appear in the app’s properties when viewed in the Intune admin center:

* **Owner –** The name of the owner of this app.
* **Intune Notes –** Notes about the app that we send to Intune when we create a deployment.
* **Information URL -** Link to a website or documentation that has more information about the app.
* **Privacy URL -** A link for people who want to learn more about the app's privacy settings and terms
* **Developer –** The name/contact details of the developer as this is a plain text field.

![‘App Info' section](../../../.gitbook/assets/image-\(3615\).png)

## Next Steps

If you want to configure Native Detection Rules for this app, click **Next** to go to the [Detection Rules](custom-apps-detection-rules-tab.md) tab.\
\
If you do not want to configure Native Detection Rules, click **Next** twice to go to the [Summary ](custom-apps-summary-tab.md)tab.

# Using Post-Uninstall Scripts in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

A _Post-Uninstall Script_ is a script that can be run after the uninstaller runs.

To add a Post-Uninstall script:

1. Click **Add** beside the **Post-Uninstall** option.

![Clicking "Add" beside the "Post-Uninstall" option](../../../../../../.gitbook/assets/image-\(3310\).png)

The **Add Pre-Install Script** page is shown, highlighting that the default **Script Format** is **.ps1**, with built-in support for PSADT functions.

2. To import an existing script, click **Import,** then browse to the location containing the script and select it.

![Clicking "Import" to import an existing script](<../../../../../../.gitbook/assets/image-(53) (1).png>)

The **Script Name** field is populated with the filename of the script selected, and the **Add Post-Uninstall Scripts** page is populated with the imported script.

!['Add Post-Uninstall Script' page is populated with the imported script.](<../../../../../../.gitbook/assets/image-(54) (1).png>)

3. To manually add a script, enter a unique name for the script in the **Script Name** field.

![Entering a unique name for the script in the 'Script Name' field](<../../../../../../.gitbook/assets/image-(55) (1).png>)

4. Select the type of script from the **Script Format** dropdown.

![Selecting the type of script from the 'Script Format' dropdown.](<../../../../../../.gitbook/assets/image-(56) (1).png>)

5. In the script editor, type your script.

![Typing your script in the Script Editor](<../../../../../../.gitbook/assets/image-(57) (1).png>)

> \*\*Note\*\*
>
> We currently have a limit of 50,000 characters per script. Use the \*\*Number of characters used\*\* counter to keep track of the number of characters you’ve entered in the script editor.
>
> If PSADT commands are detected in the Script Editor, the \*\*Script Format\*\* field is updated to show \*\*.ps1 +\*\* the PSADT logo.
>
> !\[]\(/\_images/image-(4371).png>)

> \*\*Tip\*\*
>
> Under the script editor, we include example syntax to help you understand the required syntax for referencing any additional files you've uploaded, which updates depending on the \*\*Script Format\*\* selected.

6. In the **Arguments** field, enter any arguments you want to provide to the script.

![Entering any arguments you want to provide to the script by specifying them in the 'Arguments' field](<../../../../../../.gitbook/assets/image-(58) (1).png>)

> \*\*Tip\*\*
>
> You can use variable names as arguments, provided they are enclosed by percentage signs (\`%\`). We provide common variables under this field, which you can add by clicking the plus (\`+\`) symbol or relevant variable name.
>
> \`%ReturnCode%\` is currently only supported on post-scripts.

> \*\*Important\*\*
>
> Using script Arguments is currently unsupported when deploying an app to macOS.
>
> Also, if you add any PSADT scripts to your deployments, you need to ensure .NET version 4.7.2 is installed on any devices to which this app will be deployed.

7. Click **Save** to save your script.

![Clicking 'Save' to save your script](<../../../../../../.gitbook/assets/image-(59) (1).png>)

The **Configurations** tab is re-displayed with the name of the configured script beside it.

!["Configurations" tab re-displayed with the name of the configured script beside it](<../../../../../../.gitbook/assets/image-(798) (1).png>)

> \*\*Tip\*\*
>
> You can click \*\*Edit\*\* to edit a script or its settings. You can also click the red “\`x\`” beside a script to delete it.

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.

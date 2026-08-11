# Configure Scripts in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

> \*\*Note\*\*
>
> Using the \*\*Scripts\*\* tool is optional. However, if you deploy a Custom App where the \*\*Installer Type\*\* is set to \*\*Installation Script\*\*, the \*\*Scripts\*\* tool is automatically added to your deployment. See the \[Deploying Scripted Custom Apps]\(./#deploying-scripted-custom-apps) section in this article for more information.

The **Scripts** tool in the Patch My PC (PMPC) Cloud deployment wizard allows you to configure settings for install and uninstall scripts.

This includes regular PowerShell (.ps1) scripts as well as PSADT scripts, which can be specified directly in our Portal without having to upload the required PSADT module files separately.

> \*\*Note\*\*
>
> Although we support both PSADT v3 and V4, we recommend using V4 whenever possible.
>
> Also:
>
> \* Scripts will be run in the same context as the application.
>
> \* Each install script is limited to 1 MB per script, with a total size limit of 4 MB for all scripts.
>
> \* There is a limit of 50,000 characters per script.
>
> We currently support the following script types:
>
> \* .BAT
>
> \* .CMD
>
> \* .PS1
>
> \* .VBS

> \*\*Important\*\*
>
> Currently, scripts containing \`"${env:ProgramFiles(x86)}"\` or \`"${env:ProgramFiles}"\` cannot be uploaded as Cloudflare is falsely identifying them as a false positive related to Log4j exploits. We are actively working with them to resolve this, but as this is outside our control, we cannot provide an estimated resolution time.
>
> To work around this issue, see the \[Resolution]\(../../../../../troubleshoot/deployments/typeerror-failed-to-fetch-error-when-trying-to-upload-a-pre-or-post-script-in-cloud.md#resolution) section of \["TypeError: Failed to fetch" error when trying to upload a Pre or Post Script]\(../../../../../troubleshoot/deployments/typeerror-failed-to-fetch-error-when-trying-to-upload-a-pre-or-post-script-in-cloud.md).

To add a script:

1. Add the [**Scripts** tool](../../#adding-additional-tools).
2. Click the **Scripts** tool.

![Clicking the 'Scripts' tool](/_images/image-(3637).png)

> \*\*Note\*\*
>
> If the app includes our recommended scripts, you will see the \*\*Customer Scripts | PMPC Scripts\*\* toggle shown above the \*\*Install Scripts\*\* section.
>
> See \[PMPC Scripts]\(../../../../technical-references/use-pmpc-scripts.md) for more details on the options you have for managing these scripts.

3. Click **Add** beside the relevant script option to add a script, then configure the required settings as per the relevant articles:

* [Pre-Install Script](pre-install-scripts.md) - a script that can be run before the installer runs.
* [Post-Install Script](post-install-scripts.md) - a script that can be run after the installer runs.
* [Pre-Uninstall Script](pre-uninstall-scripts.md) - a script that can be run before the uninstaller runs.
* [Post-Uninstall Script](post-uninstall-scripts.md) - a script that can be run after the uninstaller runs.

!['Scripts' tool settings](/_images/image-(4222).png)

> \*\*Note\*\*
>
> If you upload \[Extra Files]\(../extra-files.md) as part of your Patch My PC (PMPC) Cloud Deployment, you can reference those files in any of the \[Scripts]\(./) in the same deployment by building a path relative to the script's current location. See \[Referencing Extra Files in Scripts]\(../../../../technical-references/reference-external-scripts.md) for more information.
>
> Also, if any PSADT commands are detected in any of the scripts configured in the \*\*Scripts\*\* section, a warning is displayed about ensuring that any devices to which this deployment is assigned have at least .NET Framework 4.7.2 installed.
>
> !\[PSADT warning]\(/\_images/image-(4223 "PSADT warning").png>)
>
> If this warning appears, check the \*\*Enable PSADT Module\*\* checkbox (available only if PSADT commands are detected), which will ensure the PSADT Toolkit is uploaded to Intune when this deployment is created.
>
> If this warning is not displayed, you should not check the \*\*Enable PSADT Module\*\* checkbox.

> \*\*Important\*\*
>
> Checking the \*\*Enable PSADT Module\*\* checkbox causes the following behaviors:
>
> \* When \[creating a deployment]\(../../../):
>
> \* If a PSADT script is included and you have not manually interacted with the checkbox, it will be \*\*automatically enabled\*\*.
>
> \* If you manually change the checkbox state, your selection will be preserved.
>
> \* When \[editing a deployment]\(../../../../manage-deployments/edit.md):
>
> \* The checkbox is treated as \*\*manually configured\*\*, and its state will not be automatically changed.
>
> \* If a PSADT script is added during edit, the checkbox will \*\*not be auto-enabled\*\* and must be adjusted manually if needed.

## Deploying Scripted Custom Apps

As previously mentioned, if you deploy a Custom App where the **Installer Type** is set to **Installation Script**, the **Scripts** tool is automatically added to your deployment.

The **Scripts** tool will also show the **Install File** and **Uninstall Command** fields. Clicking **View** next to these fields opens the Script Editor, which displays the associated script (this is read-only, so you cannot make any changes).

![Script tool showing the install and uninstall scripts](/_images/image-(4367).png)

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.
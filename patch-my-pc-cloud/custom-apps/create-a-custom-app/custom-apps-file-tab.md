# Custom Apps "File" tab

_Applies to: Patch My PC Cloud Custom Apps_

The **File** tab of the Patch My PC (PMPC) Cloud Custom Apps Deployment wizard lets you configure various settings for the Custom App you are creating.

To configure the **File** tab:

1. Select the relevant type of installer for this Custom App:
   1. **Installer File –** Select this option (selected by default) if the installation will be based on an installer file. Proceed to the [Add the Primary Install File](custom-apps-file-tab.md#add-the-primary-install-file) section.
   2. **Installation Script –** If the installation will be controlled based on a script, select this item and proceed to the [Add the Installation Script](custom-apps-file-tab.md#add-the-installation-script) section.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Changing the **Install Method** will reset all of the settings in the Custom Apps Deployment Wizard.</p>
</blockquote>

!['Install Method' section](/_images/image-(4492).png "&#x27;Install Method&#x27; section")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Scripts will be run in the same context as the application.</p>
<p>Also, we currently support the following script types:</p>
<p>* .BAT</p>
<p>* .CMD</p>
<p>* .PS1</p>
<p>* .VBS</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Currently, Pre and Post scripts containing "`${env:ProgramFiles(x86)}`" or "${env:ProgramFiles}" cannot be uploaded as Cloudflare is falsely identifying them as a false positive related to Log4j exploits. We are actively working with them to resolve this, but as this is outside our control, we cannot provide an estimated resolution time.</p>
<p>To work around this issue, see the [Resolution](../../troubleshoot/deployments/typeerror-failed-to-fetch-error-when-trying-to-upload-a-pre-or-post-script-in-cloud.md#resolution) section of ["TypeError: Failed to fetch" error when trying to upload a Pre or Post Script](../../troubleshoot/deployments/typeerror-failed-to-fetch-error-when-trying-to-upload-a-pre-or-post-script-in-cloud.md).&#x20;</p>
</blockquote>

## Add the Primary Install File

To add the primary installer for a Custom App:

1. On the **File** page, either:
   1. Click **Add Primary Install File** and browse to the location containing the app’s installer (EXE or MSI).
   2. Drag and drop the installer file onto this page.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>We do not support macOS in Custom Apps. If you select a .pkg/.dmg you will see a warning stating this and explaining how you can upvote this idea.</p>
</blockquote>

![Clicking ‘Add Primary Install File'](/_images/image-(4493).png "Clicking ‘Add Primary Install File’")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you plan to deploy an EXE-based installer, use our free script to help you extract the required information from the registry. See [Finding properties for EXE-Based Installers](../custom-apps-reference/find-properties-for-exe-based-installers.md) for more information.</p>
</blockquote>

The hash for the file is calculated as it is uploaded to your Cloud Portal and will appear as completed once the upload has finished.

![Uploading the installer](/_images/image-(4494).png "Uploading the installer")

2. If the installer does not require any additional folders or files, click **Next** to go to the [General Information](custom-apps-general-information-tab.md) tab. \
   \
   If the installer does require additional folders or files, go to [Add Extra Folders and Files](custom-apps-file-tab.md#add-extra-folders-and-files) .

## Add the Installation Script

To use an installation script to install the app, from the Script section, choose how you are going to add the script:

* [Import a Script](custom-apps-file-tab.md#import-a-script)
* [Add a Script Manually](custom-apps-file-tab.md#add-a-script-manually)

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>It is currently unsupported to deploy a Custom App created using the **Installation Script** option via our On-Premises Publisher.</p>
</blockquote>

### Import a Script

To import an existing script:

1. Click **Import Script** and browse to the location containing the script and select it.

![Clicking ‘Import Script'](/_images/image-(4495).png "Clicking ‘Import Script’")

The **App Installation Script** editor appears with the **Script Name** and **Script Format** fields automatically populated, and the script editor is populated with the imported script.

![‘App Installation Script'](/_images/image-(4304).png "‘App Installation Script’")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If the script you are importing contains PSADT commands, we automatically detect this and update the **Script Format** to **PowerShell + PSADT**.</p>
<p>![](/_images/image-(4305).png)</p>
<p>Also, as the warning at the bottom of the script editor tells you, we do not sign scripts. If you want this script to be signed, click the **How to sign a script** link for a walkthrough.</p>
</blockquote>

2. Click **Save** to save the script and return to the **File** tab, where details of the script appear under the **Script** section.

![Script details](/_images/image-(4496).png "Script details")

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If the script you imported contains PSADT commands, you will see the following warning under the **Script** section :</p>
<p>**PSADT functions were detected. Please ensure .NET Framework 4.7.2 or greater is installed on your device.**</p>
<p>As the warning states, you should ensure that .NET Framework 4.7.2 (or later) is installed on any devices to which this app will be deployed, so that it installs and functions correctly.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can edit the script by clicking the pencil icon or delete it by clicking the trash can.</p>
</blockquote>

3. If the installer does not require any additional folders or files, click **Next** to go to the [General Information](custom-apps-general-information-tab.md) tab. \
   \
   If the installer does require additional folders or files, go to [Add Extra Folders and Files](custom-apps-file-tab.md#add-extra-folders-and-files).

### Add a Script Manually&#x20;

To manually add a script:

1. Click **Add Manually**

![Clicking 'Add Manually'](/_images/image-(4497).png "Clicking &#x27;Add Manually&#x27;")

The **App Installation Script** editor appears, prefilled with some values.

![‘App Installation Script' editor](/_images/image-(4308).png "‘App Installation Script’ editor")

2. If required, change the:
   1. Name of the script in the **Script Name** field.
   2. Type of script from the **Script Format** dropdown.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can also click **Import** to import an existing script.</p>
</blockquote>

3. In the script editor, type your script, then click **Save**

![Entering a script and clicking ‘Save'](/_images/image-(4309).png "Entering a script and clicking ‘Save’")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If the enter any PSADT commands in the script editor, we automatically detect this and update the **Script Format** to **PowerShell + PSADT**.</p>
<p>![](/_images/image-(4305).png)</p>
<p>Also, as the warning at the bottom of the script editor tells you, we do not sign scripts. If you want this script to be signed, click the **How to sign a script** link for a walkthrough.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can also click **Export** to export this script to an external file.</p>
</blockquote>

The **File** tab is redisplayed, showing details of the script under the **Script** section.

![Script details](/_images/image-(4498).png "Script details")

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If your script contains PSADT commands, you will see the following warning under the **Script** section :</p>
<p>**PSADT functions were detected. Please ensure .NET Framework 4.7.2 or greater is installed on your device.**</p>
<p>As the warning states, you should ensure that .NET Framework 4.7.2 (or later) is installed on any devices to which this app will be deployed, so that it installs and functions correctly.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can edit the script by clicking the pencil icon or delete it by clicking the trash can.</p>
</blockquote>

4. If the installer does not require any additional folders or files, click **Next** to go to the [General Information](custom-apps-general-information-tab.md) tab. \
   \
   If the installer does require additional folders or files, go to [Add Extra Folders and Files](custom-apps-file-tab.md#add-extra-folders-and-files).

## Add Extra Folders and Files

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Configuring Extra Folders and Files is optional, and the process is the same regardless of the **Installer Type** selected.</p>
</blockquote>

If the installer requires additional folders or files, either:

1.  Click **Add Folder** or **Add Files** and browse to the location containing the additional folders/files\
    \
    _&#x4F;R_<br>

    Drag and drop the folders/files onto this page.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If you add any PSADT scripts to your Custom App, you need to ensure that .NET version 4.7.2 is installed on any devices to which this Custom App is deployed.</p>
</blockquote>

![Adding files or folders](/_images/image-(4499).png "Adding files or folders")

2. Click **Next** to move to the [General Information](custom-apps-general-information-tab.md) tab.

![Clicking 'Next' to move to the 'General Information' tab](/_images/image-(4500).png "Clicking &#x27;Next&#x27; to move to the &#x27;General Information&#x27; tab")
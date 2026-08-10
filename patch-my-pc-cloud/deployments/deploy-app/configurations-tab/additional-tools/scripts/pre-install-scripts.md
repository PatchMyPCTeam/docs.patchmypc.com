# Using Pre-Install Scripts in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

A _Pre-Install Script_ is a script that can be run before the installer runs.

To add a Pre-Install script:

1. Click **Add** beside the **Pre-Install** option.

![Clicking "Add" beside the "Pre-Install" option](/_images/image-(3307).png "Clicking “Add” beside the “Pre-Install” option")

The **Add Pre-Install Script** page is shown, highlighting that the default **Script Format** is **.ps1**, with built-in support for PSADT functions.&#x20;

!['Add Pre-Install Script' page highlighting that the default Script Format is .ps1, with built-in support for PSADT functions.](/_images/image-(4248).png "&#x27;Add Pre-Install Script&#x27; page highlighting that the default Script Format is .ps1, with built-in support for PSADT functions.")

2. To import an existing script, click **Import,** then browse to the location containing the script and select it.

![Clicking 'Import' to import an existing script](/_images/image-(4189).png "Clicking &#x27;Import&#x27; to import an existing script")

The **Script Name** field is populated with the filename of the script selected, and the **Add Pre-Install Script** page is populated with the imported script.

![The 'Add Pre-Install Script' page is populated with the imported script.](/_images/image-(4190).png "The &#x27;Add Pre-Install Script&#x27; page is populated with the imported script.")

3. To manually add a script, enter a unique name for the script in the **Script Name** field.

![Entering a unique name for the script in the 'Script Name' field](/_images/image-(4191).png "Entering a unique name for the script in the &#x27;Script Name&#x27; field")

4. Select the type of script from the **Script Format** dropdown.

![Selecting the type of script from the 'Script Format' dropdown.](/_images/image-(4192).png "Selecting the type of script from the &#x27;Script Format&#x27; dropdown.")

5. In the script editor, type your script.

![Typing your script in the Script Editor](/_images/image-(4193).png "Typing your script in the Script Editor")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>We currently have a limit of 50,000 characters per script. Use the **Number of characters used** counter to keep track of the number of characters you’ve entered in the script editor.</p>
<p>If PSADT commands are detected in the Script Editor, the **Script Format** field is updated to show **.ps1 +** the PSADT logo.</p>
<p>![Script Format modified to show .ps1 and PSADT logo](/_images/image-(4368 "Script Format modified to show .ps1 and PSADT logo").png>)</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Under the script editor, we include example syntax to help you understand the required syntax for referencing any additional files you've uploaded, which updates depending on the **Script Format** selected.&#x20;</p>
</blockquote>

6. In the **Arguments** field, enter any arguments you want to provide to the script.

![Entering any arguments you want to provide to the script by specifying them in the 'Arguments' field](/_images/image-(4196).png "Entering any arguments you want to provide to the script by specifying them in the &#x27;Arguments&#x27; field")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can use variable names as arguments, provided they are enclosed by percentage signs (`%`). We provide common variables under this field, which you can add by clicking the plus (+) symbol or relevant variable name.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Using script Arguments is currently unsupported when deploying an app to macOS.</p>
<p>Also, if you add any PSADT scripts to your deployments, you need to ensure .NET version 4.7.2 is installed on any devices to which this app will be deployed.</p>
</blockquote>

7.  Check the **Don’t attempt software update if the pre-script returns an exit code other than 0 or 3010** checkbox if you don’t want the app to be installed if the pre-script returns an exit code other than **0** or **3010**.<br>

    If you do not check this checkbox, we will attempt to install the app regardless of the exit code returned by the pre-install script.

![Checking the 'Don't attempt software update if the pre script returns an exit code other than 0 or 3010' checkbox](/_images/image-(4197).png "Checking the &#x27;Don’t attempt software update if the pre script returns an exit code other than 0 or 3010&#x27; checkbox")

8. Check the **Run the pre-update script before performing any auto-close or skip process checks** checkbox if you want to run the pre-install script before the conflicting process notification is displayed (if relevant).\
   \
   If you do not check this checkbox, we will run the pre-install script after the conflicting process notification.

![Checking the 'Run the pre-update script before performing any auto-close or skip process checks' checkbox](/_images/image-(4198).png "Checking the &#x27;Run the pre-update script before performing any auto-close or skip process checks&#x27; checkbox")

9. Click **Save** to save your script.

![Clicking 'Save' to save your script.](/_images/image-(4199).png "Clicking &#x27;Save&#x27; to save your script.")

The **Configurations** tab is re-displayed with the name of the configured script beside it.

!["Configurations" tab re-displayed with the name of the configured script beside it](/_images/image-(795).png "“Configurations” tab re-displayed with the name of the configured script beside it")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can click **Edit** to edit a script or its settings. You can also click the red “`x`” beside a script to delete it.</p>
</blockquote>

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.
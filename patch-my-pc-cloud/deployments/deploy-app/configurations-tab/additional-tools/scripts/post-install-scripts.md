# Using Post-Install Scripts in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

A _Post-Install Script_ is a script that can be run after the installer runs.

To add a **Post-Install** script:

1. Click **Add** beside the **Post-Install** option.

![Clicking "Add" beside the "Post-Install" option](/_images/image-(3308).png "Clicking “Add” beside the “Post-Install” option")

The **Add Pre-Install Script** page is shown, highlighting that the default **Script Format** is **.ps1**, with built-in support for PSADT functions.&#x20;

2. To import an existing script, click **Import**, browse to the location containing the script, and select it.

![Clicking 'Import' to import an existing script](/_images/image-(37).png "Clicking &#x27;Import&#x27; to import an existing script")

The **Script Name** field is populated with the filename of the script selected, and the **Add Post-Install Script** page is populated with the imported script.

!['Add Post-Install Script' page is populated with the imported script.](/_images/image-(38).png "&#x27;Add Post-Install Script&#x27; page is populated with the imported script.")

3. To manually add a script, enter a unique name for the script in the **Script Name** field.

![Entering a unique name for the script in the 'Script Name' field](/_images/image-(39).png "Entering a unique name for the script in the &#x27;Script Name&#x27; field")

4. Select the type of script from the **Script Format** dropdown.

![Selecting the type of script from the 'Script Format' dropdown.](/_images/image-(40).png "Selecting the type of script from the &#x27;Script Format&#x27; dropdown.")

5. In the script editor, type your script.

![Typing your script in the Script Editor](/_images/image-(41).png "Typing your script in the Script Editor")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>We currently have a limit of 50,000 characters per script. Use the **Number of characters used** counter to keep track of the number of characters you’ve entered in the script editor.</p>
<p>If PSADT commands are detected in the Script Editor, the **Script Format** field is updated to show **.ps1 +** the PSADT logo.</p>
<p>![](/_images/image-(4369).png>)</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Under the script editor, we include example syntax to help you understand the required syntax for referencing any additional files you've uploaded, which updates depending on the **Script Format** selected.&#x20;</p>
</blockquote>

6. In the **Arguments** field, enter any arguments you want to provide to the script.

![Entering any arguments you want to provide to the script by specifying them in the 'Arguments' field](/_images/image-(42).png "Entering any arguments you want to provide to the script by specifying them in the &#x27;Arguments&#x27; field")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can use variable names as arguments, provided they are enclosed by percentage signs (`%`). We provide common variables under this field, which you can add by clicking the plus (`+`) symbol or relevant variable name.</p>
<p>&#x20;`%ReturnCode%` is currently only supported on post-scripts.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Using script Arguments is currently unsupported when deploying an app to macOS.</p>
<p>Also, if you add any PSADT scripts to your deployments, you need to ensure .NET version 4.7.2 is installed on any devices to which this app will be deployed.</p>
</blockquote>

7. Click **Save** to save your script.

![Clicking 'Save' to save your script](/_images/image-(43).png "Clicking &#x27;Save&#x27; to save your script")

The **Configurations** tab is re-displayed with the name of the configured script beside it.

!["Configurations" tab re-displayed with the name of the configured script beside it](/_images/image-(796).png "“Configurations” tab re-displayed with the name of the configured script beside it")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can click **Edit** to edit a script or its settings. You can also click the red “`x`” beside a script to delete it.</p>
</blockquote>

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.
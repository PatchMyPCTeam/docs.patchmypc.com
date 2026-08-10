# Custom Apps "Detection Rules" tab

_Applies to: Patch My PC Cloud Custom Apps_

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Configuring Native Detection Rules is optional.</p>
</blockquote>

If you want to configure Native Detection Rules:

1. On the **Detection Rules** tab, click **Use Custom** to use a custom detection rule, then choose the relevant type of rule from the **Rule Type** dropdown.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You should only choose to use a custom detection method if our default method of scanning the uninstall registry on the endpoint to find a **Display Name** matching your **Apps & Features Name** entry and a **Display Version** that meets or exceeds the **Version** in the **Configuration** tab is unsuitable for this app.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If you configure Detection Rules in the PMPC Cloud portal you:</p>
<p>* Cannot deploy the same app in Publisher as Publisher does not support Native Detection Rules.</p>
<p>* Should not create and manage detection rules in the Intune admin center as they will not be detected and shown in the PMPC Cloud portal.</p>
<p>* Cannot mix our default detection method with custom detection methods for the same Custom App.</p>
</blockquote>

![Clicking 'Use Custom' to use a custom detection rule and choosing the relevant type of rule from the 'Rule Type' dropdown](/_images/image-(3543).png "Clicking &#x27;Use Custom&#x27; to use a custom detection rule and choosing the relevant type of rule from the &#x27;Rule Type&#x27; dropdown")

2. Go to Step 8 if you chose the **Use Custom Script** option.
3. If you choose the **Configure Manually** option, click **Add Rule**.

![Clicking 'Add Rule'](/_images/image-(3544).png "Clicking &#x27;Add Rule&#x27;")

4. On the **Add Detection Rule** screen, select the relevant type of rule from the **Rule Type** dropdown, then configure the required options as required.

![Selecting the relevant type of rule to configure from the 'Rule Type' dropdown](/_images/image-(901).png "Selecting the relevant type of rule to configure from the &#x27;Rule Type&#x27; dropdown")

<table><thead><tr><th width="99.111083984375">Rule Type</th><th>Available Options</th></tr></thead><tbody><tr><td>File</td><td><p><strong>Path –</strong> The path to the folder you are checking for</p><p><strong>File or Folder –</strong> The folder containing the file you are checking for</p><p><strong>Detection Method –</strong> Choose from the list of available checks.</p></td></tr><tr><td>MSI</td><td><p><strong>MSI Product Code –</strong> This is the MSI product code extracted from the file you imported.</p><p><strong>MSI Product Version Check (optional)</strong> – Click this slider to enable this check for a specific version number that matches the options you configure in the <strong>Operator</strong> and <strong>Value</strong> fields.</p></td></tr><tr><td>Registry</td><td><p><strong>Key Path –</strong> The path to the Registry key</p><p><strong>Value name (optional) –</strong> The name of a value contained within the specified <strong>Key Path</strong> that you want to check for</p><p><strong>Detection Method –</strong> Choose from the list of available checks.</p></td></tr></tbody></table>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You can only create up to a maximum of 25 rules of all types per deployment. Of these 25, only one can be an MSI detection rule and the rest can be a mixture of **File** and **Registry** rules.</p>
<p>See the following Microsoft resources for more information:</p>
<p>* <a href="https://learn.microsoft.com/en-us/graph/api/resources/intune-apps-win32lobappfilesystemrule?view=graph-rest-1.0">win32LobAppFileSystemRule resource type</a></p>
<p>* <a href="https://learn.microsoft.com/en-us/graph/api/resources/intune-apps-win32lobapppowershellscriptrule?view=graph-rest-1.0">win32LobAppPowerShellScriptRule resource type</a></p>
<p>* <a href="https://learn.microsoft.com/en-us/graph/api/resources/intune-apps-win32lobappproductcoderule?view=graph-rest-1.0">win32LobAppProductCodeRule resource type</a></p>
<p>* <a href="https://learn.microsoft.com/en-us/graph/api/resources/intune-apps-win32lobappregistryrule?view=graph-rest-1.0">win32LobAppRegistryRule resource type</a></p>
</blockquote>

5.  If you have created either a **File** or **Registry** detection rule, click the **Associated with a 32-bit app on 64-bit clients** slider to enable it to expand any path environment variables in the 32-bit context on 64-bit endpoints.<br>

    ![Enabling the 'Associated with a 32-bit app on 64-bit clients' slider](/_images/image-(902).png "Enabling the &#x27;Associated with a 32-bit app on 64-bit clients&#x27; slider")


6.  Click **Add Rule** to add the rule.<br>

    ![Clicking 'Add Rule' to add a rule](/_images/image-(903).png "Clicking &#x27;Add Rule&#x27; to add a rule")

    \
    The rule is added to the list of detection rules.

![Rule is added to the list of rules](/_images/image-(3545).png "Rule is added to the list of rules")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You can:</p>
<p>* Edit a Detection Rule by clicking the pencil icon beside the relevant rule, making the required changes then clicking **Save rule** to save the changes.</p>
<p>* Delete a Detection rule by clicking the red trashcan beside the relevant rule to remove it from the list of rules.</p>
</blockquote>

7. Go to step 10 if you do not want to add a detection rule that uses the **Use Custom Script** option.
8. If you choose the **Use Custom Script** option, click **Import Script**, then browse to and select the relevant script you want to import.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>In the current version:</p>
<p>* We only support PowerShell (.ps1) scripts</p>
<p>* You can only import a single script</p>
<p>* We do not sign your scripts if we use them in one of our deployments. If this is a requirement, you will need to sign the scripts yourself.</p>
</blockquote>

![Clicking 'Import Script'](/_images/image-(3546).png "Clicking &#x27;Import Script&#x27;")

A preview of the script is shown in the **Script Preview** window.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You cannot edit the script in the **Script Preview** window.</p>
</blockquote>

![Preview of the script shown in the 'Script Preview' window.](/_images/image-(3547).png "Preview of the script shown in the &#x27;Script Preview&#x27; window.")

9. Click the **Associated with a 32-bit app on 64-bit clients** slider to enable it to expand any path environment variables in the 32-bit context on 64-bit endpoints.

![Enabling the 'Associated with a 32-bit app on 64-bit clients' slider](/_images/image-(3548).png "Enabling the &#x27;Associated with a 32-bit app on 64-bit clients&#x27; slider")

10. Repeat the steps in this section to add any additional detection rules.
11. If you are happy you have entered all of the details for the app correctly, click **Create** to complete the creation of the Custom App.\
    \
    However, we recommend you click **Next** to move to the [Summary](custom-apps-summary-tab.md) tab where you can  verify the configuration before saving the Custom App.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You can use the [Check Detection Rules](../../technical-references/intune-reference/check-detection-rules-in-intune.md) process to verify your detection rules have been successfully created in Intune by PMPC Cloud.</p>
</blockquote>
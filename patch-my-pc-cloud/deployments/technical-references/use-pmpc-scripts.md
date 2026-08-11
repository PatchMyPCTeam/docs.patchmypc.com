# Use Patch My PC Scripts in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

For certain applications in the Patch My PC (PMPC) App Catalog, we include scripts to enhance the installation and configuration of the app, based on our experience. By default, if an app includes one of our recommended scripts, these are automatically executed at the time the app is installed.

However, this default behavior can cause issues for some customers who are not aware of the scripts and their contents.

To give you better visibility and to allow you to customize the deployment process, for those apps that include our recommended scripts, you will now see the **Customer Scripts | PMPC Scripts** toggle on the **Scripts** tool page of the **Configurations** tab of the PMPC Cloud Deployment Wizard.

<figure><img src="../../../.gitbook/assets/image (3432).png" alt="“Customer Scripts | PMPC Scripts” toggle" width="563"><figcaption></figcaption></figure>

Contrast this to an app that does not include any recommended scripts.

<figure><img src="../../../.gitbook/assets/image (3433).png" alt="App without the “Customer Scripts | PMPC Scripts” toggle" width="563"><figcaption></figcaption></figure>

Using this feature allows you to:

* [View PMPC Scripts](use-pmpc-scripts.md#viewing-pmpc-scripts)
* [Disable a PMPC Script](use-pmpc-scripts.md#disable-a-pmpc-script)
* [Enable a PMPC Script](use-pmpc-scripts.md#enable-a-pmpc-script)

## View PMPC Scripts

To view the PMPC scripts, click the PMPC Scripts toggle.

<figure><img src="../../../.gitbook/assets/image (3434).png" alt="Clicking “PMPC Scripts”" width="563"><figcaption></figcaption></figure>

Any recommended scripts included with the app are shown.

<figure><img src="../../../.gitbook/assets/image (3435).png" alt="Recommended PMPC Scripts" width="563"><figcaption></figcaption></figure>

Once you have clicked PMPC Scripts, you can:

* Hover over the script’s name to see its location.
* Click the script, which will open it in a new browser tab so you can see its contents.
* Click **Edit** to open the script in the relevant script editor window.

<figure><img src="../../../.gitbook/assets/image (3436).png" alt="Script editor window" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

In the current release, you cannot modify the script’s name, format, contents, or arguments. You can disable the script as detailed in [Disable a PMPC Script](use-pmpc-scripts.md#disable-a-pmpc-script).
{% endhint %}

## Disable a PMPC Script

If you do not want to use our recommended scripts in your deployments, you can disable them (although we’d recommend you do not do this unless you have a genuine reason for doing so).

To disable a PMPC script:

1. Either [deploy ](../deploy-app/)or [edit an existing deployment](../manage-deployments/edit.md) for the relevant app.
2. Navigate to the **Configurations** tab.

<figure><img src="../../../.gitbook/assets/image (3437).png" alt="Navigating to the “Configurations” tab" width="563"><figcaption></figcaption></figure>

3. Click the **Scripts** tool if it is not already selected.

<figure><img src="../../../.gitbook/assets/image (3438).png" alt="Clicking the “Scripts” tool" width="563"><figcaption></figcaption></figure>

4. Click **PMPC Scripts**

<figure><img src="../../../.gitbook/assets/image (3439).png" alt="Clicking “PMPC Scripts”" width="563"><figcaption></figcaption></figure>

5. Click **Edit** beside the relevant script.

<figure><img src="../../../.gitbook/assets/image (3440).png" alt="Clicking “Edit” beside the relevant script" width="563"><figcaption></figcaption></figure>

6. If the app includes a recommended Post-Install script, go to Step 9.
7. If the app includes a recommended Pre-Install script, you have the option of checking either or both of the following checkboxes:
   1. **Don’t attempt software update if the pre script returns an exit code other than 0 or 3010**
   2. **Disable the Patch My PC Recommended Pre-Install scripts for this product**

<figure><img src="../../../.gitbook/assets/image (3441).png" alt="Checking the required “Pre-install checkboxes." width="563"><figcaption></figcaption></figure>

8. Go to Step 10.
9. If the app includes a recommended Post-Install script, check the **Disable the Patch My PC Recommended Post-Install scripts for this product** checkbox.

<figure><img src="../../../.gitbook/assets/image (3442).png" alt="Checking the “Disable the Patch My PC Recommended Post-Install for this product” checkbox" width="563"><figcaption></figcaption></figure>

10. Click **Save**

The **Configurations** tab is displayed.

If either a Pre or Post-Install script has been disabled, a red circle is shown beside the script to indicate this and that it will not be included as part of the deployment.

<figure><img src="../../../.gitbook/assets/image (3443).png" alt="Red circle is shown beside the script to indicate this and that it will not be included as part of the deployment." width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Checking the **Don’t attempt software update if the pre script returns an exit code other than 0 or 3010** checkbox for a Pre-Install script does not cause the red circle to be displayed.
{% endhint %}

## Enable a PMPC Script

If you have previously [disabled a PMPC Script](use-pmpc-scripts.md#disable-a-pmpc-script), you can re-enable it by [editing the deployment](../manage-deployments/edit.md) and following the [Disable a PMPC Script](use-pmpc-scripts.md#disable-a-pmpc-script) section, but uncheck the **Disable the Patch My PC Recommended <**_**script\_type**_**> for this product** checkbox.

When you click **Save** to save the deployment, a new deployment will be created that includes the script.

## How new versions are handled

If you create a deployment for an app and disable the PMPC Scripts, when your Sync Schedule runs and creates a new deployment for the new version, we check the existing deployment. If you have disabled any scripts, we will also disable them for the new deployment of the new version.

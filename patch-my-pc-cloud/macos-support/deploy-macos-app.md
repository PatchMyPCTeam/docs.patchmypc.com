# Deploy a macOS app using Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Using Patch My PC (PMPC) Cloud, users can deploy **.DMG** or **.PKG** apps to Intune-managed devices running macOS.

{% hint style="info" %}
**Note**

We currently do not support deploying PMPC Cloud Custom Apps to macOS devices.

We do support deployment templates for macOS as detailed in [Patch My PC Cloud Deployment Templates for macOS](../manage/settings/deployment-templates/macos-templates.md).
{% endhint %}

To deploy a macOS app using Patch My PC (PMPC) Cloud:

1.  Locate the required app on the App Catalog page.<br>

    <figure><img src="../../.gitbook/assets/image (2987).png" alt="Locating the app to be deployed"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

Use the Search field and filters to help you locate the app.
{% endhint %}

2.  Click the relevant app.<br>

    <figure><img src="../../.gitbook/assets/image (2988).png" alt="Clicking the relevant app"><figcaption></figcaption></figure>
3.  On the app’s properties page, click **Deploy** under the **macOS** section to start the Deployment Wizard.<br>

    <figure><img src="../../.gitbook/assets/image (993).png" alt="Clicking “Deploy” under the “macOS” section"><figcaption></figcaption></figure>
4. Continue from [General Information](../deployments/deploy-app/general-information-tab.md) to configure the deployment as required, whilst referring to the [macOS Deployment Specifics](deploy-macos-app.md#macos-deployment-specifics) section below.\
   \
   The first time you deploy a macOS app in your PMPC Cloud company, at the end of the Deployment Wizard, you will see the **This is your first macOS deployment** dialog box, which asks you to confirm that you understand each macOS device you deploy apps to requires its own PMPC Cloud license.

<figure><img src="../../.gitbook/assets/image (700).png" alt="“This is your first macOS deployment” dialog box" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If you do not want macOS devices to count towards your license count, simply do not deploy any macOS apps.
{% endhint %}

{% hint style="success" %}
**Tip**

Once a macOS deployment has been completed successfully, you’ll can see it under **Apps | Monitor | macOS | macOS apps** in the Microsoft Intune admin center.

<img src="../../.gitbook/assets/image (2990).png" alt="Successful deployment visible in the Microsoft Intune admin center" data-size="original">
{% endhint %}

## macOS Deployment Specifics

As Intune handles Windows and macOS apps differently, not all options are available for macOS apps. As Microsoft improves macOS support in Intune, we will endeavor to support any such improvements in PMPC Cloud.

But for now, the following key differences exist:

* **Installer Types (General tab) –** macOS only supports **.dmg**, **.pkg (LOB)**, and **.pkg** installers.
* **Architecture (General tab) –** macOS supports the **Universal** type, which runs on all macOS architectures.
* You cannot add an **Available** assignment and assign it to the built-in **All Devices** group, as Intune currently does not support deploying macOS apps to devices.
* We do not visually identify Line of Business (LOB) apps specifically in our App Catalog.
* Once you've added an Assignment, the following options are unavailable:
  * Availability/Deadline
  * Notifications
  * Content Download.

{% hint style="info" %}
**Note**

See [How to add macOS line-of-business (LOB) apps to Microsoft Intune](https://learn.microsoft.com/en-us/mem/intune/apps/lob-apps-macos) for more details on deploying this type of app with Microsoft Intune.
{% endhint %}

## Create a macOS Deployment

When creating a deployment, the following settings are available for each **Installer Type**.

<table><thead><tr><th width="379.5555419921875" valign="top">Setting</th><th width="92.4444580078125" align="center" valign="top">.dmg</th><th width="79.111083984375" align="center" valign="top">.pkg</th><th width="118" align="center" valign="top">.pkg (LOB) Managed</th><th align="center" valign="top">.pkg (LOB) Unmanaged</th></tr></thead><tbody><tr><td valign="top">Add <strong>Required</strong> assignment?</td><td align="center" valign="top">Yes</td><td align="center" valign="top">Yes</td><td align="center" valign="top">Yes</td><td align="center" valign="top">Yes</td></tr><tr><td valign="top">Add <strong>Available</strong> assignment?</td><td align="center" valign="top">Yes</td><td align="center" valign="top">Yes</td><td align="center" valign="top">Yes</td><td align="center" valign="top">Yes</td></tr><tr><td valign="top">Add an <strong>Add Uninstall</strong> assignment?</td><td align="center" valign="top">Yes</td><td align="center" valign="top">No</td><td align="center" valign="top">Yes*</td><td align="center" valign="top">Yes*</td></tr><tr><td valign="top">Add an <strong>Update Only</strong> assignment?</td><td align="center" valign="top">No</td><td align="center" valign="top">No</td><td align="center" valign="top">No</td><td align="center" valign="top">No</td></tr><tr><td valign="top">Supports Assignment Filters?</td><td align="center" valign="top">No</td><td align="center" valign="top">Yes</td><td align="center" valign="top">Yes</td><td align="center" valign="top">Yes</td></tr><tr><td valign="top">Add <strong>Scripts</strong>?</td><td align="center" valign="top">No</td><td align="center" valign="top">Yes</td><td align="center" valign="top">No</td><td align="center" valign="top">No</td></tr><tr><td valign="top">Supports managed device assignment filters?</td><td align="center" valign="top">N/A</td><td align="center" valign="top">No</td><td align="center" valign="top">Yes***</td><td align="center" valign="top">No</td></tr><tr><td valign="top">Modify the <strong>Uninstall on Unenrollment</strong> setting?</td><td align="center" valign="top">No</td><td align="center" valign="top">No</td><td align="center" valign="top">Yes**</td><td align="center" valign="top">No</td></tr><tr><td valign="top">Modify the <strong>Install App as Managed</strong> setting?</td><td align="center" valign="top">N/A</td><td align="center" valign="top">No</td><td align="center" valign="top">Yes*</td><td align="center" valign="top">No</td></tr></tbody></table>

\* Requires the **Install App as Managed** setting to be enabled, which is enabled by default.

\*\* Only available for the **Required** and **Available** Assignment types and also requires the **Install App as Managed** setting to be enabled (which it is by default).

\*\*\* Managed device filters are only supported for macOS **.pkg (LOB)**. These are not supported for the **.pkg** and **.dmg** installer types.

{% hint style="info" %}
**Note**

This separation ensures that each flow adheres to the correct platform capabilities.

It is supported to switch the **Installer Type** when creating a deployment, but doing so will cause the **Do you want to continue** dialog box to be displayed, warning you that switching will reset all of the values for the deployment.
{% endhint %}

In addition, the following logic is supported for an LOB deployment:

* If the **Install App as Managed** setting on the **Configurations** tab is enabled (by default), on the **Assignments** tab, you can:
  * Add an **Uninstall** assignment
  * Configure the **Uninstall on Enrollment** setting (**On** by default)
  * Add managed device assignment filters.
* If you disable the **Install App as Managed** setting on the **Configurations** tab, although you can still add managed device assignment filters on the **Assignments** tab, you cannot:
  * Add an **Uninstall** assignment
  * Configure the **Uninstall on Enrollment** setting.
* If a deployment has both **Required** and **Uninstall** assignments, you will be unable to disable the **Install App as Managed** setting on the **Configurations** tab without first deleting the **Uninstall** assignment.

## Edit a macOS LOB Deployment

When editing an LOB deployment, you cannot:

* Switch the **Installer Type**, which applies regardless of whether this is a Windows or macOS deployment (if you need to do this, you will need to create a new deployment).
* Change the **Install App as Managed** setting on the **Configurations** tab.

However, when editing an LOB deployment, you can:

* Modify the **Uninstall on Enrollment** setting
* Modify assignment filters
* Add scripts.

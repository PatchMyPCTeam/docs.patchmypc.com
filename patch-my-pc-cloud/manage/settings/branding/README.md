# Manage Branding in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Intune Apps for Patch My PC (PMPC) Cloud lets you configure your company's branding to appear to users whenever software is installed or updated via Manage Conflicting Processes notifications.

Creating a branding app, packages up the settings for Manage Conflicting Processes into its own app, which Intune Apps manages. This application is published to Intune, where it’s deployed to the following location on all of your devices:

```
C:\ProgramData\PatchMyPC\Notification\
```

We currently support two different types of branding:

* Classic (default)
* Modern (PSADT), which supports more localizations and additional settings

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The choice of Branding Type you use is largely up to you. The only differences between them are:</p>
<p>* Modern branding requires .NET Framework 4.7.2 or later to be installed on any devices to which the Modern branding app is assigned.</p>
<p>* Modern branding does not support the **close the application and perform the update** option of the [Conflicting Processes](../../../deployments/deploy-app/configurations-tab/#conflicting-process-settings) **if the timeout expires and no action is taken** setting.</p>
<p>You can use both types of branding in your company; you just can’t have two different branding app types with overlapping assignments</p>
</blockquote>

All branding-related tasks are performed from the **Branding** node of the portal, which is accessed by:

1. Sign in to the PMPC Portal [https://portal.patchmypc.com/](https://portal.patchmypc.com/).
2. Navigate to **Settings | Branding**.

![Navigating to ‘Settings | Branding'](/_images/image-(3718).png "Navigating to ‘Settings | Branding’")

The **Branding** screen is then displayed, allowing you to:

* [Add Branding](add-branding.md)
* [Modify/Recreate Branding](modify-recreate-branding.md)
* [Manage Localizations](localizations.md)
* [Delete Branding](delete-branding.md)
* [Uninstall Branding](uninstall-branding.md)

![‘Branding' screen](/_images/image-(3719).png "‘Branding’ screen")
# Add Branding in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Adding branding to your Patch My PC (PMPC) Cloud company involves:

* [Creating a Branding app](add-branding.md#creating-a-branding-app)
* [Assigning the Branding app to the relevant audience](add-branding.md#assigning-the-branding-app-to-the-relevant-audience)
* [Deploying the Branding app](add-branding.md#deploying-the-branding-app)

## Creating a Branding app

To add a new branding app to your Patch My PC (PMPC) Cloud company:

1. Navigate to **Settings | Branding**

![Navigating to ‘Settings | Branding'](<../../../../.gitbook/assets/image-(545) (1).png>)

2. Click **Add Branding**

![Clicking ‘Add Branding'](<../../../../.gitbook/assets/image-(546) (1).png>)

3. If you want to continue with the default **Classic** branding, go to Step 5.
4. If you want to create modern branding, **click Modern (PSASDT)**

![Clicking ‘Modern(PSASDT)'](<../../../../.gitbook/assets/image-(547) (1).png>)

> \*\*Important\*\*
>
> When you select \*\*Modern (PSADT)\*\*, you will see the \*\*Are you sure you want to switch branding types\*\* prompt.
>
> !\[‘Are you sure you want to switch branding type' prompt]\(/\_images/unknown.png "‘Are you sure you want to switch branding type' prompt")
>
> Click \*\*Confirm\*\* to continue.
>
> You will also see the warning message that .NET Framework 4.7.2 or later is required on any devices on which a Modern branding app is targeted to.
>
> !\[]\(/\_images/unknown-(1).png>)

> \*\*Note\*\*
>
> The process for creating a branding app is the same regardless of the \*\*Branding Type\*\*. The differences are with the configuration settings for each branding app, which are detailed in \[Default Language Notifications in Cloud]\(default-language-notifications.md).

5. In the **Branding Intune App Name** field, type a name for the branding app that will be created in Intune, containing your branding. For example, use the **Branding** prefix followed by the name of the Entra ID group this branding app will be deployed to.

![Entering the name for the Branding app](<../../../../.gitbook/assets/image-(548) (1).png>)

> \*\*Note\*\*
>
> The \*\*Notification Preview\*\* does not update as you change the text in the various fields.

6. In the **Company Name** field, if required, set the name of the company you want to appear on the branding notification when it is displayed on the assigned devices for this branding app. By default, this is the same as the the **Company Name** configured under **Settings | Company | General**.

![Entering your company name](<../../../../.gitbook/assets/image-(549) (1).png>)

7. Click **Upload Logo** to upload the logo for your branding that meets the requirements detailed on the **Branding** screen.

> \*\*Note\*\*
>
> The logo you are uploading must be less than 50 MB.

![Clicking ‘Upload Logo'](<../../../../.gitbook/assets/image-(550) (1).png>)

The selected image is shown on the **Branding** screen and the **Notification Preview** updates to show what the notification will look like when shown on the assigned devices.

![Notification Preview](<../../../../.gitbook/assets/image-(551) (1).png>)

8. Adjust the logo until you are happy.
9. In the **Localizations** section, click the language you want to use to display this branding app on the relevant devices (**English** is selected by default).

![‘Localizations' section](<../../../../.gitbook/assets/image-(552) (1).png>)

> \*\*Note\*\*
>
> Please note the following:
>
> \* Changing the localization does not update the \*\*Notification Preview\*\* to that language.
>
> \* If a device targeted for this branding app is running a language that is configured under the \*\*Localizations\*\* section, the Manage Conflicting Processes notification will be displayed in the configured language.\\
>
> \\
>
> However, if the device’s language is different from that set in the branding app, the default language configured in the branding app will be used to display the notification (the default being \*\*English\*\* unless you change it).
>
> \* You can only have one localization defined as the default per branding app.
>
> \* As ScriptRunner only supports two-letter language codes such as \*\*EN\*\*, \*\*FR\*\*, DE, etc. If the branding app contains a localization for French and the user's device has a system language of \*\*fr-FR\*\*, the user will receive notifications in French. However, if the user's device has the system language \*\*fr-CI\*\* (French in the Ivory Coast), the user will receive notifications in the default language. This is a limitation of ScriptRunner, not PMPC Cloud.

10. If you need to add a localization for this branding, click **Add Language** and follow the [Add a Localization](localizations.md#add-a-localization) section of [Managing Localizations](localizations.md).

![Clicking ‘Add Language'](<../../../../.gitbook/assets/image-(553) (1).png>)

Now, you need to decide who to assign this branding app to.

## Assign the Branding app to the relevant audience

To assign a branding app:

1. Click the **Assignments** tab.

![Clicking the ‘Assignments' tab.](../../../../.gitbook/assets/image-\(3720\).png)

2. Click **Add Assignment**

![Clicking ‘Add Assignment'](../../../../.gitbook/assets/image-\(3721\).png)

3. On the **Add Required Assignment** screen, choose the relevant users/Entra ID security groups to target for this branding app, then click **Save**.

> \*\*Important\*\*
>
> Avoid overlapping assignments between Branding Apps. Deploying multiple Branding Apps to the same groups will produce unwanted behavior.
>
> You should also check that if an Uninstall Branding App exists (it will appear at the top of the list of Branding Apps), that the assignments for it don't overlap with those for the new Branding App you are deploying.

![Choosing the relevant Entra ID security groups to target for this branding app on the 'Add Required Assignment' screen, then clicking 'Save'](../../../../.gitbook/assets/image-\(3121\).png)

The **Assignments** tab is redisplayed, showing all of the assignments for this branding app.

![‘Assignments' tab is redisplayed.](../../../../.gitbook/assets/image-\(3722\).png)

> \*\*Note\*\*
>
> When a branding app is deployed, it overwrites any existing branding app with the same name.
>
> If you deploy multiple branding apps with overlapping assignments, when ScriptRunner executes, it will choose the branding app with the most recent creation/modification date.
>
> For example, branding app A was deployed two months ago, and branding app B was deployed two weeks ago. In this case, branding app B will display the banner.

## Deploy the Branding app

Once you have configured the branding app and added the required assignments, click **Save** to save and deploy the branding.

![Clicking ‘Save'](../../../../.gitbook/assets/image-\(3723\).png)

The **Success – Branding created** notification is displayed, and the Status of the branding app is shown as **In Progress**.

!['Success – Branding created' notification and the 'Status' of the branding app is shown as 'In Progress'](../../../../.gitbook/assets/image-\(3741\).png)

Once the branding app has been successfully deployed, the **Status** field will automatically update to **Success** and the **Last Updated** field will show the last time this branding app was updated.

![‘Status' showing as ‘Success' and the ‘Last Updated' value is updated.](../../../../.gitbook/assets/image-\(3742\).png)

> \*\*Tip\*\*
>
> If you look in the \*\*Events\*\* section, you see a message stating either:
>
> \* \*\*Default Branding <\*\*\_\*\*your\\\_branding\\\_app\\\_name\*\*\_\*\*> Created -\*\* If you used the default out-the-box logo
>
> \* \*\*Custom Branding <\*\*\_\*\*your\\\_branding\\\_app\\\_name\*\*\_\*\*> Created -\*\* If you upload a custom logo.

If you look in the Intune admin center, you will see the branding app listed along with your other apps.

![Branding app listed with all of your other apps](../../../../.gitbook/assets/image-\(3199\).png)

When ScriptRunner runs on your devices, it checks to see if the device has the branding. If it doesn't, ScriptRunner installs it.

Also, if a new branding app includes a device that already has branding deployed to it, the branding on the device will be updated to the new branding app.

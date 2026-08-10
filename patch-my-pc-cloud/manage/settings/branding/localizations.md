# Manage Localizations in Patch My PC Cloud Branding

_Applies to: Patch My PC Cloud_

Using the Branding feature of Patch My PC (PMPC) Cloud, you can customize which localizations are used to display the Manage Conflicting Processes notification on your devices.

> \*\*Note\*\*
>
> The language displayed when the conflicting processes notification appears on devices is determined by the end user's operating system locale:
>
> \* If the system locale matches a configured Branding language, the message will be shown in that language.
>
> \* If the system locale does not match any configured languages, the message will fall back to the default language set by the Cloud Portal Admin.

We recommend you create one branding app per language and then assign this app to the relevant Entra ID Security Groups running the configured language.

Using Branding Apps you can:

* [Add a Localization](localizations.md#add-a-localization)
* [Modify a Localization](localizations.md#modify-an-localization)
* [Delete a Localization](localizations.md#delete-a-localization)

> \*\*Note\*\*
>
> The process for managing localizations for a Branding App is the same, regardless of the type (Classic or Modern (PSADT)).

## Add a Localization

To add a Localization:

1. To a new Branding app, follow the [Create a Branding app](add-branding.md#creating-a-branding-app) process until Step 10.
2. To an existing Branding app, follow the [Modify/Recreate Branding](modify-recreate-branding.md) process.
3. Click **Add Language**

![Clicking 'Add Language'](../../../../.gitbook/assets/image-\(3726\).png)

4. In the **Language** dropdown of the **Add Localization** screen, start typing the name of the relevant language or select it from the dropdown.

![Typing the name of the relevant language or selecting it from the 'Language' dropdown of the 'Add Localization' screen](../../../../.gitbook/assets/image-\(4238\).png)

5. If you are adding a localization to a **Modern (PSADT)** branding app, complete each of the required fields denoted by a read asterisk (<mark style="color:red;">\*</mark>) with the relevant values as detailed in [Default Language Notifications in Cloud](default-language-notifications.md).
6. For each of the three tabs (**Install**, **Uninstall**, **Update)**, complete each field with the relevant text and variables you want to use as detailed in [Default Language Notifications in Cloud](default-language-notifications.md).

![Completing all of the fields on all of the tabs](../../../../.gitbook/assets/image-\(4239\).png)

> \*\*Important\*\*
>
> When you add a new localization, you must complete all of the fields on all of the tabs before you can save it.

> \*\*Tip\*\*
>
> We include common variable names under each field, which you can add by clicking the relevant variable(s).
>
> Also, see \[Default Language Notifications]\(default-language-notifications.md) for a list of the default language notifications for English, which you can use to help you configure other languages.

7. Click **Save** to save your settings.

![Clicking 'Save' to save your settings](../../../../.gitbook/assets/image-\(4240\).png)

> \*\*Tip\*\*
>
> If you make a mistake or want to start again, click \*\*Reset\*\* to reset this screen and start over from the beginning of this process.

The **Branding** screen is redisplayed with the newly added localization shown at the top of the list allowing you to select it if required.

!['Branding' screen redisplayed with the newly added localization shown at the top of the list allowing you to select it if required](../../../../.gitbook/assets/image-\(3727\).png)

## Modify a Localization

To modify a Localization for an existing Branding app:

1. Follow the [Edit Branding](modify-recreate-branding.md#edit-branding) process.
2. Click **Add Language** if you want to add a new language and follow the [Add a Localization](localizations.md#add-a-localization) process.
3. To modify an existing localization, click the pencil icon () beside the relevant language.

![Clicking the pencil icon beside the relevant language](../../../../.gitbook/assets/image-\(3728\).png)

4. Make any required changes, then click **Save** to save your changes.

![Clicking 'Save'](../../../../.gitbook/assets/image-\(4241\).png)

The **Branding** screen is redisplayed.

!['Branding' screen is redisplayed](../../../../.gitbook/assets/image-\(3729\).png)

5. Click **Save** to save your changes.

![Clicking 'Save' to save your changes](../../../../.gitbook/assets/image-\(3730\).png)

The list of branding apps is displayed along with the **Success – Branding Updated** notification.

!['Success – Branding Updated' notification](../../../../.gitbook/assets/image-\(3749\).png)

## Delete a Localization

To delete a Localization from either a new or existing branding app:

1. [Edit the branding app](modify-recreate-branding.md#edit-branding).
2. Click the red trash can beside the language you want to remove.

![Clicking the red trashcan beside the language you want to remove](../../../../.gitbook/assets/image-\(3732\).png)

The language is removed.

3. Click **Save** to save your changes.

![Clicking 'Save' to save your changes](../../../../.gitbook/assets/image-\(3734\).png)

The **Success – Branding updated** notification is displayed.

!['Success – Branding updated' notification](../../../../.gitbook/assets/image-\(3750\).png)

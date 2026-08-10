# Permissions required for Patch My PC Cloud

_Applies to: Patch My PC Cloud_

To onboard to Patch My PC (PMPC) Cloud, we require the following permissions:

<table><thead><tr><th valign="top">Permission</th><th valign="top">Claim</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">View your basic profile</td><td valign="top">profile</td><td valign="top"><p>Allows the app to see your basic profile (e.g., name, picture, user name, email address).</p><p>This is a permission requested to access your data in your Intune Tenant.</p></td></tr><tr><td valign="top">Maintain access to data you have given it access to</td><td valign="top">offline_access</td><td valign="top"><p>Allows the app to see and update the data you gave it access to, even when you are not currently using the app. This does not give the app any additional permissions.</p><p>This is a permission requested to access your data in &#x3C;<em>your_intune_tenant's_name</em>>.</p></td></tr></tbody></table>

As per the dialog box:

“_Accepting these permissions means that you allow this app to use your data as specified in their_ [_terms of service_](https://patchmypc.com/terms-of-service) _and_ [_privacy statement_](https://patchmypc.com/privacy-policy)_. You can change these permissions at_ [_https://myapps.microsoft.com_](https://myapps.microsoft.com)_._ [_Show details_](https://login.microsoftonline.com/common/login)_._”

You will be prompted to grant these during the onboarding process by clicking **Accept** on the **Permissions requested** dialog box.

!["Permissions required" prompting to grant permissions to your environment.](/_images/image-(2053).png)

> \*\*Note\*\*
>
> Whether or not you see the \*\*Permissions Required\*\* dialog box and what you see on it depends on the account you use to sign into Entra and how the \*\*User consent for applications\*\* settings are configured in your environment.
>
> !\[]\(/\_images/image-(3682).png>)
>
> You will only see the C\*\*onsent on behalf of your organization\*\* checkbox if the user account you are signed in with is a Global Administrator or has the Privileged Role Administrator role.
>
> How the \*\*User consent for applications\*\* settings are configured determines whether you can sign up for the PMPC Cloud or not.
>
> If \*\*Do not allow user consent\*\* is configured, you will not see the \*\*Permissions Requested\*\* dialog box, but an error prompting you to contact an administrator.
>
> If either \*\*Allow user consent for apps from verified publishers, for selected permissions\*\* or \*\*Let Microsoft manage your consent settings (Recommended)\*\* is configured, any user can register for the PMPC Cloud and complete the app registration.
>
> Also, if you will use the Intune Apps Feature, the onboarding process requires additional permissions as detailed in \[Permissions required for Intune Apps]\(permissions-required-for-intune-apps.md).
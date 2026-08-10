---
description: Enabling user authentication using Azure Active Directory
---

# Advanced Insights Azure AD (Entra ID) Authentication

_Applies to: Patch My PC Advanced Insights_

Advanced Insights supports authentication using Entra ID credentials using OpenID. To configure this is a two-step process:

1. Create an App Registration in Entra
2. Enter the App Registration details to Advanced Insights

### Creating the App Registration <a href="#creating-the-app-registration" id="creating-the-app-registration"></a>

Navigate to the Entra Admin Centre and log in with an account that has permissions to create App Registrations.

You will add a name for the App Registration (for example _"AdvancedInsights"_).

In Supported Accounts select _**"Accounts in this organizational directory only"**_

**Redirect URI**

> \*\*Redirect URI\*\* is used for Microsoft to return the login token to Advanced Insights.
>
> \\
>
> This URI must be configured with the value of the internal FQDN of the server hosting Advanced Insights, including the configured port.
>
> \_(https://\*\*{AdvancedInsightsInternalServerFQDN}:{port}\*\*/account/login)\_

Example redirect URI:

_https://advinsightsserver01.contoso.local:444/account/login_

Select _**"Single-Page Application (SPA)"**_ from the dropdown list in the **"**_**Redirect URI"**_ section, and enter the URI.

![](/_images/app-reg-(3).png)

When you have filled in the required properties click **Register**.

You will be shown the App Registration overview screen. We need to copy some properties from here.

Copy **Application (client) ID** and **Directory (tenant) ID** values into a Notepad document.

![](/_images/app-reg2-(1).png)

Now click the _"**Authentication"**_ link on the left in the _"**Manage**"_ section.

In the _"**Implicit grant for hybrid flows"**_ section, tick both options for:

_**"Access tokens (used for implicit flows)"**_

_**"ID tokens (used for implicit and hybrid flows)"**_

This grants the application permissions to issue the tokens used by Advanced Insights to validate login.

To save changes, click **'Save'**.

![](/_images/app-reg3-(1).png)

Click "**Certificates and secrets"**, then within the **"Client secrets"** section, click _**"New client secret"**_.

Name the secret and set an expiry duration that is suitable for your environment.

> On expiry, logins to Advanced Insights using Entra ID credentials will stop working if you don’t update the client secret.

![](/_images/app-reg5-(1).png>)

Click 'Add' to save the **"Client secret"** configuration.

Now you can copy the **"Value"** of your client secret and add it to your Notepad document:

![](/_images/app-reg6-(1).png>)

This completes the configuration work in the Azure Portal.

### Adding settings to Advanced Insights <a href="#adding-settings-to-callisto" id="adding-settings-to-callisto"></a>

1. Log into Advanced Insights with an **administrator** role account and navigate to the _**'Administration' > 'Settings'**_ menu. Select the _**"AzureAD"**_ tab.
2. Clear the _**"Deactivate"**_ checkbox.
3. Enter the value for your **Application ID/ClientID**.
4. Enter the value for your **Client Secret**.
5. Enter the value for your **Directory (tenant) ID**.
6. Select _**'Save All'**_.

![](/_images/9-(1).jpg>)

## **New users**

> By default, new users configured in Advanced Insights \*\*(including new Entra ID logins)\*\* will not be active (and can not login) until an administrator manually activates the account.
>
> !\[]\(/\_images/10.png)

1. Log into Advanced Insights with an **administrator** role account and navigate to the _**'Administration' > 'Settings'**_ menu. Select the _**"User Management"**_ tab.
2. Enable _**"New registered users are active by default."**_ checkbox.
3. Select _**'Save All'**_.

![](/_images/11-(1).jpg>)

This completes the configuration for adding the Entra ID App Registration details to Advanced Insights.

## **First login - Consent to Permissions**

The Advanced Insights logon screen will now show a _**"Sign in with Microsoft"**_ button.

![](/_images/12-(1).jpg>)

At first logon, an Azure administrator will have to consent to the application registration requested permissions.

![](/_images/advinslogin2-(1).png>)

> By default, new users will only be granted access to the Advanced Insights overview home page.
>
> Advanced Insights administrator can then enable access to additional dashboard views.

![](/_images/13-(1).jpg>)

### User requirements <a href="#user-requirements" id="user-requirements"></a>

You should check in the Users area in Advanced Insights that there are no existing user accounts with email addresses that match the Entra ID accounts you are going to have logging in. If you do, you can delete these accounts and they will be recreated on first login by that user.

You will always be able to log in as the Advanced Insights "Admin" to make configuration changes.

If the Entra ID account a user logs into Advanced Insights with has a matching on-prem AD Account with the same Email Address set, any RBAC role they have in ConfigMgr for their on-prem AD account will be maintained in Advanced Insights.

For example, if a log in with this Entra ID Account is used:

![](/_images/user1-(2).png>)

The on-premises Active Directory object of this account has the users Entra ID UPN set as the email property:

![](/_images/user2-(1).png>)
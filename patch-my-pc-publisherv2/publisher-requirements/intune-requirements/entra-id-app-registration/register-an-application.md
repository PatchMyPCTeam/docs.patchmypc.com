# Register an Application

_Applies to: Patch My PC Publisher V2.x_

The Publisher requires an Entra ID Application (client) ID to uniquely identify itself when authenticating to your tenant. This app registration represents the Publisher as a trusted service in Microsoft Entra ID and is used to request access tokens from the Microsoft identity platform. These tokens allow the Publisher to securely call the Microsoft Graph API to create, update, and assign Win32 applications in Intune without requiring a user to be signed in.

You can leverage an existing application or create a new one. The following section details how to create a new app registration for use with the Publisher.

{% hint style="info" %}
**Note**

If your Microsoft Entra ID administrator has already created an app registration for use with the Publisher, you can skip this step and proceed directly to reviewing and configuring the required Microsoft Graph [API permissions](/broken/pages/s6XwSjlokRedJV0oI4KF).
{% endhint %}

1. **Sign in to the Microsoft Entra admin center**\
   Sign in using an account with sufficient privileges (Application Developer or higher).
2. **Switch tenants (if applicable)**\
   If you are managing multiple tenants, use the Settings menu to select the target tenant where the app should be registered.
3.  **Navigate to App registrations**\
    Under **Microsoft Entra ID** > **App registrations**, select **New registration**.<br>

    <figure><img src="../../../../.gitbook/assets/image (392).png" alt="New app registration" width="563"><figcaption></figcaption></figure>
4.  **Enter registration details**

    1. Choose a friendly **Name** for the app (e.g., _Patch My PC Publisher – Intune Connector_)
    2. Select **Supported account types >** _**Accounts in this organizational directory only**_
    3. Leave **Redirect URI** blank
    4. **Register the application**\
       Click **Register** to create the app. Once complete, the **Overview** page will show the newly assigned **Application (client) ID** and **Directory (tenant) ID** — record both for later use.<br>

    <figure><img src="../../../../.gitbook/assets/image (393).png" alt="App registration details" width="563"><figcaption></figcaption></figure>

Once the application has been created, the next step is to configure the correct [API Permisisons](api-permissions.md).

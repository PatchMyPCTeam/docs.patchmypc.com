# OAuth2 (App Auth) Configuration

_Applies to: Patch My PC Publisher V2.x_

## Overview

OAuth2 allows the Publisher to send email without using a mailbox username and password. Instead, email is sent using a **Microsoft Entra ID app registration**, which is the recommended approach for modern cloud email services such as **Microsoft 365 (Exchange Online)** and **Google Workspace**.

This authentication method is intended for environments where SMTP basic authentication is restricted or deprecated and where secure, non-interactive service authentication is required.

## App Registration and Permissions

OAuth2 email authentication requires a **Microsoft Entra ID app registration** with the **Microsoft Graph Mail.Send (Application)** permission granted.

{% hint style="warning" %}
**Important**

This guidance applies to customers who choose to use OAuth with Microsoft Graph instead of SMTP based mail delivery. When using this approach, the Publisher sends email through Microsoft Graph as an unattended background service. Because no signed in user is present, OAuth 2.0 application permissions must be used along with the `/users/{user}/sendMail` endpoint, which requires the `Mail.Send` application permission. When granted, this permission allows the application to send mail as **any** mailbox in the tenant.

[Exchange Online documentation](https://learn.microsoft.com/en-us/exchange/permissions-exo/application-rbac#why-does-my-application-still-have-access-to-mailboxes-that-arent-granted-by-the-scope-i-used-in-exchange-online-application-rbac) explains that permissions assigned in Microsoft Entra ID and Exchange Online RBAC are additive and evaluated independently. If a tenant wide Microsoft Entra `Mail.Send` permission is granted, any scoped permission configured using Exchange Online RBAC or Application Access Policies is combined with the broader permission. The effective result is the union of both permissions, which still allows sending as any mailbox. For this reason, Exchange Online RBAC and Application Access Policies do not effectively restrict Microsoft Graph app only send operations. This behavior is a Microsoft platform limitation, not a Publisher specific design choice.
{% endhint %}

When configuring the app registration, you can apply standard Entra ID security practices such as:

* Using a dedicated app registration for email
* Using certificate-based authentication where possible
* Reviewing Entra ID sign-in and audit logs as part of normal operations

This approach aligns with Microsoft’s recommended model for service authentication and automation.

When deciding which Microsoft Entra ID app registration to use for OAuth2 email authentication, you have two options:

* [Use existing App Registration (Recommended)](oauth2-app-auth-configuration.md#option-1-use-existing-app-registration-recommended)
* [Create a new (or use a different) App Registration](oauth2-app-auth-configuration.md#option2-create-a-new-or-use-a-different-app-registration)

## Option 1: Use existing App Registration (Recommended)

This option reuses the existing authentication method already configured for Intune publishing, removing the need to create and manage a separate app registration. Using a single app registration centralises permissions and credentials, simplifying both initial setup and ongoing management.

### **When to choose this option**

* You already have Intune publishing configured in the Publisher.
* You want to manage a single app registration for all Patch My PC operations in Microsoft Graph.

### **Requirements**

* The existing app registration must have the Microsoft Graph – **Mail.Send (Application)** permission granted.

### Configure the App Registration

Follow the steps below to add the required Microsoft Graph **Mail.Send (Application)** permission to the Entra ID app registration used by the Publisher.

1. Sign in to the **Microsoft Entra admin center**.
2. Navigate to **Entra ID > App registrations**.
3. Select the app registration created for Patch My PC Publisher (for example, _Patch My PC Publisher – Intune Connector_).
4. In the left-hand menu, select **API permissions**.
5. Select **Add a permission**.

<figure><img src="../../../../.gitbook/assets/image (394).png" alt="Add an API Permission" width="563"><figcaption></figcaption></figure>

5. In the **Request API permissions** pane, choose **Microsoft Graph**.
6. Select **Application permissions** (not Delegated permissions).
7. Use the search box or expand the relevant categories and add the permissions listed in the table above, including:
   * Mail.Send
8. Select **Add permissions** to apply the selected permissions.
9. Select **Grant admin consent** and confirm the prompt to approve the permission.

<figure><img src="../../../../.gitbook/assets/image (238).png" alt="Confirm the Mail.Send permissions has been added and granted" width="563"><figcaption></figcaption></figure>

### Configure the Publisher

After selecting OAuth2 as the email authentication type, select **Use existing app registration** to reuse the same Microsoft Entra ID app registration configured under [Intune Apps/Updates > Options](../../intune-apps-updates/options/). The available fields are automatically updated to reflect the existing app registration details and authentication method.

<figure><img src="../../../../.gitbook/assets/image (4206).png" alt="Use existing app registration" width="446"><figcaption></figcaption></figure>

Click [Test Permissions](oauth2-app-auth-configuration.md#test-permissions) to verify the API permissions has been configured correctly.

{% hint style="info" %}
**Note**

If multiple tenants are configured in the Publisher using an **MSP** or **MSP Plus** license, select the appropriate **tenant** from the tenant selector to use the app registration for that specific tenant.
{% endhint %}

## Option 2: Create a new (or use a different) App Registration

This option uses a separate Microsoft Entra ID app registration that is not shared with Intune app and update publishing (if configured). The app registration can be newly created or an existing one in the tenant that you choose to use specifically for sending email from the Publisher.

{% hint style="info" %}
**Note**

Using a separate app registration allows you to isolate email-sending permissions from Intune publishing and manage credentials independently.
{% endhint %}

### When to choose this option

* You want to separate email functionality from Intune publishing in the Publisher
* You do not use Intune publishing with the Publisher
* You prefer separate ownership, auditing, or credential rotation
* Your security policy requires functional isolation or least-privilege separation

### Requirements

* The app registration must have the Microsoft Graph – **Mail.Send (Application)** permission granted
* Admin consent must be granted for the permission

### Configure the App Registration

Follow the steps below to add the required Microsoft Graph **Mail.Send (Application)** permission to the Entra ID app registration used by the Publisher.

1. Sign in to the Microsoft Entra admin center.
2. Decide which approach best fits your environment.
   1.  **Create a new app registration**

       i. Follow the guidance in [Register an Application](../../../publisher-requirements/intune-requirements/entra-id-app-registration/register-an-application.md) to register an application in Entra ID.\
       ii. After the app registration is created, continue to step 3.
   2.  **Use an existing app registration**

       i. Navigate to **Entra ID** > **App registrations**.\
       ii. Select the desired app registration to use for sending email notifications.\
       iii. Continue to step 3.
3. In the left hand menu of the app registration, select **API permissions**.
4. In the left-hand menu, select **API permissions**.
5. Select **Add a permission**.

<figure><img src="../../../../.gitbook/assets/image (394).png" alt="Add an API Permission" width="563"><figcaption></figcaption></figure>

5. In the **Request API permissions** pane, choose **Microsoft Graph**.
6. Select **Application permissions** (not Delegated permissions).
7. Use the search box or expand the relevant categories and add the permissions listed in the table above, including:
   * Mail.Send
8. Select **Add permissions** to apply the selected permissions.
9. Select **Grant admin consent** and confirm the prompt to approve the permission.

<figure><img src="../../../../.gitbook/assets/image (239).png" alt="Confirm the Mail.Send permissions has been added and granted" width="563"><figcaption></figcaption></figure>

10. Navigate to **Certificates & secrets** in the Entra ID app registration. Create or identify the client credential that will be used by the Publisher for email notifications. This can be either a certificate or a client secret, depending on the selected authentication method. Record the required values, such as the Application Client ID, Tenant ID, and certificate or secret details so you can [Configure the Publisher](oauth2-app-auth-configuration.md#configure-the-publisher-1).

{% hint style="info" %}
**Note**

For additional guidance on choosing and configuring app registration credentials, refer to the [Client Credentials](../../../publisher-requirements/intune-requirements/entra-id-app-registration/client-credentials.md), which explains credential types, requirements, and best practices in more detail.
{% endhint %}

### Configure the Publisher

After selecting OAuth2 as the email authentication type, configure the following options to complete the OAuth2 configuration in the Publisher.

#### Auth Type

Select the authentication type based on the client credential configured for the Entra ID app registration.

* Choose **Client Secret** if the app registration is configured with a client secret.
* Choose **Certificate** if the app registration is configured with a certificate.

#### Client ID

Enter the **Application Client ID** from the Entra ID app registration.

You can find the Application Client ID on the **Overview** page of the app registration in the Microsoft Entra admin center.

#### Tenant ID

Enter the tenant authority URL for your Microsoft Entra ID tenant.

This value is typically in the format:

`https://login.microsoftonline.com/<tenant-id>`

The tenant ID can be found on the **Overview** page of the Entra ID app registration or on the Entra ID tenant properties page. The Publisher uses this value to authenticate against the correct Entra ID tenant.

### Test Permissions

Click **Test Permissions** to validate that the configured app registration can authenticate successfully and has the required API permissions to send email.

When the test runs, the Publisher connects to Microsoft Entra ID using the configured app registration and checks whether the required permissions are present and granted.

The **App Registration Connection Status** window displays the status of each permission:

**Green check (OK)**\
The **Mail.Send** permission is present and correctly granted.

<figure><img src="../../../../.gitbook/assets/image (237).png" alt="App Registration Connection Status OK" width="563"><figcaption></figcaption></figure>

**Red error (Missing)**\
The **Mail.Send** permission is missing or has not been granted. Email Notifications will not work until the permission is added and admin consent is granted.

<figure><img src="../../../../.gitbook/assets/image (240).png" alt="App Registration Connection Status Failed" width="563"><figcaption></figcaption></figure>

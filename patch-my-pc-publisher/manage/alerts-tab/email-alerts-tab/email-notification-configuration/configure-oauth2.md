# Configure OAuth2 (App Auth) in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This article has not been updated for Version 3.x. Once it has, this banner will be removed.</p>
</blockquote>

_OAuth2_ allows Patch My PC (PMPC) Publisher to send emails without using a mailbox username and password. Instead, email is sent using a Microsoft Entra ID app registration, which is the recommended approach for modern cloud email services such as Microsoft 365 (Exchange Online) and Google Workspace.

This authentication method is intended for environments where SMTP basic authentication is restricted or deprecated and where secure, non-interactive service authentication is required.

## App Registration and Permissions

OAuth2 email authentication requires a **Microsoft Entra ID app registration** with the **Microsoft Graph Mail.Send (Application)** permission granted.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This guidance applies to customers who choose to use OAuth with Microsoft Graph instead of SMTP-based mail delivery. When using this approach, Publisher sends emails through Microsoft Graph as an unattended background service.&#x20;</p>
<p>As no signed-in user is present, OAuth 2.0 application permissions must be used along with the `/users/{user}/sendMail` endpoint, which requires the `Mail.Send` application permission. When granted, this permission allows the application to send mail as **any** mailbox in the tenant.</p>
<p><a href="https://learn.microsoft.com/en-us/exchange/permissions-exo/application-rbac#why-does-my-application-still-have-access-to-mailboxes-that-arent-granted-by-the-scope-i-used-in-exchange-online-application-rbac">Exchange Online documentation</a> explains that permissions assigned in Microsoft Entra ID and Exchange Online RBAC are additive and evaluated independently. If a tenant-wide Microsoft Entra `Mail.Send` permission is granted, any scoped permission configured using Exchange Online RBAC or Application Access Policies is combined with the broader permission. The effective result is the union of both permissions, which still allows sending as any mailbox. For this reason, Exchange Online RBAC and Application Access Policies do not effectively restrict Microsoft Graph app-only send operations. This behavior is a Microsoft platform limitation, not a Publisher-specific design choice.</p>
</blockquote>

When configuring the app registration, you can apply standard Entra ID security practices such as:

* Using a dedicated app registration for email
* Using certificate-based authentication where possible
* Reviewing Entra ID sign-in and audit logs as part of normal operations

This approach aligns with Microsoft’s recommended model for service authentication and automation.

When deciding which Microsoft Entra ID app registration to use for OAuth2 email authentication, you have two options:

* [Option 1: Use existing App Registration (Recommended)](configure-oauth2.md#option-1-use-existing-app-registration-recommended)
* [Option 2: Create a new (or use a different) App Registration](configure-oauth2.md#option2-create-a-new-or-use-a-different-app-registration)

## Option 1: Use existing App Registration (Recommended)

Using an existing App Registration reuses the existing authentication method already configured for Intune publishing, removing the need to create and manage a separate app registration. Using a single app registration centralizes permissions and credentials, simplifying both initial setup and ongoing management.

### **When to choose this option**

Use this option when you:

* Already have Intune publishing configured in Publisher.
* Want to manage a single app registration for all PMPC operations in Microsoft Graph.

### **Requirements**

* The existing app registration requires the Microsoft Graph – **Mail.Send (Application)** permission to be granted.

### Configure the App Registration

To add the required Microsoft Graph **Mail.Send (Application)** permission to the Entra ID app registration used by Publisher:

1. Sign in to the **Microsoft Entra admin center**.
2. Navigate to **Entra ID > App registrations**.
3. Select the app registration created for Patch My PC Publisher (for example, _Patch My PC Publisher – Intune Connector_).
4. In the left-hand menu, select **API permissions**.
5. Select **Add a permission**.

![Add an API Permission](/_images/image-(394).png "Add an API Permission")

6. In the **Request API permissions** pane, choose **Microsoft Graph**.
7. Select **Application permissions** (not Delegated permissions).
8. Use the search box or expand the relevant categories and add the permissions listed in the table above, including:
   * **Mail.Send**
9. Select **Add permissions** to apply the selected permissions.
10. Select **Grant admin consent** and confirm the prompt to approve the permission.

![Confirm the Mail.Send permissions has been added and granted](/_images/image-(238).png "Confirm the Mail.Send permissions has been added and granted")

### Configure Publisher

After selecting OAuth2 as the email authentication type, select **Use existing app registration** to reuse the same Microsoft Entra ID app registration configured under [Intune Apps/Updates | Options](../../../../../patch-my-pc-publisherv2/administration/intune-apps-updates/options/). The available fields are automatically updated to reflect the existing app registration details and authentication method.

![Use existing app registration](/_images/image-(4206).png "Use existing app registration")

Click [Test Permissions](configure-oauth2.md#test-permissions) to verify the API permissions have been configured correctly.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If multiple tenants are configured in Publisher using an **MSP** or **MSP Plus** license, select the appropriate tenant from the tenant selector to use the app registration for that specific tenant.</p>
</blockquote>

## Option 2: Create a new (or use a different) App Registration

Creating a new (or using a different) App Registration uses a separate Microsoft Entra ID app registration that is not shared with Intune app and update publishing (if configured). The app registration can be newly created or an existing one in the tenant that you choose to use specifically for sending email from Publisher.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Using a separate app registration allows you to isolate email-sending permissions from Intune publishing and manage credentials independently.</p>
</blockquote>

### When to choose this option

Use this option when you:

* Want to separate email functionality from Intune publishing in Publisher.
* Do not use Intune publishing with Publisher.
* Prefer separate ownership, auditing, or credential rotation.
* Have a security policy that requires functional isolation or least-privilege separation.

### Requirements

* The app registration must have been granted the Microsoft Graph – **Mail.Send (Application)** permission.
* Admin consent must be granted for the permission.

### Configure the App Registration

To add the required Microsoft Graph **Mail.Send (Application)** permission to the Entra ID app registration used by Publisher:

1. Sign in to the Microsoft Entra admin center.
2. Decide which approach best fits your environment.
   1.  **Create a new app registration**

       i. Follow the guidance in [Register an Application](../../../../../patch-my-pc-publisherv2/publisher-requirements/intune-requirements/entra-id-app-registration/register-an-application.md) to register an application in Entra ID.\
       ii. After the app registration is created, continue to step 3.
   2.  **Use an existing app registration**

       i. Navigate to **Entra ID** > **App registrations**.\
       ii. Select the desired app registration to use for sending email notifications.\
       iii. Continue to step 3.
3. In the left-hand menu of the app registration, select **API permissions**.
4. In the left-hand menu, select **API permissions**.
5. Select **Add a permission**.

![Add an API Permission](/_images/image-(394).png "Add an API Permission")

6. In the **Request API permissions** pane, choose **Microsoft Graph**.
7. Select **Application permissions** (not Delegated permissions).
8. Use the search box or expand the relevant categories and add the permissions listed in the table above, including:
   * **Mail.Send**
9. Select **Add permissions** to apply the selected permissions.
10. Select **Grant admin consent** and confirm the prompt to approve the permission.

![Confirm the Mail.Send permissions has been added and granted](/_images/image-(239).png "Confirm the Mail.Send permissions has been added and granted")

11. Navigate to **Certificates & secrets** in the Entra ID app registration. Create or identify the client credential Publisher will use for email notifications (this can be either a certificate or a client secret, depending on the selected authentication method). Make a note of the required values, such as the Application Client ID, Tenant ID, and certificate or secret details so you can [Configure Publisher](configure-oauth2.md#configure-the-publisher-1).

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>For additional guidance on choosing and configuring app registration credentials, refer to [Client Credentials](../../../../../patch-my-pc-publisherv2/publisher-requirements/intune-requirements/entra-id-app-registration/client-credentials.md), which explains credential types, requirements, and best practices in more detail.</p>
</blockquote>

### Configure Publisher

After selecting **OAuth2** as the email authentication type, configure the following options to complete the OAuth2 configuration in the Publisher.

#### Auth Type

Select the authentication type based on the client credential configured for the Entra ID app registration.

* Choose **Client secret** if the app registration is configured with a client secret.
* Choose **Certificate** if the app registration is configured with a certificate.

#### Client ID

Enter the Application **Client ID** from the Entra ID app registration, which you can find on the **Overview** page of the app registration in the Microsoft Entra admin center.

#### Tenant ID

Enter the tenant authority URL for your Microsoft Entra ID tenant in the **Tenant ID** field, which is typically in the format:

`https://login.microsoftonline.com/{tenant-id}`&#x20;

The tenant ID can be found on the **Overview** page of the Entra ID app registration or on the Entra ID tenant properties page. Publisher uses this value to authenticate against the correct Entra ID tenant.

### Test Permissions

Click **Test Permissions** to validate that the configured app registration can authenticate successfully and has the required API permissions to send email.

When the test runs, Publisher connects to Microsoft Entra ID using the configured app registration and checks whether the required permissions are present and granted.

The **App Registration Connection Status** window displays the status of each permission:

#### **Green check (OK)**

The **Mail.Send** permission is present and correctly granted.

![App Registration Connection Status OK](/_images/image-(237).png "App Registration Connection Status OK")

#### **Red error (Missing)**

The **Mail.Send** permission is missing or has not been granted. Email Notifications will not work until the permission is added and admin consent is granted.

![App Registration Connection Status Failed](/_images/image-(240).png "App Registration Connection Status Failed")
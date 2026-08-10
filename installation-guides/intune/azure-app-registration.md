# Entra ID App Registration

_Applies to: On-premises Publisher_

This article covers integrating the Patch My PC Publisher with your **Intune tenant**.  We will go over creating an **app registration** in your **Entra ID** environment and configuring the Graph API permissions required for the Publisher to automatically create, update and assign **Win32 applications** in your Intune tenant; as well as configuring the tenant authority, application ID and application secret within the Publisher.

**Topics** covered in this article:

* [**Step 1: Registering the Patch My PC Application in Entra ID**](azure-app-registration.md#step-1-registering-the-patch-my-pc-application-in-entra-id)
* [**Step 2: Configure API Permissions for the New Application**](azure-app-registration.md#step-2-configure-api-permissions-for-the-new-application)
* [**Step 3: Configuring Certificates & Secrets**](azure-app-registration.md#step-3-configuring-a-certificate-or-client-secret)
  * [Option 1: Creating a self-signed Certificate](azure-app-registration.md#option-1-creating-a-self-signed-certificate)
    * [Create the Certificate](azure-app-registration.md#create-the-certificate)
    * [Export the Public Key](azure-app-registration.md#export-the-public-key)
  * [Option 2: Creating a Client Secret](azure-app-registration.md#option-2-creating-a-client-secret)
* [**Step 4: Configuring the Patch My PC Publisher to Connect to the Intune Tenant**](azure-app-registration.md#step-4-configuring-the-patch-my-pc-publisher-to-connect-to-the-intune-tenant)
  * [Test authentication, Connectivity and API Permissions](azure-app-registration.md#test-authentication-connectivity-and-api-permissions)

## Step 1: Registering the Patch My PC Application in Entra ID

In order for our service to have permissions to your Intune tenant for application management, start by navigating to [Entra ID](https://entra.microsoft.com/) > **App registrations,** and click **New registration** in the top left of the main pane.

![](/_images/image-(1823).png>)

Give your app registration a relevant name such as “Patch My PC – Intune Connector”.  Configure the account types based on your tenant requirements.  For the Redirect URI, leave it to the default unless you have specific requirements for configuring the Redirect URI.  Then click **Register**.

![](/_images/image-(1815).png>)

## Step 2: Configure API Permissions for the New Application

<blockquote class="wp-block-quote">
<p>A full Intune API reference KB article for the Publisher can be found at <a href="https://patchmypc.com/patchmypc-publisher-api-reference">https://patchmypc.com/patchmypc-publisher-api-reference</a></p>
</blockquote>

After you register a new application, we will need to delegate certain permissions in order for the Patch My PC Publisher to create and update Win32 applications in your Intune tenant, as well as view Entra ID groups and create assignments for the applications automatically.&#x20;

Once the new app is registered, navigate to the **API permissions** node in the left column of the newly created app’s page. In the **API permissions** page, click the button to **Add a permission**, then in the right pane that appears, select the **Microsoft Graph** API. &#x20;

![](/_images/image-(1976).png>)

Then, you are prompted for what type of permissions your app requires select **Application permissions**. In the **Select permissions** table view, search for “**DeviceManagement**” and under those permissions, enable the following:

*   **DeviceManagementApps.ReadWrite.All**

    (View and create applications in Intune)
*   **DeviceManagementConfiguration.Read.All**

    (View properties and relationships of assignment filters)
*   **DeviceManagementManagedDevices.Read.All**

    (View device inventory for the auto-publish feature)
*   **DeviceManagementRBAC.Read.All**

    (View scopes to be assigned to applications)
*   **DeviceManagementServiceConfig.ReadWrite.All**

    (Update Enrollment Status Page configurations)

![](/_images/image-(1904).png>)

Then, search for “GroupMember”, and under Group permissions, enable:

* **GroupMember.Read.All**
  * View Entra ID groups to enable automatic application deployment

![](/_images/image-(1849).png>)

Click **Add permissions**.

To approve the new permissions, click **Grant admin consent for**. Choose **Yes** if you are prompted to consent for the required permissions.  You must be logged in with an account that has permissions to perform this task.

<blockquote class="wp-block-quote">
<p>Note: Granting admin consent may require one of the following roles: <a href="https://docs.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#global-administrator">Global Administrator</a> or <a href="https://docs.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#privileged-role-administrator">Privileged Role Administrator</a>.</p>
</blockquote>

The result is shown below.

![](/_images/image-(1784).png>)

<blockquote class="wp-block-quote">
<p>Note: To display the _names_ of users or devices inside an Entra ID group when assigning apps or updates in the Publisher, the following Microsoft Graph API permissions are also required:</p>
<p>• **User.ReadBasic.All**\</p>
<p>Allows the service to read basic user details so user **names** can be shown when double clicking a group in the group picker window.</p>
<p>• **Device.Read.All**\</p>
<p>Allows the service to read device details so device **names** can be can be shown when double clicking a group in the group picker window.</p>
<p>Without these permissions, the Publisher can see that a group contains members, but it cannot resolve those members into readable user or device names. The image below shows the experience both with and without the adidtional permissions listed above.</p>
<p>![](/_images/image-(3712).png>)</p>
</blockquote>

## Step 3: Configuring a Certificate or Client Secret

A certificate is considered more secure than a client secret for authentication to the new app registration as it is something you have (private key) rather than something you know (password). A client secret is the easiest configuration method but is considered less secure. &#x20;

<blockquote class="wp-block-quote">
<p>More guidance on why a certificate should be used instead of a client secret can be found at <a href="https://learn.microsoft.com/en-us/azure/active-directory/develop/security-best-practices-for-app-registration#certificates-and-secrets">https://learn.microsoft.com/en-us/azure/active-directory/develop/security-best-practices-for-app-registration#certificates-and-secrets</a></p>
</blockquote>

Choose _**either**_ [Option 1](azure-app-registration.md#option-1-creating-a-self-signed-certificate) or [Option 2](azure-app-registration.md#option-2-creating-a-client-secret) from the steps below to create an authentication credential for use with the new app registration. We strongly recommend using [Option 1](azure-app-registration.md#option-1-creating-a-self-signed-certificate).

### Option 1: Creating a Self-Signed Certificate

<blockquote class="wp-block-quote">
<p>Certificate-based authentication is the preferred authentication method when connecting to an Entra ID App Registration. This document will focus on creating a self-signed certificates for use with the Patch My PC Publisher: <a href="https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-self-signed-certificate">Create a self-signed public certificate to authenticate your application</a>.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>Self-signed certificates with long expiry dates may use outdated hash and cipher suites that may not be strong enough as industry standards and best practices change. For this reason, choose short expiry dates or purchase a certificate signed by a well-known certificate authority.</p>
</blockquote>

The following are the current **requirements** for using certificate-based authentication that apply to both purchased and self-signed certificates:-

* A 2048-bit key length. While longer values are supported, the 2048-bit size is highly recommended for the best combination of security and performance.
* Uses the RSA cryptographic algorithm. Entra ID currently supports only RSA.
* The certificate is signed with the SHA256 hash algorithm (Entra ID also supports certificates signed with SHA384 and SHA512 hash algorithms).
* The certificate is valid for only one year.

Follow the steps below to create a self-signed certificate using the _**New-SelfSignedCertificate**_ and _**Export-Certificate**_ PowerShell cmdlets:-

#### _**Create the Certificate**_

Open a PowerShell window on the same computer where the Patch My PC Publisher is installed. Be sure to elevate the prompt by choosing _**Run as Administrator.**_

![](/_images/image-(1746).png)

Copy the following code snippet to and paste into the elevated PowerShell window.

```
$subjectName = 'PatchMyPCIntuneConnector'
$certStore = 'LocalMachine'
$validityPeriod = 12

$newCert = @{
    Subject = "CN=$($subjectName)"
    CertStoreLocation = "Cert:\$($certStore)\My"
    HashAlgorithm = 'sha256'
    KeyExportPolicy = 'NonExportable'
    KeyUsage = 'DigitalSignature'
    KeyAlgorithm = 'RSA'
    KeyLength = 2048
    KeySpec = 'Signature'
    NotAfter = (Get-Date).AddMonths($($validityPeriod))
    TextExtension = @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
}
$cert = New-SelfSignedCertificate @newCert
```

![](/_images/image-(1979).png)

Verify the certificate was created successfully in the Local Machine _**Personal**_ Certificate Store by running _**certlm.msc.**_

![](/_images/image-(1744).png)

#### Export the Public Key

We need to export the Public Key and upload it to the new app registration for the Patch My PC Intune connector. Follow the steps below:-

Open  PowerShell window on the same computer where the Patch My PC Publisher is installed. Be sure to elevate the prompt by choosing _**Run as Administrator.**_

![](/_images/image-(1746).png)

Copy the following code snippet to and paste into the elevated PowerShell window.

```
$subjectName = 'PatchMyPCIntuneConnector'
$certFolder = "C:\temp\certs"
New-Item -Path $certFolder -ItemType Directory -Force | Out-Null
$certExport = @{
Cert = $Cert
FilePath = "$($certFolder)\$($subjectName).cer"
}
Export-Certificate @certExport
```

![](/_images/image-(1751).png)

Verify the certificate was exported successfully in the _**C:\temp\certs**_ folder.

![](/_images/image-(1752).png)

<blockquote class="wp-block-quote">
<p>If you receive the message "The system cannot find the path specified" (as shown below), please ensure the credentials used to launch the PowerShell session have permission to create a folder at C:\temp or specify a new path for the $certFolder variable where you do have permission to create the folder.</p>
</blockquote>

![](/_images/image-(1750).png)

In the browser, navigate to the App registration created in [Step 1](azure-app-registration.md#step-1-registering-the-patch-my-pc-application-in-azure-a-d) and select the **Certificates & secrets node** in the left column. Select the _**Certificates**_ and click _**Upload certificate**_.

![](/_images/image-(1754).png)

Browse to the _**C:\temp\certs**_ folder, select the certificate that was exported earlier, click _**Open**_ and then click _**Add.**_

![](/_images/image-(1755).png)

Verify the public key is listed correctly in the app registration.

![](/_images/image-(1756).png)

### Option 2: Creating a Client Secret

<blockquote class="wp-block-quote">
<p>If you have already followed the instructions for Option 1, you do not need to create a client secret. Instead, go to [Step 4](azure-app-registration.md#step-4-configuring-the-patch-my-pc-publisher-to-connect-to-the-intune-tenant)</p>
</blockquote>

A client secret, a password string that our app will use to prove its identity when requesting a token.  Navigate to the **Certificates & secrets node** in the left column, and click the button to add a **New client secret**. Decide on a description and expiration date (in months) that best suits your organization’s needs, then click **Add**.

<blockquote class="wp-block-quote">
<p>Microsoft recommends a client secret of no longer than 6 months</p>
</blockquote>

![](/_images/image-(1933).png>)

Copy the **Value** for the Client Secret you created. Save this value to a secure location, you will enter the value under **Application Secret** in the **Intune Options** of the Publisher.&#x20;

![](/_images/image-(1857).png>)

<blockquote class="wp-block-quote">
<p>You may receive an error similar to **‘An error occurred while connecting to Intune: AADSTS7000215: Invalid client secret is provided.’** within the PatchMyPC.log file. If you receive this error please **repeat** [**option 2**](azure-app-registration.md#option-2-creating-a-client-secret) **above** to create a new secret, or review your existing secret configuration within the Publisher to ensure you are using the correct value.</p>
</blockquote>

## Step 4: Configuring the Patch My PC Publisher to Connect to the Intune Tenant

Navigate to the **Overview** node of the app registration, and copy the **Application (client) ID**.  Save this value to a secure location along with your secret key value.

![](/_images/application-client-id.png)

If you do not know your Intune tenant domain, navigate to the [tenant status page](https://devicemanagement.microsoft.com/#blade/Microsoft_Intune_DeviceSettings/TenantAdminMenu/tenantStatus) in your Intune tenant, and look at the property for **Tenant name**.

![](/_images/tenant-status.png)

Now, it is time to go to the **Intune Options** window of the Publisher **Patch My PC Publisher** to configure the following:-

[**Authority**](azure-app-registration.md#authority)\
[**Application ID**](azure-app-registration.md#application-id)\
[**Certificate or Application Secret** ](azure-app-registration.md#certificate-application-secret)(depending on whether you followed Step 3 option 1 or option 2)

![](/_images/Intune-Options.png)

### **Authority**

The **Authority** value is a URL made up from the Microsoft authentication endpoint and your tenant name. The newer Microsoft authentication endpoint should be used:-\
\
**https://login.microsoftonline.com**

<blockquote class="wp-block-quote">
<p>Referring to the screenshot above, replace _tenantname.onmicrosoft.com_ with the **Tenant name** you found in the **tenant status page** of your Intune tenant. \</p>
<p>\</p>
<p>The construct of the URL should look something like **https://login.microsoftonline.com/<\<Tenant name>>** \</p>
<p>\</p>
<p>The complete Authority value should look similar to this example below:-\</p>
<p>\</p>
<p>**https://login.microsoftonline.com/tenantname.onmicrosoft.com**</p>
</blockquote>

### **Application ID**

Paste the **Application ID** that you recorded earlier.&#x20;

### **Certificate / Application Secret**

If you chose to use a Certificate for authentication, click the certificate option and browse the Local Machine store for the correct certificate and click **Ok.**

![](/_images/image-(1757).png)

If you chose to use a Client Secret for authentication, click the Application Secret option and enter the Client Secret _**value**_ you recorded earlier.

![](/_images/image-(1758).png)

### Test Authentication, Connectivity and API Permissions

Click **Test** to view the **Intune Connection Status** and validate that the **Publisher** can connect to your Intune tenant. If the listed permissions all have a green checkmark under **Enabled**, you can now begin to publish applications to your Intune tenant.

![](/_images/image-(1964).png>)

<blockquote class="wp-block-quote">
<p>If the associated tenant is on <a href="https://learn.microsoft.com/en-us/graph/deployments">GCC High</a> (US Government), the changes below are required:</p>
<p>**Authority:** <a href="https://login.microsoftonline.us/">https://login.microsoftonline.us</a>\</p>
<p>**Authentication URL:** <a href="https://graph.microsoft.us/">https://graph.microsoft.us</a>\</p>
<p>**Graph Base URL:** <a href="https://graph.microsoft.us/beta">https://graph.microsoft.us/beta</a></p>
<p>If the associated tenant is operating within <a href="https://learn.microsoft.com/en-us/graph/deployments">21Vianet</a>, the changes below are required:</p>
<p>**Authority:** <a href="https://login.chinacloudapi.cn/">https://login.chinacloudapi.cn</a>\</p>
<p>**Authentication URL:** <a href="https://microsoftgraph.chinacloudapi.cn">https://microsoftgraph.chinacloudapi.cn</a>\</p>
<p>**Graph base URL:** <a href="https://microsoftgraph.chinacloudapi.cn/beta">https://microsoftgraph.chinacloudapi.cn/beta</a></p>
</blockquote>
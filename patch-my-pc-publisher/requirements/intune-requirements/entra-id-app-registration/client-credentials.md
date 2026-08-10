# Client Credentials for Patch My PC  Publisher

_Applies to: Patch My PC Publisher V3.x_

Patch My PC (PMPC) Publisher authenticates to Microsoft Intune using client credentials associated with an Entra ID app registration. Client credentials allow Publisher to authenticate using app-only (non-interactive) authentication, which is required for automation and unattended publishing.

Microsoft Entra ID supports two client credential types:

* [Certificates](client-credentials.md#use-a-certificate-for-authentication)
* [Client Secrets](client-credentials.md#use-a-client-secret-for-authentication)

Although Publisher supports both methods, [certificate-based authentication](client-credentials.md#use-a-certificate-for-authentication) is strongly recommended.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Certificate-based authentication is recommended because it uses a _"something you have"_ security model rather than a _"something you know"_ model. The private key is stored securely on the device where Publisher is installed and is never transmitted or shared.&#x20;</p>
<p>Authentication succeeds only if the calling service can prove possession of the private key, making it significantly harder to compromise than a client secret, which is simply a string value that can be copied, leaked, or reused from elsewhere.</p>
<p>This approach aligns with Microsoft’s security best practices for service-to-service authentication and provides stronger protection for automated workloads that require unattended access to Microsoft Intune.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See the <a href="https://learn.microsoft.com/entra/identity-platform/security-best-practices-for-app-registration#credentials-including-certificates-and-secrets">Credentials (including certificates and secrets)</a> section of <a href="https://learn.microsoft.com/entra/identity-platform/security-best-practices-for-app-registration">Security best practices for application properties in Microsoft Entra ID</a> for more guidance on why a certificate should be used instead of a client secret.&#x20;</p>
</blockquote>

## Use a Certificate for Authentication

Certificate-based authentication is the preferred and recommended approach for securing Publisher’s access to your Intune tenant. It uses a certificate that your Publisher service holds the private key for, while the public key is uploaded to the Entra ID app registration. This method aligns with Microsoft’s security best practices for service-to-service authentication.

### **Prerequisites**

To use a Certificate for Authentication:

* You must have created [an Entra ID App Registration](create-app-registration.md).
* You need access to the device where Publisher will be installed to create and export certificates.
* The certificate must meet the following requirements to be used for app authentication:
  * RSA key with 2048-bit minimum key length. (Entra ID currently supports only RSA).
  * Signed using SHA256 or stronger. (Entra ID also supports certificates signed with SHA384 and SHA512 hash algorithms).
  * Intended for client authentication.
  * Valid and not expired.
  * Private key accessible to the Publisher service.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The steps below detail how to create a self-signed certificate for client authentication. However, this is not the only supported option. If your organization has an established PKI and your PKI administrators provide a client authentication certificate, you may use that certificate instead.&#x20;</p>
<p>As long as the certificate meets Entra ID requirements and the private key is installed in the Local Machine certificate store on the server where Publisher is installed, Publisher can use it for authentication in the same way as a self-signed certificate.</p>
<p>See <a href="https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-self-signed-certificate">Create a self-signed public certificate to authenticate your application</a> for more information on creating a self-signed certificate for authentication with an app registration.</p>
</blockquote>

### Step 1: Create a Self-Signed Certificate

To create a Self-Signed Certificate:

1. Open **PowerShell as Administrator** on the computer where Publisher is installed.
2. Run the following PowerShell snippet to create a new self-signed certificate in the **Local Machine Personal** store.

```powershell
$subjectName = 'PatchMyPCPublisherIntuneConnector'
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
    NotAfter = (Get-Date).AddMonths($validityPeriod)
    TextExtension = @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
}
$cert = New-SelfSignedCertificate @newCert
```

3. Open **certlm.msc** and verify the new certificate appears under **Local Machine | Personal**.

![Client Authentication Certificate](/_images/image-(397).png "Client Authentication Certificate")

4. Whilst still in the elevated PowerShell session, run the following PowerShell snippet to export the **public key** (.cer) to a temporary folder.

```powershell
$certFolder = "C:\temp\certs"
New-Item -Path $certFolder -ItemType Directory -Force | Out-Null
Export-Certificate -Cert $cert -FilePath "$certFolder\PatchMyPCIntuneConnector.cer"
```

5. Confirm the `.cer` file exists in **C:\temp\certs**.

![Exported Public Key](/_images/image-(398).png "Exported Public Key")

### Step 2: Upload the Certificate to the App Registration

To upload the certificate to the App Registration:

1. In the **Microsoft Entra admin center**, open the app registration you created.
2. Navigate to **Certificates & secrets**.
3. Under **Certificates**, click **Upload certificate**.
4. Select the exported `.cer` file and click **Add**.
5. Verify the certificate’s **thumbprint** appears in the list with the correct expiration.

![Certificate Uploaded](/_images/image-(399).png "Certificate Uploaded")

### Step 3: Configure Publisher to use the Certificate

Finally, you need to configure Publisher to use the Certificate.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Authentication Settings](../../../manage/intune-tabs/intune-options/authentication-settings.md) for more details on using the certificate for authentication.</p>
</blockquote>

![Intune 'Authentication Settings'](/_images/image-(4754).png "Intune &#x27;Authentication Settings&#x27;")

## Use a Client Secret for Authentication

Client secret–based authentication is supported by Publisher, but it is not the recommended approach for production environments. A client secret is a shared string value (similar to a password) that Publisher uses to authenticate to Microsoft Intune via the Entra ID app registration.

This method may be suitable for:

* Short-term testing or proof-of-concept scenarios.
* Environments where certificate-based authentication is not possible.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>As client secrets are considered a weak client credential, they carry a higher risk of exposure and should be rotated regularly.</p>
</blockquote>

### **Prerequisites**

* You must have created [an Entra ID App Registration](create-app-registration.md).
* You have permission to create secrets for the app registration.

### Step 1: Create a Client Secret

To create a Client Secret:

1. Sign in to the **Microsoft Entra admin center**.
2. Navigate to **Entra ID | App registrations**.
3. Select the app registration created for Publisher.
4. In the left-hand menu, select **Certificates & secrets**.
5. Under **Client secrets**, select **New client secret**.

![New Client Secret](/_images/image-(401).png "New Client Secret")

6. Enter a **description** _(optional)_.
7. Choose an **expiration period** appropriate for your organization.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Microsoft recommends short-lived secrets. Expiration periods of **6 months or less** are strongly advised.</p>
</blockquote>

8. Select **Add**.
9. After the secret is created, **copy the Value immediately** and store it securely, as you will not be able to retrieve the secret once you navigate away from the page.

![Copy the Secret Value](/_images/image-(402).png "Copy the Secret Value")

### Step 2: Configure Publisher to use the Client Secret

Finally, you need to configure Publisher to use the Client Secret.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Authentication Settings](../../../manage/intune-tabs/intune-options/authentication-settings.md) for more details on using the Client Secret for authentication.</p>
</blockquote>

![Intune 'Authentication Settings'](/_images/image-(4755).png "Intune &#x27;Authentication Settings&#x27;")
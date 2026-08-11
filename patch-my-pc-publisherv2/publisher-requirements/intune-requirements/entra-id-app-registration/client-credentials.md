# Client Credentials

_Applies to: Patch My PC Publisher V2.x_

## Overview

The Publisher authenticates to Microsoft Intune using client credentials associated with an Entra ID app registration. Client credentials allow the Publisher to authenticate using app-only (non-interactive) authentication, which is required for automation and unattended publishing.

Microsoft Entra ID supports two client credential types:

* [Certificates](client-credentials.md#configure-a-certificate-for-authentication)
* [Client Secrets](client-credentials.md#configure-a-client-secret-for-authentication)

Both methods are supported by the Publisher, however, [certificate-based authentication](client-credentials.md#use-a-certificate-for-authentication) is strongly recommended.

> \*\*Tip\*\*
>
> Certificate-based authentication is recommended because it uses a "\*\*something you have"\*\* security model rather than a "\*\*something you know"\*\* model. The private key is stored securely on the device where the Publisher is isntalled and is never transmitted or shared. Authentication succeeds only if the calling service can prove possession of that private key, making it significantly harder to compromise than a client secret, which is simply a string value that can be copied, leaked, or reused from another location.
>
> This approach aligns with Microsoft’s security best practices for service-to-service authentication and provides stronger protection for automated workloads that require unattended access to Microsoft Intune.
>
> More guidance on why a certificate should be used instead of a client secret can be found at [https://learn.microsoft.com/en-us/azure/active-directory/develop/security-best-practices-for-app-registration#certificates-and-secrets](https://learn.microsoft.com/en-us/azure/active-directory/develop/security-best-practices-for-app-registration#certificates-and-secrets)

## Use a Certificate for Authentication

Certificate-based authentication is the preferred and recommended approach for securing the Publisher’s access to your Intune tenant. It uses a certificate that your Publisher service holds the private key for, while the public key is uploaded to the Entra ID app registration. This method aligns with Microsoft’s security best practices for service-to-service authentication.

**Prerequisites**

* You must have [registered an application](register-an-application.md) in Entra ID.
* You need access to the device where the Publisher will be installed to create and export certificates.
* The certificate must meet the following requirements to be used for app authentication:
  * RSA key with 2048-bit minimum key length. (Entra ID currently supports only RSA).
  * Signed using SHA256 or stronger. (Entra ID also supports certificates signed with SHA384 and SHA512 hash algorithms).
  * Intended for client authentication.
  * Valid and not expired.
  * Private key accessible to the Publisher service.

> \*\*Note\*\*
>
> The following steps detail how to create a self-signed certificate for client authentication. However, this is not the only supported option. If your organization has an established PKI and your PKI administrators provide a client authentication certificate, you may use that certificate instead.
>
> As long as the certificate meets Entra ID requirements and the private key is installed in the Local Machine certificate store on the server where Patch My PC Publisher is installed, the Publisher can use it for authentication in the same way as a self-signed certificate.
>
> For more information on creating a self-signed certificate for authentication with an app registration, see [Create a self-signed public certificate to authenticate your application](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-self-signed-certificate).

### Step 1: Create a Self-Signed Certificate

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

3. Open **certlm.msc** and verify the new certificate appears under **Local Machine > Personal**.

![Client Authentication Certificate](<../../../../.gitbook/assets/image-(397) (1).png>)

3. While still in the elevated PowerShell session, export the **public key** (.cer) to a temporary folder.

```powershell
$certFolder = "C:\temp\certs"
New-Item -Path $certFolder -ItemType Directory -Force | Out-Null
Export-Certificate -Cert $cert -FilePath "$certFolder\PatchMyPCIntuneConnector.cer"
```

4. Confirm that the `.cer` file exists in **C:\temp\certs**.

![Exported Public Key](<../../../../.gitbook/assets/image-(398) (1).png>)

### Step 2: Upload the Certificate to the App Registration

1. In the **Microsoft Entra admin center**, open the app registration you created.
2. Navigate to **Certificates & secrets**.
3. Under **Certificates**, click **Upload certificate**.
4. Select the exported `.cer` file and click **Add**.
5. Verify the certificate’s **thumbprint** appears in the list with the correct expiration.

![Certificate Uploaded](<../../../../.gitbook/assets/image-(399) (1).png>)

### Step 3: Configure the Publisher to use the Certificate

For more details on how to use the certificate for authnetication, see [Intune Apps / Updates > Options > Intune Authentication](/broken/pages/fRFRGAjMdaZk5TYWEwkt)

![Certificate Authentication in the Publisher](../../../../.gitbook/assets/image-\(4148\).png)

## Use a Client Secret for Authentication

Client secret–based authentication is supported by the Publisher, but it is not the recommended approach for production environments. A client secret is a shared string value (similar to a password) that the Publisher uses to authenticate to Microsoft Intune via the Entra ID app registration.

This method may be suitable for:

* Short-term testing or proof-of-concept scenarios.
* Environments where certificate-based authentication is not possible.

> \*\*Important\*\*
>
> Because client secrets are considered a weak client credential, they carry a higher risk of exposure and should be rotated at regular intervals.

**Prerequisites**

* You must have [registered an application](register-an-application.md) in Entra ID.
* You have permission to create secrets for the app registration.

### Step 1: Create a Client Secret

1. Sign in to the **Microsoft Entra admin center**.
2. Navigate to **Entra ID > App registrations**.
3. Select the app registration created for the Publisher.
4. In the left-hand menu, select **Certificates & secrets**.
5. Under **Client secrets**, select **New client secret**.

![New Client Secret](<../../../../.gitbook/assets/image-(401) (1).png>)

6. Enter a **description** _(optional)_.
7. Choose an **expiration period** appropriate for your organization.

> \*\*Note\*\*
>
> Microsoft recommends short-lived secrets. Expiration periods of \*\*6 months or less\*\* are strongly advised.

8. Select **Add**.
9. After the secret is created, **copy the Value immediately** and store it securely as you will not be able to retrieve the secret once you navigate away from the page.

![Copy the Secret Value](<../../../../.gitbook/assets/image-(402) (1).png>)

### Step 2: Configure the Publisher to use the Client Secret

For more details on how to use the certificate for authentication, see [Intune Apps / Updates > Options > Authentication Settings](../../../administration/intune-apps-updates/options/authentication-settings.md).

![Client Secret Authentication Settings in the Publisher](../../../../.gitbook/assets/image-\(4150\).png)

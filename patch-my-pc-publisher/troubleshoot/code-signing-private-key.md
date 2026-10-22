# Troubleshoot Code Signing Certificate Private Key Issues for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This article provides guidance for resolving script-signing failures caused by a missing or inaccessible certificate private key.

## Identify Private Key Issues

When Publisher cannot use the code signing certificate’s private key, publishing may fail with entries similar to the following in **PatchMyPC.log**:

```
Failed to sign the file using native method. [Error 2148081670].
Trying with PowerShell command...
```

```
Set-AuthenticodeSignature returned status 'UnknownError':
No provider was specified for the store or object.
```

```
The code signing certificate's private key is held by the legacy provider [unknown]
```

```
Code signing certificate private key provider: [unknown] [CNG=False] [SupportsSha256=False]
```

These errors can occur when:

* The certificate’s private key file is missing.
* Permissions prevent the Publishing Service account from accessing the private key.
* The certificate’s association with its private key is missing or incorrect.

## Check the Certificate and Private Key

Perform these checks on the server running the Patch My PC Publishing Service.

### Identify the Certificate

Depending on the publishing operation that failed, check the code signing certificate configured in the Publisher under:

* **ConfigMgr Apps > Base Install Options**
* **Intune Apps > Intune Options**
* **WSUS Updates > WSUS Options**

Open `certlm.msc`, locate the certificate in the corresponding **Local Computer** certificate store, and verify that its thumbprint matches the certificate configured in Publisher.

On the **General** tab, check for:

<figure><img src="../../.gitbook/assets/image (1513).png" alt="Check for Private Key" width="563"><figcaption></figcaption></figure>

```
You have a private key that corresponds to this certificate.
```

{% hint style="info" %}
**Note**

This message indicates a private-key association. It does not confirm that the private key file exists or that the Publishing Service account can use it.
{% endhint %}

### Locate the Private Key File

Run the following from an elevated PowerShell session. Replace the thumbprint and store with the values identified in the log:

```
$cert  = '08B3DB3AAD4144D9E838452DF939D40CE5657465'
$store = 'My' # My = Personal; or WSUS

certutil.exe -v -store $store $cert
```

Look for **Provider** and **Unique container name**. The unique container name identifies the private key filename.

<table><thead><tr><th valign="top">Provider</th><th valign="top">Machine private key folder</th></tr></thead><tbody><tr><td valign="top">Microsoft Software Key Storage Provider</td><td valign="top"><code>C:\ProgramData\Microsoft\Crypto\Keys</code></td></tr><tr><td valign="top">Legacy RSA Cryptographic Service Provider</td><td valign="top"><code>C:\ProgramData\Microsoft\Crypto\RSA\MachineKeys</code></td></tr></tbody></table>

<figure><img src="../../.gitbook/assets/image (1514).png" alt="Private Key Filename" width="563"><figcaption></figcaption></figure>

To check whether the private key file exists and view its permissions, run the following in an elevated PowerShell session. Set $keyPath to the folder appropriate to your provider, replacing `UNIQUE_CONTAINER_NAME` with the value identified above.

```
$keyPath = 'C:\ProgramData\Microsoft\Crypto\Keys\UNIQUE_CONTAINER_NAME'

Get-Item -LiteralPath $keyPath -Force
Get-Acl -LiteralPath $keyPath | Format-List Owner, AccessToString
```

Use the following table to interpret the script’s output and determine the next troubleshooting step:

<table><thead><tr><th valign="top">Output</th><th valign="top">What it means</th></tr></thead><tbody><tr><td valign="top">File details followed by <code>Owner</code> and <code>AccessToString</code></td><td valign="top">The file exists, and the current account can read its permissions. Confirm the Publishing Service account has access.</td></tr><tr><td valign="top"><code>Cannot find path… because it does not exist</code></td><td valign="top">The file was not found at the specified path. Confirm the provider, folder, and filename.</td></tr><tr><td valign="top">An access-denied error</td><td valign="top">The current account cannot access the file or read its permissions. This alone does not confirm the file is missing.</td></tr></tbody></table>

### Optional: Check the Private Key Using PowerShell

Run the following script in an elevated PowerShell session on the Publisher server. Replace $cert with the signing certificate’s thumbprint and set $store to its **Local Computer** certificate store: `My` for Personal, or `WSUS`.

The script attempts to open the private key, identify its filename, and display the file’s location and permissions.

```
# Enter the signing certificate's thumbprint and Local Computer store.
$cert  = 'YOUR_CERTIFICATE_THUMBPRINT'
$store = 'My' # Use 'My' for Personal or 'WSUS' for the WSUS store.

$rsa = $null

try {
    $certificate = Get-Item "Cert:\LocalMachine\$store\$cert" -ErrorAction Stop

    if (!$certificate.HasPrivateKey) {
        throw 'Certificate has no private-key association.'
    }

    $rsa = [System.Security.Cryptography.X509Certificates.RSACertificateExtensions]::GetRSAPrivateKey($certificate)

    $keyName = switch ($rsa) {
        { $_ -is [System.Security.Cryptography.RSACng] } {
            $_.Key.UniqueName
            break
        }
        { $_ -is [System.Security.Cryptography.RSACryptoServiceProvider] } {
            $_.CspKeyContainerInfo.UniqueKeyContainerName
            break
        }
    }

    if (!$keyName) {
        throw 'Unable to identify an RSA key filename.'
    }

    foreach ($folder in 'Keys', 'RSA\MachineKeys') {
        $path   = "$env:ProgramData\Microsoft\Crypto\$folder\$keyName"
        $status = 'Found'
        $acl    = ''

        try {
            $null = Get-Item -LiteralPath $path -Force -ErrorAction Stop

            try {
                $acl = (Get-Acl -LiteralPath $path -ErrorAction Stop).AccessToString
            }
            catch {
                $acl = "Cannot read ACL: $($_.Exception.Message)"
            }
        }
        catch {
            $status = switch ($_.CategoryInfo.Category) {
                'ObjectNotFound' {
                    'Not found'
                }
                'PermissionDenied' {
                    'Access denied; existence unconfirmed'
                }
                default {
                    $_.Exception.GetBaseException().Message
                }
            }
        }

        [pscustomobject]@{
            Path   = $path
            Status = $status
            ACL    = $acl
        } | Format-List
    }
}
catch {
    Write-Warning $_.Exception.GetBaseException().Message
}
finally {
    if ($rsa) {
        $rsa.Dispose()
    }
}
```

Use the following table to interpret the results:

<table><thead><tr><th valign="top">Output</th><th valign="top">What it means</th></tr></thead><tbody><tr><td valign="top"><code>Status : Found</code> with ACL entries</td><td valign="top">The file exists, and the current account can read its permissions. Confirm the Publishing Service account has access.</td></tr><tr><td valign="top"><code>Status : Not found</code></td><td valign="top">No file was found at that path. The script checks both folders; a <code>Not found</code> result for the unused folder is expected.</td></tr><tr><td valign="top"><code>Status : Access denied; existence unconfirmed</code></td><td valign="top">The current account cannot check the file’s presence.</td></tr><tr><td valign="top"><code>Cannot read ACL</code></td><td valign="top">The file was found, but its permissions could not be read.</td></tr><tr><td valign="top"><code>WARNING: Certificate has no private-key association.</code></td><td valign="top">Windows does not report a private-key association for this certificate.</td></tr><tr><td valign="top"><code>WARNING: Invalid provider type specified.</code></td><td valign="top">Windows could not open the key through its configured provider. The script stops before checking the file. This does not distinguish a missing file from a permissions or provider issue.</td></tr><tr><td valign="top"><code>WARNING: Cannot find path 'Cert:\LocalMachine\My\…' because it does not exist.</code></td><td valign="top">The certificate was not found in the specified store. Verify $cert and $store, and run the script on the Publisher server. This error occurs before the private key is checked.</td></tr></tbody></table>

{% hint style="info" %}
**Note**

**T**he script checks access using your current account. Successful results do not confirm that the Publishing Service account can use the private key.
{% endhint %}

## Repair a Missing Private Key Association

If the matching private key still exists on the server but its association with the certificate is missing, run the following from an elevated PowerShell session:

```
$cert  = '08B3DB3AAD4144D9E838452DF939D40CE5657465'
$store = 'My' # My = Personal; or WSUS

certutil.exe -repairstore $store $cert
```

This attempts to associate the certificate with an existing matching private key. It cannot restore a deleted key.

## Restore a Missing Private Key

If the private key is missing, re-import the original certificate and private key from a **PFX backup** using the appropriate certificate import workflow.

A `.cer` file contains the public certificate and cannot restore the private key.

If no backup is available, configure a replacement code signing certificate with an accessible private key.

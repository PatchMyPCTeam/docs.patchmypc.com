# Troubleshoot Content Repositories in  Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

When Patch My PC (PMPC) Publisher cannot use a file from the Staged Content Repository, it provides clear indicators through alerts and logging. The behavior depends on whether the file is missing entirely or present but does not match the expected file hash value defined in the Patch My PC catalog.

## Missing Installer File

If the required installer file is **not present** in the Staged Content Repository using the expected file name, publishing for that product fails. This failure is recorded in the **PatchMyPC.log**, indicating that the installer file could not be located. For example:

> Cisco Jabber 12 12.9.7.57303 requires a manual download of CiscoJabberSetup.msi. Please see https://patchmypc.com/licensed-download for the resolution.

When notifications are configured on the [Alerts tab](../../patch-my-pc-publisherv2/administration/alerts/), additional notifications are generated to highlight the issue.

An email notification is sent listing the product that failed and the exact installer file name expected:

<figure><img src="../../.gitbook/assets/image (3940).png" alt="Email Notification when a file is missing from the Local Content Repository" width="563"><figcaption></figcaption></figure>

A webhook notification is sent with the same details if webhook alerts are enabled:

<figure><img src="../../.gitbook/assets/image (3937).png" alt="Webhook Notification when a file is missing from the Local Content Repository" width="563"><figcaption></figcaption></figure>

## File Present but the Hash Does Not Match

If the installer file is present, but the file hash does not match the value defined in the Patch My PC catalog, Publisher does not consume the file and publishing fails for that product. This failure is recorded in the **PatchMyPC.log**, indicating that the installer file could not be located. For example:

> The digest of the local content file does not match the expected one. Please ensure the latest version of Cisco Jabber 12 12.9.7.57303 is present in the configured local content repository. FileRetriever 2/1/2026 1:12:22 PM 128 (0x0080)\\
>
> \
> Actual digest: \[zIwSblbgxSYSAMzQg2jGmmV6cOc=], expected digest: \[iV2Xx6Ap9T2LMoQZMrfM4slExNw=] FileRetriever 2/1/2026 1:12:22 PM 128 (0x0080)

When notifications are configured on the [Alerts tab](../../patch-my-pc-publisherv2/administration/alerts/), additional notifications are generated to highlight the issue.

An email notification is sent listing the product that failed and the exact installer file name expected:

<figure><img src="../../.gitbook/assets/image (3939).png" alt="Email Notification when a file is present but has the wrong file hash in the Local Content Repository" width="563"><figcaption></figcaption></figure>

A webhook notification is sent with the same details if webhook alerts are enabled:

<figure><img src="../../.gitbook/assets/image (3941).png" alt="Webhook Notification when a file is present but has the wrong file hash in the Local Content Repository" width="563"><figcaption></figcaption></figure>

## Base64 Digest Hash for Local Content Repository Validation

When Publisher reports a digest value in email alerts, webhook notifications, or the **PatchMyPC.log**, the value mismatch is shown in the **PatchMyPC.log** as a base64 encoded SHA1 digest.

For example:

> Actual digest: \[zIwSblbgxSYSAMzQg2jGmmV6cOc=], expected digest: \[iV2Xx6Ap9T2LMoQZMrfM4slExNw=]

Although the `Get-FileHash` PowerShell cmdlet is commonly used to review file hashes, it defaults to SHA256, the Publisher uses a base64 encoded SHA1 hash when validating installer binaries for the Local Content Repository

For example:

```powershell
Get-FileHash -Path "E:\LocalContent\Cisco Jabber\v2.0\CiscoJabberSetup.msi"
```

<figure><img src="../../.gitbook/assets/image (3943).png" alt="Get-FileHash PowerShell Cmdlet" width="563"><figcaption></figcaption></figure>

We must convert that SHA1 hex hash into a base64 digest to compare with the Publisher output. A simple PowerShell function can be used for this purpose

```powershell
function Get-Base64DigestFromFile {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory)]
        [string]$Path,

        [ValidateSet("SHA1","SHA256","SHA384","SHA512","MD5")]
        [string]$Algorithm = "SHA1"
    )

    # Get hex hash (e.g. "A1B2C3...")
    $hex = (Get-FileHash -Path $Path -Algorithm $Algorithm).Hash

    # Convert hex string to byte array, then to base64
    $bytes = for ($i = 0; $i -lt $hex.Length; $i += 2) {
        [Convert]::ToByte($hex.Substring($i, 2), 16)
    }

    [Convert]::ToBase64String($bytes)
}
```

Example Usage:

```powershell
Get-Base64DigestFromFile -Path "E:\LocalContent\Cisco Jabber\v2.0\CiscoJabberSetup.msi"
```

<figure><img src="../../.gitbook/assets/image (3944).png" alt="Get-Base64DigestFromFile Function" width="563"><figcaption></figcaption></figure>

After you calculate the base64 SHA1 digest for the installer file, compare it to the values shown in **PatchMyPC.log** to confirm whether the correct binary is present in the Staged Content Repository.

If the file is correct, the value you calculate should match the expected digest shown in the log. If it does not match, Publisher has detected that the file does not match the catalog definition for that product and version.

## CDN Latency and Hash Mismatch Considerations

In some scenarios involving software vendor websites or content delivery networks (CDNs), an installer may be downloaded from the expected URL but still result in a hash mismatch during publishing.

This can occur when a CDN temporarily serves different versions of the same file due to:

* Replication latency across CDN nodes
* Regional caching behavior
* Ongoing vendor-side update rollouts.

This behavior is outside the control of Publisher.

If you encounter a hash mismatch and are confident the installer was obtained from the correct vendor source, the recommended action is to retry the download at a later time. Once the CDN has fully synchronized and is serving consistent content, the downloaded file typically matches the expected digest and publishing succeeds.

This scenario is most commonly observed shortly after a vendor releases a new version of an application.

## Compressed Installers

Some software vendors distribute installers in compressed formats, such as ZIP or other archive files, rather than providing a direct EXE or MSI.

In some cases, Publisher does support compressed installers, but administrators should always refer to the catalog details to understand which file is expected.

Before understanding if a file needs to be extracted, use the Product Tree to confirm the required installer format:

1. Locate the product in the WSUS Updates, ConfigMgr Apps, or Intune Apps/Updates tab.
2. Right-click the product.
3. Select **Show package info: title, command-line, download URL, etc**.
4. Review the **File** field in the **Package Details** window for the expected file name.

If the catalog expects an EXE or MSI, download the compressed installer and extract the required EXE or MSI into the Staged Content Repository.

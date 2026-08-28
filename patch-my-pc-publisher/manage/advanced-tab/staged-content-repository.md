# Staged Content Repository section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Staged Content Repository** section on the **Advanced** tab of Patch My PC (PMPC) Publisher, allows Publisher to store update and application content locally instead of downloading it directly from the internet during publishing. This is primarily used for binary-free and licensed applications, where customers must obtain the installer or update binaries themselves because the content is behind a paywall, login, or other restricted access and is not publicly available.

<figure><img src="../../../.gitbook/assets/image (738).png" alt="&#x27;Staged Content Repository&#x27; section" width="563"><figcaption></figcaption></figure>

The **Staged Content Repository** can also be used as a fallback mechanism to improve reliability during publishing, such as recovering from download failures or preventing hash mismatches. In environments where outbound access to specific vendor websites or CDNs is restricted, customers can download the required binaries from another machine with internet access and place them into the Local Content Repository for the Publisher to consume during publishing.

## Video Walkthrough

For a visual walkthrough of configuring and using the Local Content Repository in the Publisher, including handling manual downloads and installer validation, see the following video:

{% embed url="https://youtu.be/OvkGR_Gh4kY" %}

## Scenarios that require the Staged Content Repository

The **Staged Content Reposito**ry is commonly used for **licensed or restricted applications** where the Publisher cannot automatically download installer binaries. In these scenarios, administrators must manually obtain the installer files and place them into the repository so the Publisher can consume them during publishing.

Common reasons include:

* The software vendor uses a paywalled portal that requires authentication to download installers.
* The vendor provides the installer in a file format that is not compatible with the Patch My PC Publisher download or extraction process.
* Legal, licensing, or EULA restrictions prohibit automated downloads by third-party tools.
* The vendor enforces technical controls on their website that block automated or scripted downloads.
* Organizational security policies restrict access to specific vendor sites or CDNs from the Publisher server.

To work around these limitations, administrators can download the required installer binaries from a separate machine with appropriate access and place them into the Local Content Repository. During publishing, the Publisher uses the locally staged files instead of attempting to download content directly from the vendor.

For a list of applications that require manual downloads and detailed guidance, see the following knowledge base article: [https://patchmypc.com/kb/local-content-repository-licensed-applications/](https://patchmypc.com/kb/local-content-repository-licensed-applications/)

This approach ensures publishing can continue reliably while remaining compliant with vendor and organizational constraints.

## How the Staged Content Repository Works

Products that require manual downloads, often referred to as _binary free_, are identified in the product tree by a manual download icon (![Manual download icon](<../../../.gitbook/assets/image (740).png>)) on the following tabs:

* WSUS Updates
* ConfigMgr Apps
* Intune Apps
* Intune Updates

When this icon is present, Publisher will search the configured Local Content Repository path for the required installer during publishing.

## How to Configure the Staged Content Repository

To configure the Local Content Repository, you must specify a folder that the Publisher will use to locate installer binaries for products that require manual downloads.

### Configure the Content Path

1. Open the Publisher and navigate to the **Advanced** tab.
2. Locate the **Staged Content Repository** section.
3. In the **Content Path** field, specify a local folder or UNC path where installer files will be stored.
4. Click **Apply**.\
   \
   The name of the server where the **PatchMyPCService** is installed is shown under this field.

{% hint style="danger" %}
**Important**

If you use a UNC path, ensure the computer account of the server running the Publishing Service has read and modify permissions to the share.
{% endhint %}

If the folder configured in Step 3 does not exist, the following warning is displayed:

**The folder does not exist. Continuing will create it when the settings are saved.**

### Folder Structure in the Staged Content Repository

The folder structure within the Staged Content Repository is flexible and does not need to follow a specific layout. Publisher recursively searches all subfolders when locating installer content.

When evaluating files in the repository, the Publisher validates only:

* The installer file name
* The file hash matching the Patch My PC catalog

The physical folder location of the file is not considered.

Some software vendors reuse the same installer file name across multiple versions. In these cases, administrators may want to retain older binaries for manual rollback, auditing, or troubleshooting purposes.

To support this, you can organize the repository using versioned subfolders, such as:

* Product name
* Product version

<figure><img src="../../../.gitbook/assets/image (3936).png" alt="Example Local Content Repository Folder Layout" width="563"><figcaption></figcaption></figure>

This structure is fully supported and does not affect publishing, as long as the correct installer file exists somewhere in the repository and matches the expected file name and hash.

### Populate the Repository

After configuring the Staged Content Repository path, manually download the required installer files for products that require manual downloads.

Place the installer files anywhere within the configured Staged Content Repository, including the root folder or any subfolders. Publisher recursively searches the entire folder structure during publishing.

The installer file name and version must exactly match the values defined in the PMPC catalog. If the file name or version does not match, Publisher _will not_ consume the file and publishing will fail for that product.

To identify the correct installer file name and version, use the Product Tree:

1. Locate the product in the relevant tab (WSUS Updates, ConfigMgr Apps, or Intune Apps/Updates).
2. Right-click the product.
3. Select **Show Package Info**
4. On the **Package Details** screen, review the **Title** and **File** columns to confirm the expected installer file name and version.

<figure><img src="../../../.gitbook/assets/image (3934).png" alt="Review the Title and File column in the Package Details window" width="563"><figcaption></figcaption></figure>

If the file is not found or does not match the catalog definition, the product will be skipped, and a notification is generated.

{% hint style="danger" %}
**Important**

Enabling Email Notifications or Webhook Notifications is strongly recommended, as these alerts include the exact installer name and file hash expected when manual action is required.
{% endhint %}

## Optional Settings

The following options further control repository behavior.

### Set to Default

Clicking **Set to Default** automatically configures the Staged Content Repository path to Publisher's installation folder. For example:

```
C:\Program Files\Patch My PC\Patch My PC Publishing Service\LocalContentRepository
```

This provides a ready-to-use local folder for storing manually downloaded installer content without requiring any additional configuration. The default path is dynamically resolved from the Publisher installation **Path** value stored in the following registry location:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Patch My PC Publishing Service
```

### Upload Files

Click the **Upload Files** button to upload files to the Staged Content Repository, which is limited to the following file types:

* EXE
* MSI
* MSP
* ZIP

{% hint style="info" %}
**Note**

This feature is available in both the local and Remote UI.
{% endhint %}

### Delete the update file in the local repository after publishing

Removes the installer file from the repository after it has been successfully published. This helps reduce disk usage but requires re-downloading the file if the update is republished.

### Check the local content repository for content files before attempting to download content files from the internet

When enabled, the Publisher checks the Local Content Repository first before attempting to download content from the internet.

This option is useful in restricted network environments where access to vendor download locations or CDNs is blocked, limited, or requires authentication that cannot be satisfied by the Publisher.

If a matching installer file is found in the Local Content Repository, it is used for publishing and no online download is attempted.

## Troubleshooting the Local Content Repository

When the Publisher cannot use a file from the Local Content Repository, it provides clear indicators through alerts and logging. The behavior depends on whether the file is missing entirely or present but does not match the expected file hash value defined in the Patch My PC catalog.

### Missing Installer File

If the required installer file is **not present** in the Local Content Repository using the expected file name, publishing for that product fails. This failure is recorded in the **PatchMyPC.log**, indicating that the installer file could not be located. For example:

> Cisco Jabber 12 12.9.7.57303 requires a manual download of CiscoJabberSetup.msi. Please see https://patchmypc.com/licensed-download for the resolution.

When notifications are configured on the [Alerts tab](../../../patch-my-pc-publisherv2/administration/alerts/), additional notifications are generated to highlight the issue.

An email notification is sent listing the product that failed and the exact installer file name expected:

<figure><img src="../../../.gitbook/assets/image (3940).png" alt="Email Notification when a file is missing from the Local Content Repository" width="563"><figcaption></figcaption></figure>

A webhook notification is sent with the same details if webhook alerts are enabled:

<figure><img src="../../../.gitbook/assets/image (3937).png" alt="Webhook Notification when a file is missing from the Local Content Repository" width="563"><figcaption></figcaption></figure>

### File Present but the Hash Does Not Match

If the installer file is present, but the file hash does not match the value defined in the Patch My PC catalog, the Publisher does not consume the file and publishing fails for that product. This failure is recorded in the PatchMyPC.log, indicating that the installer file could not be located. For example:

> The digest of the local content file does not match the expected one. Please ensure the latest version of Cisco Jabber 12 12.9.7.57303 is present in the configured local content repository. FileRetriever 2/1/2026 1:12:22 PM 128 (0x0080)\\
>
> \
> Actual digest: \[zIwSblbgxSYSAMzQg2jGmmV6cOc=], expected digest: \[iV2Xx6Ap9T2LMoQZMrfM4slExNw=] FileRetriever 2/1/2026 1:12:22 PM 128 (0x0080)

When notifications are configured on the [Alerts tab](../../../patch-my-pc-publisherv2/administration/alerts/), additional notifications are generated to highlight the issue.

An email notification is sent listing the product that failed and the exact installer file name expected:

<figure><img src="../../../.gitbook/assets/image (3939).png" alt="Email Notification when a file is present but has the wrong file hash in the Local Content Repository" width="563"><figcaption></figcaption></figure>

A webhook notification is sent with the same details if webhook alerts are enabled:

<figure><img src="../../../.gitbook/assets/image (3941).png" alt="Webhook Notification when a file is present but has the wrong file hash in the Local Content Repository" width="563"><figcaption></figcaption></figure>

### Base64 Digest Hash for Local Content Repository Validation

When the Publisher reports a digest value in email alerts, webhook notifications, or the PatchMyPC.log, the value mismatch is shown in the **PatchMyPC.log** as a base64 encoded SHA1 digest.

For example:

> Actual digest: \[zIwSblbgxSYSAMzQg2jGmmV6cOc=], expected digest: \[iV2Xx6Ap9T2LMoQZMrfM4slExNw=]

Although the `Get-FileHash` PowerShell cmdlet is commonly used to review file hashes, it defaults to SHA256, the Publisher uses a base64 encoded SHA1 hash when validating installer binaries for the Local Content Repository

For example:

```powershell
Get-FileHash -Path "E:\LocalContent\Cisco Jabber\v2.0\CiscoJabberSetup.msi"
```

<figure><img src="../../../.gitbook/assets/image (3943).png" alt="Get-FileHash PowerShell Cmdlet" width="563"><figcaption></figcaption></figure>

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

<figure><img src="../../../.gitbook/assets/image (3944).png" alt="Get-Base64DigestFromFile Function" width="563"><figcaption></figcaption></figure>

After you calculate the base64 SHA1 digest for the installer file, compare it to the values shown in **PatchMyPC.log** to confirm whether the correct binary is present in the Local Content Repository.

If the file is correct, the value you calculate should match the expected digest shown in the log. If it does not match, the Publisher has detected that the file does not match the catalog definition for that product and version.

### CDN Latency and Hash Mismatch Considerations

In some scenarios involving software vendor websites or content delivery networks (CDNs), an installer may be downloaded from the expected URL but still result in a hash mismatch during publishing.

This can occur when a CDN temporarily serves different versions of the same file due to:

* Replication latency across CDN nodes
* Regional caching behavior
* Ongoing vendor-side update rollouts

This behavior is outside the control of the Publisher.

If you encounter a hash mismatch and are confident the installer was obtained from the correct vendor source, the recommended action is to retry the download at a later time. Once the CDN has fully synchronized and is serving consistent content, the downloaded file typically matches the expected digest and publishing succeeds.

This scenario is most commonly observed shortly after a vendor releases a new version of an application.

### Compressed Installers

Some software vendors distribute installers in compressed formats, such as ZIP or other archive files, rather than providing a direct EXE or MSI.

In some cases, the Publisher does support compressed installers, but administrators should always refer to the catalog details to understand what file is expected.

Before understanding if a file needs to be extracted, use the Product Tree to confirm the required installer format:

1. Locate the product in the Updates, ConfigMgr Apps, or Intune Apps/Updates tab.
2. Right click the product.
3. Select **Show package info: title, command-line, download URL, etc**.
4. Review the File field in the Package Details window for the expected file name.

If the catalog expects an EXE or MSI, download the compressed installer and extract the required EXE or MSI into the Local Content Repository.

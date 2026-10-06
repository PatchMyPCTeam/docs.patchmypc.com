---
hidden: true
---

# Content Repositories category of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Content Repositories** category on the **Advanced** tab of Patch My PC (PMPC) Publisher allows you to configure where Publisher stores update and application content locally instead of downloading it directly from the internet during publishing. This is primarily used for binary-free and licensed applications, where customers must obtain the installer or update binaries themselves because the content is behind a paywall, login, or other restricted access and is not publicly available.

<figure><img src="../../../.gitbook/assets/image (1364).png" alt="&#x27;Content Repositories&#x27; category" width="506"><figcaption></figcaption></figure>

There are two main sections on this screen:

* [Staged Content Repository](content-repositories.md#staged-content-repository)
* [Additional Content Repository](content-repositories.md#additional-content-repository)

## Staged Content Repository

The **Staged Content Repository** can also be used as a fallback mechanism to improve reliability during publishing, such as recovering from download failures or preventing hash mismatches. In environments where outbound access to specific vendor websites or CDNs is restricted, customers can download the required binaries from another machine with internet access and place them into the Local Content Repository for the Publisher to consume during publishing.







## Additional Content Repository



\*\*\*\*\*\*\*

<figure><img src="../../../.gitbook/assets/image (738).png" alt="&#x27;Staged Content Repository&#x27; section" width="563"><figcaption></figcaption></figure>



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

### Delete after publishing

Removes the installer file from the repository after it has been successfully published. This helps reduce disk usage but requires re-downloading the file if the update is republished.

### Check repository first

When enabled, the Publisher checks the Local Content Repository first before attempting to download content from the internet.

This option is useful in restricted network environments where access to vendor download locations or CDNs is blocked, limited, or requires authentication that cannot be satisfied by the Publisher.

If a matching installer file is found in the Local Content Repository, it is used for publishing and no online download is attempted.


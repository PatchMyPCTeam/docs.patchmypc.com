---
hidden: true
---

# Content Repositories category of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Content Repositories** category on the **Advanced** tab of Patch My PC (PMPC) Publisher allows you to configure where Publisher stores update and application content instead of downloading it directly from the internet during publishing. This is primarily used for binary-free and licensed applications, where customers must obtain the installer or update binaries themselves because the content is behind a paywall, login, or other restricted access and is not publicly available.

<figure><img src="../../../.gitbook/assets/image (1403).png" alt="&#x27;Content Repositories&#x27; category" width="563"><figcaption></figcaption></figure>

There are two main sections on this screen:

* [Staged Content Repository](content-repositories.md#staged-content-repository)
* [Additional Content Repository](content-repositories.md#additional-content-repository)

## Staged Content Repository

The **Staged Content Repository** can also be used as a fallback mechanism to improve reliability during publishing, such as recovering from download failures or preventing hash mismatches. In environments where outbound access to specific vendor websites or CDNs is restricted, customers can download the required binaries from another machine with internet access and place them into the Staged Content Repository for the Publisher to consume during publishing.

### To configure the Staged Content Repository

1. Load Publisher.
2. Navigate to **Advanced | Content Repositories**.
3. In the **Content path** field, specify/browse to a folder or UNC path where installer files will be stored.

<figure><img src="../../../.gitbook/assets/image (1366).png" alt="&#x27;Content path&#x27; field" width="496"><figcaption></figcaption></figure>

Underneath this field the name of the server where the **PatchMyPCService** is installed is shown.

{% hint style="danger" %}
**Important**

If you use a UNC path, ensure the computer account of the server running the Publishing Service has read and modify permissions to the share.
{% endhint %}

4. Click **Apply**.\
   \
   If the folder configured in Step 3 does not exist, the following warning is displayed:\
   \
   **The folder does not exist. Continuing will create it when the settings are saved.**

{% hint style="info" %}
**Note**

See [Populate the Staged Content Repository](content-repositories.md#populate-the-staged-content-repository) for more details on populating the Staged Content Repository.
{% endhint %}

### Set to Default button&#x20;

Clicking **Set to Default** automatically configures the Staged Content Repository path to Publisher's installation folder. For example:

```
C:\Program Files\Patch My PC\Patch My PC Publishing Service\LocalContentRepository
```

This provides a ready-to-use local folder for storing manually downloaded installer content without requiring any additional configuration. The default path is dynamically resolved from Publisher's installation **Path** value stored in the following registry location:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Patch My PC Publishing Service
```

### Upload Files button

Clicking **Upload Files** allows you yo to upload files to the Staged Content Repository, which is limited to the following file types:

* EXE
* MSI
* MSP
* ZIP

{% hint style="info" %}
**Note**

This feature is available in both the local and Remote UI.
{% endhint %}

### Show Staged Content button

Clicking **Show Staged Content** opens the **Files in the service Staged Content Repository** screen, which displays all of the files currently in the Staged Content Repository.

<figure><img src="../../../.gitbook/assets/image (1365).png" alt="&#x27;Files in the service Staged Content Repository&#x27; screen" width="563"><figcaption></figcaption></figure>

### Delete after publishing

Enabling the **Delete after publishing** option (which is disabled by default) removes the installer file from the repository after it has been successfully published. This helps reduce disk usage but requires re-downloading the file if the update is republished.

<figure><img src="../../../.gitbook/assets/image (1367).png" alt="&#x27;Delete after publishing&#x27; option" width="502"><figcaption></figcaption></figure>

### Check repository first

When the **Check repository first** option is enabled (which it is by default) Publisher checks the Staged Content Repository first before attempting to download content from the internet.

<figure><img src="../../../.gitbook/assets/image (1368).png" alt="&#x27;Check repository first&#x27; option" width="502"><figcaption></figcaption></figure>

This option is useful in restricted network environments where access to vendor download locations or CDNs is blocked, limited, or requires authentication that cannot be satisfied by Publisher.

If a matching installer file is found in the Staged Content Repository, it is used for publishing and no online download is attempted.

### Populate the Staged Content Repository

After configuring the Staged Content Repository path, manually download the required installer files for products that require manual downloads.

Place the installer files anywhere within the configured Staged Content Repository, including the root folder or any subfolders. Publisher recursively searches the entire folder structure during publishing.

The installer file name and version must exactly match the values defined in the PMPC catalog. If the file name or version does not match, Publisher _will not_ consume the file and publishing will fail for that product.

#### To identify the correct installer file name and version

1. Locate the product in the relevant Product Tree (**WSUS Updates**, **ConfigMgr Apps**, or **Intune Apps/Updates**).
2. Right-click the product and select **Show Package Info**
3. On the **Package Details** screen, review the **Title** and **File** columns to confirm the expected installer file name and version.

<figure><img src="../../../.gitbook/assets/image (3934).png" alt="&#x27;Package Details&#x27; screen" width="563"><figcaption></figcaption></figure>

If the file is not found or does not match the catalog definition, the product will be skipped, and a notification is generated.

{% hint style="danger" %}
**Important**

Enabling Email Notifications or Webhook Notifications is strongly recommended, as these alerts include the exact installer name and file hash expected when manual action is required.
{% endhint %}

## Additional Content Repository

The **ADDITIONAL CONTENT REPOSITORY** section allows you to configure a service-side folder for pre/post scripts and extra files a remote Ul attaches to a product.

<figure><img src="../../../.gitbook/assets/image (1369).png" alt="&#x27;ADDITIONAL CONTENT REPOSITORY&#x27; section" width="500"><figcaption></figcaption></figure>

# About the Staged Content Repository in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Staged Content Reposito**ry is commonly used for licensed or restricted applications where Publisher cannot automatically download installer binaries. In these scenarios, administrators must manually obtain the installer files and place them into the repository so Publisher can consume them during publishing.

Common reasons include:

* The software vendor uses a paywalled portal that requires authentication to download installers.
* The vendor provides the installer in a file format that is not compatible with Publisher's download or extraction process.
* Legal, licensing, or EULA restrictions prohibit automated downloads by third-party tools.
* The vendor enforces technical controls on their website that block automated or scripted downloads.
* Organizational security policies restrict access to specific vendor sites or CDNs from the Publisher server.

To work around these limitations, administrators can download the required installer binaries from a separate machine with appropriate access and place them into the Staged Content Repository.&#x20;

During publishing, Publisher uses the locally staged files instead of attempting to download content directly from the vendor.

This approach ensures publishing can continue reliably while remaining compliant with vendor and organizational constraints.

{% hint style="info" %}
**Note**

See [Local Content Repository for Licensed Applications that Require Manual Download](https://patchmypc.com/kb/local-content-repository-licensed-applications/) for a list of applications that require manual downloads and detailed guidance.
{% endhint %}

## How the Staged Content Repository Works

Products requiring manual download (often referred to as _binary-free_) are identified in the Product Tree by a manual download icon (![Manual download icon](<../../../../.gitbook/assets/image (740).png>)) on the following tabs:

* **WSUS Updates**
* **ConfigMgr Apps**
* **Intune Apps**
* **Intune Updates**

When this icon is present, Publisher will search the configured Staged Content Repository path for the required installer during publishing.

## Folder Structure in the Staged Content Repository

The folder structure within the Staged Content Repository is flexible and does not need to follow a specific layout. Publisher recursively searches all subfolders when locating installer content.

When evaluating files in the repository, Publisher validates only:

* The installer file name.
* The file hash matching the Patch My PC catalog.

The physical folder location of the file is not considered.

Some software vendors reuse the same installer file name across multiple versions. In these cases, administrators may want to keep older binaries for manual rollback, auditing, or troubleshooting purposes.

To support this, you can organize the repository using versioned subfolders, such as:

* Product name
* Product version

<figure><img src="../../../../.gitbook/assets/image (3936).png" alt="Example Local Content Repository Folder Layout" width="563"><figcaption></figcaption></figure>

This structure is fully supported and does not affect publishing, as long as the correct installer file exists somewhere in the repository and matches the expected file name and hash.

# Create a Self-Signed Certificate in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Create Self-Signed** certificate option allows Patch My PC (PMPC) Publisher to create a code-signing certificate.

This option is commonly used when you do not want Microsoft ConfigMgr to manage the certificate, or in standalone WSUS environments where self-signed certificates are permitted and a Certificate Authority is not available.

## Create a Self-Signed Certificate

To create a self-signed code-signing certificate:

1. Load Publisher.
2. Navigate to **WSUS Updates | WSUS Options**.&#x20;
3. Under the **Certificate Management** section, click the **Create Self-Signed** button.

<figure><img src="../../../../../../.gitbook/assets/image (778).png" alt="Clicking the &#x27;Create-Self-Sgined&#x27; button under the &#x27;Certificate Management&#x27; section"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If Publisher detects an existing valid certificate, the **Overwrite Current Certificate** dialog is displayed, warning you and prompting you to click **Yes** to overwrite the existing certificate with the new one. This helps prevent you from accidentally replacing an active and trusted signing certificate.

![Overwrite Current Certificate](<../../../../../../.gitbook/assets/image (777).png>)
{% endhint %}

4. On the **WSUS Code Signing Certificate** screen, review and adjust the certificate options as required:
   1. **Subject** (Default: **PatchMyPC Service**)
   2. **Valid for** (Default: **5 years**)
   3. **Key length** (Default: 2048 **bits**)

<figure><img src="../../../../../../.gitbook/assets/image (779).png" alt="&#x27;WSUS Code Signing Certificate&#x27; screen" width="298"><figcaption></figcaption></figure>

5. Optionally, leave the **Disable Private Key Export** checkbox unchecked if you may need to move Publisher to another top-level Software Update Point (SUP) in the future and want to take the same code-signing certificate to the new server.
6. Click the **Generate** button.
7. If the certificate is created successfully, the **Certificate Created Successfully** dialog is shown, which you can close by clicking **OK.**

<figure><img src="../../../../../../.gitbook/assets/image (780).png" alt="&#x27;Certificate Created Successfully&#x27; dialog" width="464"><figcaption></figcaption></figure>

The **Certificate Management** section updates to show the certificate is valid and its expiry date.

<figure><img src="../../../../../../.gitbook/assets/image (781).png" alt="&#x27;Certificate Management&#x27; section updating" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

By default, the generated certificate’s **private key is marked as exportable**. This is intentional and recommended, as it allows the certificate (including the private key) to be exported and reused if the Publisher is later moved to a new top-level Software Update Point (SUP). Without an exportable private key, the same signing certificate could not be transferred to another server.
{% endhint %}

After generation, the self-signed certificate is automatically placed in the following **Local Machine** certificate stores on the server:

* **WSUS**\
  Used by Publisher, through the WSUS API, to sign third-party updates.
* **Trusted Publishers**\
  Allows the operating system to trust updates signed with this certificate.
* **Trusted Root Certification Authorities**\
  Required because the certificate is **self-signed** and does not chain back to a trusted Certificate Authority.

{% hint style="danger" %}
**Important**

As self-signed certificates do not have a parent Certificate Authority, they must be explicitly trusted to establish a valid trust chain. For environments using ConfigMgr or WSUS, this means the certificate must be trusted not only on the WSUS server, but also on **all devices that will install updates signed with the certificate**.

As a result, the self-signed certificate must be placed in the **Trusted Publishers** store (to allow installation of signed updates) and the **Trusted Root Certification Authorities** store (to establish trust for the signing certificate) on those devices.

When third-party updates are enabled for the SUP and in Client Settings, ConfigMgr can automatically distribute the signing certificate to managed devices, place it into the required certificate stores, and configure the necessary local Windows Update policies so the Windows Update Agent trusts that signing certificate.

This ensures client devices trust updates signed by a third-party code-signing certificate, rather than only updates signed by Microsoft, without requiring manual certificate deployment. See [ConfigMgr Client Setting Requirements](../../../../../requirements/configmgr-requirements/client-settings.md) for more information.
{% endhint %}

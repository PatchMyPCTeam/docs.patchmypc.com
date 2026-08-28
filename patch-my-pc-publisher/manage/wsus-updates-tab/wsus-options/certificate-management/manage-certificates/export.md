# Export Certificate in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Export** option in Patch My PC (PMPC) Publisher allows you to export the currently configured code-signing certificate to a file. This is typically used when the certificate needs to be distributed to client systems or manually trusted in additional certificate stores.

## Export a Certificate

To export a certificate:

1. Load Publisher.
2. Navigate to **WSUS Updates | WSUS Options**.&#x20;
3. Under the **Certificate Management** section, click the **Export** button.

<figure><img src="../../../../../../.gitbook/assets/image (773).png" alt="Clicking the &#x27;Export&#x27; button under the &#x27;Certificate Management&#x27; section" width="563"><figcaption></figcaption></figure>

4. Choose a name and location for the exported certificate and click **Save**.\
   \
   The **Export Complete** dialog is displayed to confirm the export, which you can close by clicking **OK**.

<figure><img src="../../../../../../.gitbook/assets/image (774).png" alt="&#x27;Export Complete&#x27; dialog" width="422"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

When exporting the certificate, Publisher saves it as a **`.cer`** file, which contains the **public portion of the certificate only**. The private key is **not exported**, even if the key is marked as exportable.
{% endhint %}

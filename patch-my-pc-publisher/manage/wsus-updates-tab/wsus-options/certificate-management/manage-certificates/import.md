# Import a Certificate in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Import** certificate option in Patch My PC (PMPC) Publisher allows you to import a code-signing certificate using a PFX file that includes the certificate's private key, which Publisher uses to sign content it publishes.

## Import a Certificate

To import a PFX certificate:

1. Load Publisher.
2. Navigate to **WSUS Updates | WSUS Options**.&#x20;
3. Under the **Certificate Management** section, click the **Import** button.

<figure><img src="../../../../../../.gitbook/assets/image (763).png" alt="Clicking the &#x27;Import&#x27; button under the &#x27;Certificate Management&#x27; section" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If Publisher detects an existing valid certificate, the **Overwrite Current Certificate** dialog is displayed, warning you and prompting you to click **Yes** to overwrite the existing certificate with the new one. This helps prevent you from accidentally replacing an active and trusted signing certificate.

![Overwrite Current Certificate](<../../../../../../.gitbook/assets/image (777).png>)
{% endhint %}

4. Browse to the location where the **.pfx** certificate is saved and click **Open**.
5. In the **Certificate password** field, enter the private key password and click **OK**.

<figure><img src="../../../../../../.gitbook/assets/image (775).png" alt="&#x27;Certificate password&#x27; field" width="388"><figcaption></figcaption></figure>

If the certificate is valid and suitable for code signing, the **Certificate Imported Successfully** dialog is shown, which you can close by clicking **OK**.

<figure><img src="../../../../../../.gitbook/assets/image (82).png" alt="&#x27;Certificate Imported Successfully&#x27; pop-up" width="444"><figcaption></figcaption></figure>

If the PFX certificate is unsuitable for code signing, the **Certificate Import Failed** dialog will indicate this.

<figure><img src="../../../../../../.gitbook/assets/image (4139).png" alt="Certificate unsuitable" width="317"><figcaption></figcaption></figure>

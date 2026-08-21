# Import a Certificate in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Import Certificate** option in Patch My PC (PMPC) Publisher allows you to import a code signing certificate using a PFX file that includes the certificate's private key, which Publisher uses to sign content it publishes.

## Import a PFX Certificate

To import a PFX certificate:

1. Load Publisher.
2. On the **General** tab, under the **Certificate Management** section, click the **Import** button.
3. Browse to the location where the **.pfx** certificate is saved and click **Open**.
4. Enter the password for the private key.

<figure><img src="../../../../../../.gitbook/assets/image (81).png" alt="Enter the PFX password" width="390"><figcaption></figcaption></figure>

5. Click **OK**.\
   \
   If the certificate is valid and suitable for code signing, the import completes successfully.

<figure><img src="../../../../../../.gitbook/assets/image (82).png" alt="Import was successful" width="444"><figcaption></figcaption></figure>

If the PFX certificate is unsuitable for code signing, the **Certificate Import Failed** dialog will indicate this.

<figure><img src="../../../../../../.gitbook/assets/image (4139).png" alt="Certificate unsuitable" width="317"><figcaption></figcaption></figure>

If Publisher detects an existing certificate that is still valid, the **Overwrite Current Certificate** dialog is displayed, warning you and prompting you to click **Yes** to overwrite the existing certificate with the new one. This helps prevent you from accidentally replacing an active and trusted signing certificate.

<figure><img src="../../../../../../.gitbook/assets/image (3915).png" alt="Overwrite Certificate Validation" width="328"><figcaption></figcaption></figure>

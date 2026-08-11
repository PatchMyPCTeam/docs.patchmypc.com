# Import a Certificate in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Import Certificate** option in Patch My PC (PMPC) Publisher allows you to import a code signing certificate using a PFX file that includes the certificate's private key, which Publisher uses to sign content it publishes.

## Import a PFX Certificate

To import a PFX certificate:

1. Load Publisher.
2. On the **General** tab, under the **Certificate Management** section, click the **Import** button.
3. Browse to the location where the **.pfx** certificate is saved and click **Open**.
4. Enter the password for the private key.

![Enter the PFX password](/_images/image-(81 "Enter the PFX password") (1).png>)

5. Click **OK**.\
   \
   If the certificate is valid and suitable for code signing, the import completes successfully.

![Import was successful](/_images/image-(82 "Import was successful") (1).png>)

If the PFX certificate is unsuitable for code signing, the **Certificate Import Failed** dialog will indicate this.

![Certificate unsuitable](/_images/image-(4139).png)

If Publisher detects an existing certificate that is still valid, the **Overwrite Current Certificate** dialog is displayed, warning you and prompting you to click **Yes** to overwrite the existing certificate with the new one. This helps prevent you from accidentally replacing an active and trusted signing certificate.

![Overwrite Certificate Validation](/_images/image-(3915).png)
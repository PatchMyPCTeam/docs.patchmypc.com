# Export Certificate in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Export** option in Patch My PC (PMPC) Publisher allows you to export the currently configured code-signing certificate to a file. This is typically used when the certificate needs to be distributed to client systems or manually trusted in additional certificate stores.

## Export a Certificate

To export a certificate:

1. Load Publisher.
2. On the **General** tab, under the **Certificate Management** section, click the **Export** button.
3. Choose a name and location for the certificate and click **Save**.\
   \
   The **Export Complete** dialog is displayed confirming the export.<br>

!['Export Complete' dialog](/_images/image-(4490).png)

> \*\*Note\*\*
>
> When exporting the certificate, Publisher saves it as a \*\*\`.cer\`\*\* file, which contains the \*\*public portion of the certificate only\*\*. The private key is \*\*not exported\*\*, even if the key is marked as exportable.
# Import PFX Certificate

_Applies to: Patch My PC Publisher V2.x_

The **Import PFX Certificate** option allows you to import a code signing certificate using a PFX file that includes the certificate private key. This certificate is used to sign content published by the Publisher.

When importing a new certificate, the Publisher checks whether an existing certificate is already configured. If the current certificate is still valid, you are prompted to confirm before it is replaced. This helps prevent accidental replacement of an active and trusted signing certificate.

<figure><img src="../../../../.gitbook/assets/image (420).png" alt="Import a PFX certificate" width="563"><figcaption></figcaption></figure>

When importing a new certificate, the Publisher will prompt you to confirm if an existing certificate is still valid, helping prevent accidental replacement of an active and trusted signing certificate.

<figure><img src="../../../../.gitbook/assets/image (3915).png" alt="Overwrite Certificate Validation" width="328"><figcaption></figcaption></figure>

To import a PFX certificate:

1. Click Import PFX Certificate
2. Browse to the location where the .pfx certificate is saved.
3. Click Open.
4. Enter the password for the private key

<figure><img src="../../../../.gitbook/assets/image (81).png" alt="Enter the PFX password" width="390"><figcaption></figcaption></figure>



5. Click **OK**.

If the certificate is valid and suitable for code signing, the import completes successfully.

<figure><img src="../../../../.gitbook/assets/image (82).png" alt="Import was succesful" width="444"><figcaption></figcaption></figure>

If the PFX certificate is not suitable for code signing operations, an error dialog will indicate that.

<figure><img src="../../../../.gitbook/assets/image (4139).png" alt="Certificate not suitable" width="317"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

When importing a new certificate, the Publisher will prompt you to confirm if an existing certificate is still valid, helping prevent accidental replacement of an active and trusted signing certificate.
{% endhint %}

# Import PFX Certificate

_Applies to: Patch My PC Publisher V2.x_

The **Import PFX Certificate** option allows you to import a code signing certificate using a PFX file that includes the certificate private key. This certificate is used to sign content published by the Publisher.

When importing a new certificate, the Publisher checks whether an existing certificate is already configured. If the current certificate is still valid, you are prompted to confirm before it is replaced. This helps prevent accidental replacement of an active and trusted signing certificate.

![Import a PFX certificate](<../../../../.gitbook/assets/image-(420) (1).png>)

When importing a new certificate, the Publisher will prompt you to confirm if an existing certificate is still valid, helping prevent accidental replacement of an active and trusted signing certificate.

![Overwrite Certificate Validation](../../../../.gitbook/assets/image-\(3915\).png)

To import a PFX certificate:

1. Click Import PFX Certificate
2. Browse to the location where the .pfx certificate is saved.
3. Click Open.
4. Enter the password for the private key

![Enter the PFX password](<../../../../.gitbook/assets/image-(81) (1).png>)

5. Click **OK**.

If the certificate is valid and suitable for code signing, the import completes successfully.

![Import was succesful](<../../../../.gitbook/assets/image-(82) (1).png>)

If the PFX certificate is not suitable for code signing operations, an error dialog will indicate that.

![Certificate not suitable](../../../../.gitbook/assets/image-\(4139\).png)

> \*\*Note\*\*
>
> When importing a new certificate, the Publisher will prompt you to confirm if an existing certificate is still valid, helping prevent accidental replacement of an active and trusted signing certificate.

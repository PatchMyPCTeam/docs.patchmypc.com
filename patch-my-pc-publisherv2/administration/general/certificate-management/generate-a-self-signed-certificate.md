# Generate a Self-Signed Certificate

_Applies to: Patch My PC Publisher V2.x_

The **Generate a Self-Signed Certificate** option allows Publisher to create a code-signing certificate. This option is commonly used when allowing ConfigMgr to manage the certificate is not desired, or in standalone WSUS environments where self-signed certificates are permitted and a Certificate Authority is not available.

![Generate a self-signed certificate](/_images/image-(3916).png)

> \*\*Note\*\*
>
> By default, the generated certificate’s \*\*private key is marked as exportable\*\*. This is intentional and recommended, as it allows the certificate (including the private key) to be exported and reused if the Publisher is later moved to a new top-level Software Update Point (SUP). Without an exportable private key, the same signing certificate could not be transferred to another server.

If a code-signing certificate is already configured, Publisher will prompt for confirmation before overwriting it, even if the existing certificate is still valid. This helps prevent accidental replacement of an active signing certificate.

Follow the steps below to generate a self-signed code-signing certificate:

1. Open the Patch My PC Publisher.
2. Navigate to **General > Generate a Self-Signed Certificate**.
3. Review or adjust the certificate options:
   * Subject (Default: PatchMyPC Service)
   * Validity period (Default: 5 years)
   * Key length (Default: 2048 btis)
4. (Optional) Leave **Disable Private Key Export** unchecked if you may need to move Publisher to another top-level SUP in the future and want to take the same code-singing certificate to the new server.
5. Select **Generate Certificate**.
6. If prompted to overwrite an existing certificate, confirm to proceed.

> \*\*Note\*\*
>
> After generation, the self-signed certificate is automatically placed in the following \*\*Local Machine\*\* certificate stores on the server:
>
> \* \*\*WSUS\*\*\\
>
> Used by the Publisher, through the WSUS API, to sign third-party updates.
>
> \* \*\*Trusted Publishers\*\*\\
>
> Allows the operating system to trust updates signed with this certificate.
>
> \* \*\*Trusted Root Certification Authorities\*\*\\
>
> Required because the certificate is \*\*self-signed\*\* and does not chain back to a trusted Certificate Authority.

> \*\*Important\*\*
>
> Because self-signed certificates do not have a parent Certificate Authority, they must be explicitly trusted to establish a valid trust chain. For environments using ConfigMgr or WSUS, this means the certificate must be trusted not only on the WSUS server, but also on \*\*all devices that will install updates signed with the certificate\*\*.
>
> As a result, the self-signed certificate must be placed in the \*\*Trusted Publishers\*\* store (to allow installation of signed updates) and the \*\*Trusted Root Certification Authorities\*\* store (to establish trust for the signing certificate) on those devices.
>
> When third-party updates are enabled for the Software Update Point and in Client Settings, ConfigMgr can automatically distribute the signing certificate to managed devices, place it into the required certificate stores, and configure the necessary local Windows Update policies so the Windows Update Agent trusts that signing certificate. This ensures client devices trust updates signed by a third-party code-signing certificate, rather than only updates signed by Microsoft, without requiring manual certificate deployment. See \[Client Settings]\(../../../publisher-requirements/configmgr-requirements/client-settings.md) for more information.
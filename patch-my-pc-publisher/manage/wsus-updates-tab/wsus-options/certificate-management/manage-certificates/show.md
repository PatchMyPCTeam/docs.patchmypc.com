# Show Certificate in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Show Certificate** option in Patch My PC (PMPC) Publisher displays detailed information about the code-signing certificate currently configured for use by Publisher.

This view allows you to verify that a valid certificate is selected, confirm its trust status, and ensure it meets the signing requirements of Microsoft WSUS and ConfigMgr.

## Show a Certificate

To show a certificate:

1. Load Publisher.
2. Navigate to **WSUS Updates | WSUS Options**.&#x20;
3. Under the **Certificate Management** section, click the **Show Certificate** button.

<figure><img src="../../../../../../.gitbook/assets/image (764).png" alt="Clicking the &#x27;Show Certificate&#x27; button under the &#x27;Certificate Management&#x27; section" width="563"><figcaption></figcaption></figure>

The **Certificate Information** dialog is shown, displaying the information in the table below.

<figure><img src="../../../../../../.gitbook/assets/image (771).png" alt="&#x27;Certificate Information&#x27; dialog" width="401"><figcaption></figcaption></figure>

<table><thead><tr><th width="196" valign="top">Field</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">Issuer</td><td valign="top">The authority that issued the certificate. This may be ConfigMgr, Publisher, or an internal/public Certificate Authority.</td></tr><tr><td valign="top">Subject</td><td valign="top">The identity the certificate was issued to.</td></tr><tr><td valign="top">Effective Date</td><td valign="top">The date and time from which the certificate is valid.</td></tr><tr><td valign="top">Expiration Date</td><td valign="top">The date and time the certificate expires.</td></tr><tr><td valign="top">Cert Usage</td><td valign="top">Indicates whether the certificate is valid for code-signing operations, which is required for publishing updates to WSUS and signing ConfigMgr detection method scripts.</td></tr><tr><td valign="top">Public Key</td><td valign="top">The cryptographic algorithm and key length used by the certificate (for example, RSA 2048-bit).</td></tr><tr><td valign="top">Thumbprint</td><td valign="top">A unique identifier for the certificate, useful for verification and troubleshooting.</td></tr><tr><td valign="top">Trusted Publisher</td><td valign="top">Confirms whether the certificate is trusted for publishing updates to WSUS.</td></tr><tr><td valign="top">Trusted Root Authority</td><td valign="top">Indicates whether the certificate chain is trusted by the local system and WSUS.</td></tr><tr><td valign="top">Self Signed</td><td valign="top">Indicates this is a self-signed certificate.</td></tr></tbody></table>

## Validate Trust Chain

Clicking **Validate Trust Chain** checks whether the certificate and its chain of trust are trusted by the local system.

<figure><img src="../../../../../../.gitbook/assets/image (772).png" alt="Clicking &#x27;Validate Trust Chain&#x27;" width="401"><figcaption></figcaption></figure>

This is a useful troubleshooting step if the publishing of updates fails due to certificate or trust-related errors.

<figure><img src="../../../../../../.gitbook/assets/image (3914).png" alt="Validate the certificate trust chain" width="300"><figcaption></figcaption></figure>

## Troubleshooting Certificates

If you receive an error when you click **Show Certificate**, use the steps in this section to identify the cause.

### No Certificate found in the WSUS Store on this Server

<figure><img src="../../../../../../.gitbook/assets/image (4266).png" alt="No Certificate foundin the WSUS Store on this Server" width="358"><figcaption></figcaption></figure>

If clicking **Show Certificate** displays **No certificate found in the WSUS store on this server**, review **PatchMyPC.log** for related certificate extraction errors.&#x20;

For example:

`An error occurred while extracting the certificate from WSUS: C:\WINDOWS\SystemTemp\PMP-1d2xluld\jwpcs1ov.tmp : The request failed with HTTP status 503: Service Unavailable. CertManager 18/04/2026 12:12:54 34 (0x0022)`\
`Failed to extract the certificate from WSUS CertManager 18/04/2026 12:12:54 34 (0x0022)`

Verify that the WSUS Application Pool is started in IIS, then retry the action.

<figure><img src="../../../../../../.gitbook/assets/image (4267).png" alt="Verify that the WSUS Application Pool is started in IIS, then retry the action." width="563"><figcaption></figcaption></figure>

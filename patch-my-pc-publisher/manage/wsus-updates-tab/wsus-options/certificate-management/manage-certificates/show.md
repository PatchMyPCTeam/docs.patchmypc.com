# Show Certificate in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This article has not been updated for Version 3.x. Once it has, this banner will be removed.</p>
</blockquote>

The **Show Certificate** option in Patch My PC (PMPC) Publisher displays detailed information about the code-signing certificate currently configured for use by Publisher.

This view allows you to verify that a valid certificate is selected, confirm its trust status, and ensure it meets the signing requirements of Microsoft WSUS and ConfigMgr.

## Show a Certificate

To show a certificate:

1. Load Publisher.
2. On the **General** tab, under the **Certificate Management** section, click the **Show Certificate** button.\
   \
   The **Certificate Information** screen is shown, displaying the information in the table below.

!['Certificate Information' screen](/_images/image-(4487).png "&#x27;Certificate Information&#x27; screen")

<table><thead><tr><th width="196" valign="top">Field</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">Issuer</td><td valign="top">The authority that issued the certificate. This may be ConfigMgr, Publisher, or an internal/public Certificate Authority.</td></tr><tr><td valign="top">Subject</td><td valign="top">The identity the certificate was issued to.</td></tr><tr><td valign="top">Effective Date</td><td valign="top">The date and time from which the certificate is valid.</td></tr><tr><td valign="top">Expiration Date</td><td valign="top">The date and time the certificate expires.</td></tr><tr><td valign="top">Cert Usage</td><td valign="top">Indicates whether the certificate is valid for code-signing operations, which is required for publishing updates to WSUS and signing ConfigMgr detection method scripts.</td></tr><tr><td valign="top">Public Key</td><td valign="top">The cryptographic algorithm and key length used by the certificate (for example, RSA 2048-bit).</td></tr><tr><td valign="top">Thumbprint</td><td valign="top">A unique identifier for the certificate, useful for verification and troubleshooting.</td></tr><tr><td valign="top">Trusted Publisher</td><td valign="top">Confirms whether the certificate is trusted for publishing updates to WSUS.</td></tr><tr><td valign="top">Trusted Root Authority</td><td valign="top">Indicates whether the certificate chain is trusted by the local system and WSUS.</td></tr><tr><td valign="top">Self Signed</td><td valign="top">Indicates this is a self-signed certificate.</td></tr></tbody></table>

## Validate Trust Chain

Clicking **Validate Trust Chain** checks whether the certificate and its chain of trust are trusted by the local system.&#x20;

![Clicking 'Validate Trust Chain'](/_images/image-(4488).png "Clicking &#x27;Validate Trust Chain&#x27;")

This is a useful troubleshooting step if the publishing of updates fails due to certificate or trust-related errors.

![Validate the certificate trust chain](/_images/image-(3914).png "Validate the certificate trust chain")

## Troubleshooting Certificates

If you receive an error when you click **Show Certificate**, use the steps in this section to identify the cause.

### No Certificate found in the WSUS Store on this Server

![No Certificate foundin the WSUS Store on this Server](/_images/image-(4266).png "No Certificate foundin the WSUS Store on this Server")

If clicking **Show Certificate** displays **No certificate found in the WSUS store on this server**, review **PatchMyPC.log** for related certificate extraction errors. An entry such as

`An error occurred while extracting the certificate from WSUS: C:\WINDOWS\SystemTemp\PMP-1d2xluld\jwpcs1ov.tmp : The request failed with HTTP status 503: Service Unavailable. CertManager 18/04/2026 12:12:54 34 (0x0022)`
\
`Failed to extract the certificate from WSUS CertManager 18/04/2026 12:12:54 34 (0x0022)`

Verify that the WSUS Application Pool is started in IIS, then retry the action.

![Verify that the WSUS Application Pool is started in IIS, then retry the action.](/_images/image-(4267).png "Verify that the WSUS Application Pool is started in IIS, then retry the action.")
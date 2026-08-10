# Show Certificate

_Applies to: Patch My PC Publisher V2.x_

## Overview

The Show Certificate option displays detailed information about the code-signing certificate currently configured for use by the Publisher. This view allows you to verify that a valid certificate is selected, confirm its trust status, and ensure it meets WSUS and ConfigMgr signing requirements.

![Show the Certificate being used by the Publisher](/_images/image-(3913).png "Show the Certificate being used by the Publisher")

When you select **Show Certificate**, the following information is displayed:

* **Issuer**\
  The authority that issued the certificate. This may be ConfigMgr, the Publisher, or an internal/public Certificate Authority.
* **Subject**\
  The identity the certificate was issued to.
* **Effective Date**\
  The date and time from which the certificate is valid.
* **Expiration Date**\
  The date and time the certificate expires.
* **Code Signing**\
  Indicates whether the certificate is valid for code-signing operations, which is required for publishing updates to WSUS and signing ConfigMgr detection method scripts.
* **Public Key**\
  The cryptographic algorithm and key length used by the certificate (for example, RSA 2048-bit).
* **Thumbprint**\
  A unique identifier for the certificate, useful for verification and troubleshooting.
* **WSUS certificate installed in the Trusted Publishers certificate store**\
  Confirms whether the certificate is trusted for publishing updates to WSUS.
* **WSUS certificate installed in the Trusted Root certificate store**\
  Indicates whether the certificate chain is trusted by the local system and WSUS.

## Validate Trust Chain

Selecting **Validate Trust Chain** checks whether the certificate and its issuing chain are trusted by the local system. This is a useful troubleshooting step if update publishing fails due to certificate or trust-related errors.

![Validate the certificate trust chain](/_images/image-(3914).png "Validate the certificate trust chain")

## Troubleshooting

If you receive an error when you click **Show Certificate**, use the troubleshooting steps in this section to identify the cause.

### No Certificate foundin the WSUS Store on this Server

![No Certificate foundin the WSUS Store on this Server](/_images/image-(4266).png "No Certificate foundin the WSUS Store on this Server")

If clicking **Show Certificate** displays **No certificate found in the WSUS store on this server**, review **PatchMyPC.log** for related certificate extraction errors. An entry such as

`An error occurred while extracting the certificate from WSUS: C:\WINDOWS\SystemTemp\PMP-1d2xluld\jwpcs1ov.tmp : The request failed with HTTP status 503: Service Unavailable. CertManager 18/04/2026 12:12:54 34 (0x0022)`
\
`Failed to extract the certificate from WSUS CertManager 18/04/2026 12:12:54 34 (0x0022)`

Verify that the WSUS Application Pool is started in IIS, then retry the action.

![Verify that the WSUS Application Pool is started in IIS, then retry the action.](/_images/image-(4267).png "Verify that the WSUS Application Pool is started in IIS, then retry the action.")
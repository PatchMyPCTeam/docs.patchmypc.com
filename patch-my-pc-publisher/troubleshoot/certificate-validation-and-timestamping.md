# Certificate Validation and Timestamping

_Applies to: Patch My PC Publisher V3.x_

This section explains how to troubleshoot certificate trust, revocation checks, and timestamp server connectivity issues in Patch My PC (PMPC) Publisher.

These issues can affect environments **with or without a proxy**. A trusted root certificate and access to the required certificate and timestamp services are separate requirements.

## Understand the log entry or email

Review the details in **PatchMyPC.log** or the notification email to identify which check failed. Similar certificate validation messages can have different causes.

| Message details                                                                                                                 | What it means                                                                                                                | What to check                                                                |
| ------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Explicitly refers "Chain build failed: UntrustedRoot".                                                                          | Windows cannot build a trusted certificate chain. Revocation checking cannot complete successfully for that chain either.    | Establish trust for the required root certificate first.                     |
| Reports that revocation checking cannot complete. "Offline Revocation: The revocation function was unable to check revocation". | Windows cannot determine the certificate's revocation status, for example because it cannot reach the CRL or OCSP endpoints. | Check access to the revocation endpoints for the relevant certificate chain. |

The missing trusted root message is an important distinction. If it appears alongside a revocation error and addresses the root certificate trust issue first. The revocation error alone does not establish that a firewall or proxy is blocking access to allow succesful certiifcation revocation checks.

<figure><img src="../../.gitbook/assets/image (1459).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1469).png" alt="" width="563"><figcaption></figcaption></figure>

A failed revocation check also does not mean that the certificate has been revoked; it means Windows could not establish its revocation status.

<figure><img src="../../.gitbook/assets/image (1468).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1470).png" alt="" width="563"><figcaption></figcaption></figure>

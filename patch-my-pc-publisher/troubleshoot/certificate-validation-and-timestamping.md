# Certificate Validation and Timestamping

_Applies to: Patch My PC Publisher V3.x_

This section explains how to troubleshoot certificate trust, revocation checks, and timestamp server connectivity issues in Patch My PC (PMPC) Publisher.

These issues can affect environments **with or without a proxy**. A trusted root certificate and access to the required certificate and timestamp services are separate requirements.

## Identify Certificate Validation Issues

Publisher records certificate validation and timestamping issues in PatchMyPC.log. If email notifications are configured, you will also receive an email about these issues.&#x20;

Review the details in **PatchMyPC.log** or the notification email to identify which check failed. Similar certificate validation messages can have different causes.

| Message details                                                                                                                 | What it means                                                                                                                | What to check                                                                |
| ------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Explicitly refers "Chain build failed: UntrustedRoot".                                                                          | Windows cannot build a trusted certificate chain. Revocation checking cannot complete successfully for that chain either.    | Establish trust for the required root certificate first.                     |
| Reports that revocation checking cannot complete. "Offline Revocation: The revocation function was unable to check revocation". | Windows cannot determine the certificate's revocation status, for example because it cannot reach the CRL or OCSP endpoints. | Check access to the revocation endpoints for the relevant certificate chain. |

The entries in **PatchMyPC.log** and the notification email may look similar but the missing trusted root message is an important distinction. If it appears alongside a revocation error and addresses the root certificate trust issue first. The revocation error alone does not establish that a firewall or proxy is blocking access to allow succesful certiifcation revocation checks.

### Issue 1: Missing or untrusted root certificate

The message explicitly mentions the trusted root certificate. Windows cannot build a trusted certificate chain.

<figure><img src="../../.gitbook/assets/image (1459).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1469).png" alt="" width="563"><figcaption></figcaption></figure>

When Publisher validates a certificate, an attempt is made to build the certificate chain and check its revocation status. The required root certificate must be present and trusted in the **Local Computer > Trusted Root Certification Authorities** store. If it is missing or untrusted, a trusted chain cannot be built or validated.

Windows can automatically retrieve trusted root certificates during chain building. However, Group Policy or other certificate management policies may disable this behavior. For example, enabling **Turn off Automatic Root Certificates Update** prevents Windows from checking Windows Update for the required trusted root.&#x20;

<figure><img src="../../.gitbook/assets/image (1471).png" alt="" width="563"><figcaption></figcaption></figure>

This may explain why **DigiCert Trusted Root G4** is missing from the server which is a requirment for revocation checks to complete for the Patch My PC catalog.

To resolve this issue, install and trust the required root certificate using your organization’s approved certificate management process. For remediation steps, see [**Resolve certificate validation issues**](certificate-validation-and-timestamping.md#resolve-certificate-validation-issues) below.

{% hint style="info" %}
**Note**

Installing and trusting the missing root certificate resolves Issue 1. In restricted environments, access to certificate revocation endpoints may also be blocked. After resolving root certificate trust, check for any remaining revocation warnings and follow the guidance for Issue 2.
{% endhint %}

### Issue 2: Unable to complete certificate revocation checks

The message reports a failed revocation check without the additional missing trusted root message. Windows cannot reach the required revocation endpoints.

<figure><img src="../../.gitbook/assets/image (1468).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1470).png" alt="" width="563"><figcaption></figcaption></figure>

When validating a certificate, a check is perfomed to see whether it has been revoked by its issuer using the **Certificate Revocation List (CRL)** or **Online Certificate Status Protocol (OCSP)** endpoints specified in the certificate chain.

For example, when Publisher validates the downloaded Patch My PC catalog, an attempt is made to contact the revocation endpoints for its signing certificate chain. If those endpoints cannot be reached, Publisher logs a warning that the revocation check could not be completed. This does **not** mean the certificate has been revoked.

This commonly occurs when outbound access to the required endpoints over **HTTP, port 80**, is blocked or has not been permitted through a firewall or proxy. Access to these endpoints is a requirement for the Publisher, as outlined in the [**core network requirements**](../requirements/core-requirements.md#network).

These connectivity-related warnings do not prevent publishing, but we recommend restoring access so certificate revocation checks can be completed succesfully.

For remediation steps, see [**Resolve certificate validation issues**](certificate-validation-and-timestamping.md#resolve-certificate-validation-issues) below.

## Resolve certificate validation issues

Follow the steps for the issue identified above. If both issues are present, resolve issue 1 first, then check whether revocation warnings remain.

### Issue 1: Missing or untrusted root certificate

**DigiCert Trusted Root G4** is the root certificate in the signing certificate chains for the Patch My PC catalog CAB and the Publisher MSI downloaded during automatic updates. It must be present and trusted so Publisher can build and validate those certificate chains.

#### Check the certificate store

On the Publisher server:

1. Open **Manage computer certificates** (`certlm.msc`).
2. Expand **Trusted Root Certification Authorities > Certificates**.
3. Check that **DigiCert Trusted Root G4** is present.

<figure><img src="../../.gitbook/assets/image (1472).png" alt="" width="563"><figcaption></figcaption></figure>

If the root certificate is missing, ask your Windows or security administrator to deploy it using your organization's approved certificate management process and an official certificate source. Retry the affected operation after trust is established.

### Issue 2: Unable to complete certificate revocation checks

Include the required endpoints and guidance for direct or proxy access.

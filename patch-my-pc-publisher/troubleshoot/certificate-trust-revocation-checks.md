# Troubleshoot Certificate Trust and Revocation Checks for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This section explains how to troubleshoot certificate trust and revocation checks and connectivity issues in Patch My PC (PMPC) Publisher.

## Identify Certificate Validation Issues

Publisher records certificate chain validation failures and unsuccessful revocation checks in **PatchMyPC.log**. If email notifications are configured, you will also receive an email about these issues.

Use the examples below to distinguish between a missing or untrusted root certificate (Issue 1) and an inability to complete revocation checks (Issue 2).

<table><thead><tr><th valign="top">Message details</th><th valign="top">What it means</th><th valign="top">What to check</th></tr></thead><tbody><tr><td valign="top"><a href="certificate-trust-revocation-checks.md#issue-1-missing-or-untrusted-root-certificate"><strong>Issue 1: Missing or untrusted root</strong></a><br>Includes <code>Chain build failed: UntrustedRoot</code>.</td><td valign="top">Windows cannot build a trusted certificate chain. Revocation validation cannot complete successfully for that chain either.</td><td valign="top">Establish trust for the required root certificate first.</td></tr><tr><td valign="top"><a href="certificate-trust-revocation-checks.md#issue-2-unable-to-complete-certificate-revocation-checks"><strong>Issue 2: Revocation check unavailable</strong></a><br>Includes <code>Offline Revocation: The revocation function was unable to check revocation</code>.</td><td valign="top">Windows cannot determine the certificate’s revocation status, for example because the CRL or OCSP endpoints are unreachable.</td><td valign="top">Check access to the required revocation endpoints.</td></tr></tbody></table>

The entries in **PatchMyPC.log** and the notification email may look similar, but the **missing trusted root message** is an important distinction because it will appear alongside a revocation error. Resolve the root certificate trust issue first, then check whether revocation warnings remain.

### Issue 1: Missing or Untrusted Root Certificate

The message explicitly mentions the trusted root certificate. Windows cannot build a trusted certificate chain.

<figure><img src="../../.gitbook/assets/image (1459).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1469).png" alt="" width="563"><figcaption></figcaption></figure>

When Publisher validates a certificate, an attempt is made to build the certificate chain and check its revocation status. The required root certificate must be present and trusted in the **Local Computer > Trusted Root Certification Authorities** store. If it is missing or untrusted, a trusted chain cannot be built or validated.

Windows can automatically retrieve trusted root certificates during chain building. However, Group Policy or other certificate management policies may disable this behavior. For example, enabling **Turn off Automatic Root Certificates Update** prevents Windows from checking Windows Update for the required trusted root.&#x20;

<figure><img src="../../.gitbook/assets/image (1471).png" alt="" width="563"><figcaption></figcaption></figure>

This may explain why **DigiCert Trusted Root G4** is missing from the server which is a requirement for revocation checks to complete for the Patch My PC catalog.

To resolve this issue, install and trust the required root certificate using your organization’s approved certificate management process. For remediation steps, see [**Resolve certificate validation issues**](certificate-trust-revocation-checks.md#resolve-certificate-validation-issues) below.

{% hint style="info" %}
**Note**

Installing and trusting the missing root certificate resolves Issue 1. In restricted environments, access to certificate revocation endpoints may also be blocked. After resolving root certificate trust, check for any remaining revocation warnings and follow the guidance for Issue 2.
{% endhint %}

### Issue 2: Unable to Complete Certificate Revocation Checks

The message reports a failed revocation check without the additional missing trusted root message. Windows cannot reach the required revocation endpoints.

<figure><img src="../../.gitbook/assets/image (1468).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1470).png" alt="" width="563"><figcaption></figcaption></figure>

When validating a certificate, a check is performed to see whether it has been revoked by its issuer using the Certificate Revocation List (CRL) or Online Certificate Status Protocol (OCSP) endpoints specified in the certificate chain.

For example, when Publisher validates the downloaded Patch My PC catalog, an attempt is made to contact the revocation endpoints for its signing certificate chain. If those endpoints cannot be reached, Publisher logs a warning that the revocation check could not be completed. This does **not** mean the certificate has been revoked.

This commonly occurs when outbound access to the required endpoints over **HTTP, port 80**, is blocked or has not been permitted through a firewall or proxy. Access to these endpoints is a requirement for the Publisher, as outlined in the [**core network requirements**](../requirements/core-requirements.md#network).

These connectivity-related warnings do not prevent publishing, but we recommend restoring access so certificate revocation checks can be completed succesfully.

For remediation steps, see [**Resolve certificate validation issues**](certificate-trust-revocation-checks.md#resolve-certificate-validation-issues) below.

## Resolve Certificate Validation Issues

Follow the steps for the issue identified above. If both issues are present, resolve issue 1 first, then check whether revocation warnings remain.

### Issue 1: Trust the Root Certificate

**DigiCert Trusted Root G4** is the root certificate in the signing certificate chains for the Patch My PC catalog CAB and the Publisher MSI downloaded during automatic updates. It must be present and trusted so Publisher can build and validate those certificate chains.

#### Check the certificate store

On the Publisher server:

1. Open **Manage computer certificates** (`certlm.msc`).
2. Expand **Trusted Root Certification Authorities > Certificates**.
3. Check that **DigiCert Trusted Root G4** is present.

<figure><img src="../../.gitbook/assets/image (1472).png" alt="" width="563"><figcaption></figcaption></figure>

If the root certificate is missing, ask your Windows or security administrator to deploy it using your organization's approved certificate management process and an official certificate source. Retry the affected operation after trust is established.

### Issue 2: Remediate Certificate Revocation Checks

To resolve this issue, ensure the Publisher server can reach the certificate and revocation endpoints for the certificate chain being validated.

#### **Allow access to the required endpoints**

As outlined in the [**core network requirements**](../requirements/core-requirements.md#network)**,** allow outbound access over **HTTP, port 80**, to the following DigiCert endpoints. These support validation of the signing certificate chains for the **Patch My PC catalog** and **Publisher MSI**.

| Endpoint                      | Purpose                               |
| ----------------------------- | ------------------------------------- |
| `http://cacerts.digicert.com` | Certificate retrieval                 |
| `http://crl3.digicert.com`    | Certificate revocation list retrieval |
| `http://crl4.digicert.com`    | Certificate revocation list retrieval |
| `http://ocsp.digicert.com`    | Online certificate status checks      |

Ensure your firewall and network filtering rules permit these requests from the Publisher server.

{% hint style="info" %}
**Note**

A successful connection from your browser, in the logged on user context, does not confirm that the SYSTEM account can reach these endpoints.
{% endhint %}

#### **If your environment uses a proxy server**

Certificate revocation checks do not use the proxy configured in Publisher. For the default service configuration, Windows uses the SYSTEM account’s WinINet proxy settings.

Either:

* Configure the SYSTEM account’s WinINet proxy and ensure the proxy permits access to the required endpoints.
* Allow the Publisher server to reach these endpoints directly through your firewall.

See [Configure the WinINet proxy for certificate revocation checks and script signing](../manage/advanced-tab/network-proxy.md#configuring-the-wininet-proxy-for-certificate-revocation-checks-and-script-signing) for more details.

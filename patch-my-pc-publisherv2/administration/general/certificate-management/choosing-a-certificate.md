# Choosing a Certificate

_Applies to: Patch My PC Publisher V2.x_

## Overview

Customers often ask which code-signing certificate option they should use when publishing third-party updates. There is no single correct choice, as the right approach depends on your organization’s security requirements, PKI maturity, and operational preferences. In practice, many environments successfully use self-signed certificates, while others require PKI-issued certificates for compliance or governance reasons.

Regardless of the option chosen, the resulting certificate is used by the Publisher to code-sign updates published to WSUS, specifically the CAB files that contain update metadata. The same certificate is also used to sign ConfigMgr detection scripts, even in a ConfigMgr-only environment where there is no WSUS being leveraged by a Software Update Point. Ultimately, whichever method you choose, the certificate that resides in the WSUS certificate store is the certificate the Publisher will use for signing during ConfigMgr and WSUS publishing operations.

<figure><img src="../../../../.gitbook/assets/image (3912).png" alt="Code-Signing Certificate in WSUS Store" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If multiple code-signing certificates are present in the WSUS store on the SUP, the certificate with the longest validity is always selected.
{% endhint %}

The Publisher supports multiple approaches to accommodate both ConfigMgr and WSUS environments:

1. Letting ConfigMgr create and manage the certificate.
2. Generating a self-signed certificate directly in Publisher.
3. Importing a customer-provided PFX certificate issued by an internal or public Certificate Authority.

The sections below outlines the considerations for each option.

## ConfigMgr–Managed Certificate (Recommended)

No action is needed from the Publisher. If ConfigMgr is already set to automatically manage the certificate, this will be the certificate the Publisher selects by default, if there is not another certificate in the WSUS store with a longer validity period.

**Best suited for:**\
Organizations that want the simplest setup with minimal manual certificate handling.

**Why choose this option**

* Creates a self-signed WSUS code-signing certificate if one does not exist.
* Manages certificate lifecycle and renewal process.

**Considerations**

* The certificate generated is self-signed.
* May not meet stricter compliance or PKI requirements in some organizations.

{% hint style="warning" %}
**Important**

When ConfigMgr is configured to manage the code-signing certificate, an expired certificate is automatically blocked and removed from client devices during a software update scan.

If you are using a PKI-issued certificate and it expires, ConfigMgr may automatically generate and begin using a self-signed certificate instead. This behavior can be unexpected in environments that require PKI-issued certificates, so ensure certificates are renewed before expiration to avoid unintended changes or disruption.
{% endhint %}

See the following page for more details: [https://learn.microsoft.com/en-us/intune/configmgr/sum/deploy-use/third-party-software-updates#automatically-manage-the-wsus-signing-certificate](https://learn.microsoft.com/en-us/intune/configmgr/sum/deploy-use/third-party-software-updates#automatically-manage-the-wsus-signing-certificate)

## Publisher-Generated Self-Signed Certificate

Regardless of whether ConfigMgr is configured to automatically manage the certificate, or if the environment is WSUS-only, customers can choose to have the Publisher generate and use its own self-signed certificate.

**Best suited for:**\
WSUS standalone environemnts or ConfigMgr environments where self-signed certificates are allowed, but where administrators want more control over certificate creation and lifecycle.

**Pros**

* Free and immediate to create.
* Does not require a PKI.
* Allows control over key length, validity period, and exportability.
* Can still be automatically distributed to clients by ConfigMgr.

**Cons**

* Self-signed certificates cannot be revoked using a Certificate Revocation List (CRL).
* If the private key is compromised, the certificate must be manually removed from client trust stores using ConfigMgr or another method.
* When the certificate is reaching the expiry date, customers must remember to re-generate the certificate to ensure signing operations continue uninterrupted.

See the following page for more details: [Generate a Self-Signed Certificate](generate-a-self-signed-certificate.md)

{% hint style="info" %}
**Note**

By default, in this scneario, the generated certificate’s **private key is marked as exportable**. This is intentional and recommended, as it allows the certificate (including the private key) to be exported and reused if the Publisher is later moved to a new top-level SUP.&#x20;

Without an exportable private key, the same signing certificate could not be transferred to another server.
{% endhint %}

## Customer-Provided PKI (PFX) Certificate

Regardless if ConfigMgr is already set to automatically manage the certificate, customers can opt for the Publisher to use a PKI-issued certificate.

**Best suited for:**\
Organizations with strict security, compliance, or audit requirements that mandate PKI-issued certificates.

**Pros**

* Certificates can be revoked if compromised.
* Can be issued from an internal PKI (such as Active Directory Certificate Services) at no additional cost.
* Supported by Configuration Manager for automatic distribution to clients.

**Cons**

* Requires access to a PKI and coordination with security or PKI teams.
* Public Certificate Authority certificates may incur additional cost.

{% hint style="warning" %}
**Important**

If you are using a PKI-issued certificate and it expires, and ConfigMgr is set to automatically manage the certificate, ConfigMgr may automatically generate and begin using a self-signed certificate instead. This behavior can be unexpected in environments that require PKI-issued certificates, so ensure certificates are renewed before expiration to avoid unintended changes or disruption.
{% endhint %}

# Choosing a Certificate to use with Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Customers often ask which code-signing certificate option they should use when publishing third-party updates using a tool like Patch My PC (PMPC) Publisher.

There is no single correct choice, as the right approach depends on your organization’s security requirements, PKI maturity, and operational preferences.

In practice, many environments successfully use self-signed certificates, whilst others require PKI-issued certificates for compliance or governance reasons.

Regardless of the option chosen, the resulting certificate is used by Publisher to code-sign updates published to WSUS, specifically the CAB files that contain update metadata.

The same certificate is also used to sign ConfigMgr detection scripts, even in a ConfigMgr-only environment where there is no WSUS being used by a Software Update Point (SUP).

Ultimately, whichever method you choose, the certificate residing in the WSUS certificate store is the certificate Publisher will use for signing during ConfigMgr and WSUS publishing operations.

{% hint style="info" %}
**Note**

If multiple code-signing certificates are present in the WSUS store on the SUP, the certificate with the longest validity is always selected.
{% endhint %}

Publisher supports multiple approaches to accommodate both ConfigMgr and WSUS environments:

* [Letting ConfigMgr create and manage the certificate](choosing.md#configmgr-managed-certificate-recommended)
* [Generating a self-signed certificate directly in Publisher](choosing.md#publisher-generated-self-signed-certificate)
* [Importing a customer-provided PFX certificate issued by an internal or public Certificate Authority](choosing.md#customer-provided-pki-pfx-certificate)

## ConfigMgr–Managed Certificate (Recommended)

No action is needed from Publisher. If ConfigMgr is already set to automatically manage the certificate, this will be the certificate that Publisher selects by default, if there is no other certificate in the WSUS store with a longer validity period.

**Best suited for:**\
Organizations that want the simplest setup with minimal manual certificate handling.

**Why choose this option**

* Creates a self-signed WSUS code-signing certificate if one does not exist.
* Manages certificate lifecycle and renewal process.

**Considerations**

* The certificate generated is self-signed.
* May not meet stricter compliance or PKI requirements in some organizations.

{% hint style="danger" %}
**Important**

When ConfigMgr is configured to manage the code-signing certificate, an expired certificate is automatically blocked and removed from client devices during a software update scan.

If you are using a PKI-issued certificate and it expires, ConfigMgr may automatically generate and begin using a self-signed certificate instead.

This behavior can be unexpected in environments that require PKI-issued certificates, so ensure certificates are renewed before expiration to avoid unintended changes or disruption.
{% endhint %}

{% hint style="info" %}
**Note**

See [Automatically manage the WSUS signing certificate](https://learn.microsoft.com/en-us/intune/configmgr/sum/deploy-use/third-party-software-updates#automatically-manage-the-wsus-signing-certificate) for more information.
{% endhint %}

## Publisher-Generated Self-Signed Certificate

Regardless of whether ConfigMgr is configured to automatically manage the certificate or the environment is WSUS-only, customers can choose to have Publisher generate and use its own self-signed certificate.

**Best suited for:**\
WSUS standalone environments or ConfigMgr environments where self-signed certificates are allowed, but where administrators want more control over certificate creation and lifecycle.

**Pros**

* Free and immediate to create.
* Does not require a PKI.
* Allows control over key length, validity period, and exportability.
* Can still be automatically distributed to clients by ConfigMgr.

**Cons**

* Self-signed certificates cannot be revoked using a Certificate Revocation List (CRL).
* If the private key is compromised, the certificate must be manually removed from client trust stores using ConfigMgr or another method.
* When the certificate reaches its expiry date, customers must remember to regenerate it to ensure signing operations continue uninterrupted.

{% hint style="info" %}
**Note**

See [Generate a Self-Signed Certificate](../../../../../patch-my-pc-publisherv2/administration/general/certificate-management/generate-a-self-signed-certificate.md) for more details.
{% endhint %}

By default, in this scenario, the generated certificate’s private key is marked as exportable. This is intentional and recommended, as it allows the certificate (including the private key) to be exported and reused if Publisher is later moved to a new top-level SUP.

Without an exportable private key, the same signing certificate could not be transferred to another server.

## Customer-Provided PKI (PFX) Certificate

Regardless of whether ConfigMgr is already configured to automatically manage the certificate, customers can opt to use a PKI-issued certificate for Publisher.

**Best suited for:**\
Organizations with strict security, compliance, or audit requirements that mandate PKI-issued certificates.

**Pros**

* Certificates can be revoked if compromised.
* Can be issued from an internal PKI (such as Active Directory Certificate Services) at no additional cost.
* Supported by ConfigMgr for automatic distribution to clients.

**Cons**

* Requires access to a PKI and coordination with security or PKI teams.
* Public Certificate Authority certificates may incur additional cost.

{% hint style="danger" %}
**Important**

If you are using a PKI-issued certificate that expires, and ConfigMgr is set to automatically manage the certificate, it may generate and begin using a self-signed certificate instead.

This behavior can be unexpected in environments that require PKI-issued certificates, so ensure certificates are renewed before they expire to avoid unintended changes or disruptions.
{% endhint %}

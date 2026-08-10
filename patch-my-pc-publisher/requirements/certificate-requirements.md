# Certificate Requirements for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

When working with Microsoft ConfigMgr or WSUS, correct certificate configuration is required to ensure that updates are trusted and considered secure by the platform.&#x20;

Microsoft enforces this by requiring all third-party and custom updates to be code signed before they can be published into WSUS. This applies specifically to the CAB files that contain update metadata and content.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Detailed guidance on certificate creation, selection, trust requirements, and lifecycle management is covered on the [Certificate Management](../manage/wsus-updates-tab/wsus-options/certificate-management/) page.</p>
</blockquote>

To meet this requirement, Patch My PC (PMPC) Publisher must be provided with a code-signing certificate. This certificate is used to sign third-party updates during publishing, allowing WSUS and managed devices to validate the origin and integrity of the updates.

Publisher supports multiple certificate configuration options to accommodate different organizational, security, and compliance requirements:

* **ConfigMgr–managed certificate**\
  When WSUS is used as part of a Software Update Point, Microsoft ConfigMgr can automatically generate and manage a self-signed WSUS signing certificate. This is the simplest and most commonly used option.
* **Publisher-generated self-signed certificate**\
  Publisher can create and manage its own self-signed code-signing certificate, which is commonly used in WSUS-only environments or where ConfigMgr is not available to manage the certificate.
* **Customer-provided PKI certificate (PFX)**\
  Organizations with stricter security or compliance requirements can provide a PFX file containing a code-signing certificate issued by an internal or public Certificate Authority.

In most environments, allowing ConfigMgr or Publisher to manage a self-signed certificate is sufficient.&#x20;

However, for organizations that require certificate revocation, centralized PKI governance, or formal audit controls, importing a PKI-issued certificate may be necessary.
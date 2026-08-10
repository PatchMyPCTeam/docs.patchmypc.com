# Overview of Security in Patch My  PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Patch My PC (PMPC) Publisher automates third-party application and update management for Microsoft WSUS, ConfigMgr, and Intune while minimizing software supply chain risk. The core security objective is:

> _To ensure that the file installed on a client device is identical to the file originally obtained from the official vendor source and validated by Patch My PC._

The security model is built on layered validation controls that protect catalog integrity, prevent tampering, and enforce clear trust boundaries inside customer environments.

For a detailed walkthrough of our security model and catalog validation process, watch the video below featuring our Director of Security.

{% embed url="https://www.youtube.com/watch?v=oIERl7YcKMQ" %}

## Industry Comparison Narrative

Traditional third-party software packaging workflows often rely on implicit trust. An administrator downloads an installer from a vendor's website, performs limited validation, packages it, and deploys it.&#x20;

Whilst this process is common and generally well-intentioned, it typically depends on a single trust decision made at download time and may lack structured governance, repeatable validation controls, and separation of responsibilities.

Patch My PC’s model replaces that single trust checkpoint with a controlled, repeatable validation pipeline. Instead of assuming integrity, it verifies it at multiple stages before content ever reaches a customer's environment.&#x20;

This approach reflects modern supply chain security principles, in which integrity is treated as a continuously enforced condition rather than a one-time assumption.

By combining automation with structured oversight, Patch My PC reduces operational burden whilst increasing assurance compared to traditional manual packaging workflows.

## Curated Catalog Model

Patch My PC maintains a curated catalog. Updates are not submitted by external contributors and are not automatically ingested from public repositories. Each update is intentionally reviewed, validated, tested, and approved before release.

This differs significantly from crowdsourced packaging models, where external contributors may introduce content into the update pipeline.&#x20;

A curated approach reduces supply chain exposure by enforcing controlled release workflows, defined approval gates, and separation of duties throughout the catalog lifecycle.

Each catalog entry is created, validated, signed, and approved through a controlled internal process before being made available to customers.

{% hint style="info" %}
**Note**

For more information on why curated catalogs are more secure than community-based catalogs, see our blog [Curated vs. Crowdsourced: Why Enterprise Software Catalogs Require Professional Curation](https://patchmypc.com/blog/curated-vs-crowdsourced/).
{% endhint %}

## Vendor Binary Acquisition and Validation

When a new third-party update is added to the catalog, the binary is downloaded directly from the vendor’s official distribution source.

The original download URL and cryptographic file hash are recorded in the catalog metadata. This hash serves as the authoritative reference for later validation during publishing.&#x20;

Before release, binaries undergo malware and integrity validation. Files are uploaded to VirusTotal and scanned across dozens of antivirus engines.

{% hint style="info" %}
**Note**

See [Binary Validation](binary-validation.md) for more information on this acquisition and validation process.
{% endhint %}

## Catalog Creation and Code Signing

After validation, catalog metadata is compiled into a CAB file. The catalog is then dual code-signed using a hardware-protected DigiCert code-signing certificate.

Signing keys are hardware-backed and access-controlled. Catalog creation, signing, and approval are separate responsibilities. Individuals who build catalog entries are not the same individuals who sign and approve releases. Automated validation checks must pass before signing can occur.

This separation of duties reduces insider risk and strengthens release integrity.

## Secure Catalog Delivery and Integrity Protection

Publisher retrieves the catalog over HTTPS on port 443 from `api.patchmypc.com`. Before the catalog is delivered, the API verifies the customer’s license to ensure only authorized customers can download it.

Once downloaded, Publisher validates the catalog’s digital signature. The catalog CAB file is dual code-signed using a hardware-protected certificate.&#x20;

If the signature does not match Patch My PC’s trusted certificate, processing stops immediately, and the catalog is discarded.

As the catalog is cryptographically signed, any modification to the file invalidates the signature. If a malicious actor attempted to intercept, modify, or replace the catalog in transit, the signature validation would fail, and the file would be rejected. Publisher does not process unsigned or improperly signed catalog files.

The combination of encrypted HTTPS transport, license validation, and strict signature verification ensures catalog authenticity and protects against tampering or man-in-the-middle attacks before any catalog content is processed.

## Hash Verification During Publishing

Security validation continues inside the customer environment.

When publishing an update, Publisher downloads the vendor binary directly from the official vendor source using the URL stored in the catalog metadata.&#x20;

It then calculates the hash of the downloaded file and compares it to the original hash recorded during catalog creation.

Publishing only proceeds if the hashes match exactly. If a vendor distribution point were compromised or a file altered after initial validation, the hash comparison would fail, and the update would not be published.

This ensures that the file deployed in the customer environment is byte-for-byte identical to the file originally obtained from the vendor and validated by the Patch My PC catalog team.

## Customer Environment Trust Boundary

For WSUS, updates are re-signed using the customer’s WSUS code-signing certificate before deployment. Client devices install only updates signed by a certificate trusted within their own environment.

For Intune environments, publishing operations are performed using a tenant-controlled [App Registration](../requirements/intune-requirements/entra-id-app-registration/) with Microsoft Graph permissions scoped to that tenant.&#x20;

The Enterprise Application used for a Custom App is used solely for user authentication and does not perform publishing operations.

These mechanisms ensure customers maintain full control of trust within their own environment.

## Executive Security Summary for Risk and Compliance Review

Patch My PC Publisher is built around a defense-in-depth security model. Rather than relying on any single safeguard, multiple independent controls work together across the entire update lifecycle, from the moment a vendor's software is acquired through to installation on your endpoints.

Transport security comes first. All catalog delivery occurs over encrypted HTTPS with license validation, protecting against in-transit interception.&#x20;

The catalog itself is dual-code-signed with hardware-backed keys, and Publisher enforces strict digital signature verification before the catalog is processed, so any tampering is caught immediately.

On the software supply chain side, vendor binaries are scanned for malware before release, and cryptographic hashes are recorded at catalog creation and verified again at publish time.&#x20;

This means even a compromise of a vendor's own distribution infrastructure won't go undetected. To further reduce insider risk, the catalog build, signing, and approval stages are handled with separation of duties, so no single person can push a change through unilaterally.

For customers using WSUS, Publisher adds one final layer. Mandatory customer-side re-signing is enforced before any update reaches a client device, meaning nothing installs unless it has been explicitly trusted within your own PKI boundary.

Taken together, these controls are designed to protect against catalog tampering, man-in-the-middle attacks, vendor mirror compromise, unauthorized content injection, insider manipulation, and unauthorized client installation.

{% hint style="info" %}
**Note**

Please refer to the [Patch My PC Trust Center](https://trust.patchmypc.com/) for detailed documentation of our broader security posture, compliance practices, and operational controls.
{% endhint %}

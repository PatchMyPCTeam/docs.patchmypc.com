# Overview

_Applies to: Patch My PC Publisher V2.x_

## Introduction

Patch My PC Publisher automates third-party application and update management for WSUS, ConfigMgr, and Intune while minimizing software supply chain risk. The core security objective is:

> The file installed on a client device must be identical to the file originally obtained from the official vendor source and validated by Patch My PC.

The security model is built on layered validation controls that protect catalog integrity, prevent tampering, and enforce clear trust boundaries inside customer environments.

For a detailed walkthrough of our security model and catalog validation process, watch the video below featuring our Director of Security.

{% embed url="https://www.youtube.com/watch?v=oIERl7YcKMQ" %}

## Industry Comparison Narrative

Traditional third-party software packaging workflows often rely on implicit trust. An administrator downloads an installer from a vendor website, performs limited validation, packages it, and deploys it. While this process is common and generally well-intentioned, it typically depends on a single trust decision made at download time and may lack structured governance, repeatable validation controls, and separation of responsibilities.

Patch My PC’s model replaces that single trust checkpoint with a controlled, repeatable validation pipeline. Instead of assuming integrity, it verifies it at multiple stages before content ever reaches a customer environment. This approach reflects modern supply chain security principles, where integrity is treated as a continuously enforced condition rather than a one-time assumption.

By combining automation with structured oversight, Patch My PC reduces operational burden while increasing assurance compared to traditional manual packaging workflows.

## Curated Catalog Model

Patch My PC maintains a curated catalog. Updates are not submitted by external contributors and are not automatically ingested from public repositories. Each update is intentionally reviewed, validated, tested, and approved before release.

This differs significantly from crowdsourced packaging models, where external contributors may introduce content into the update pipeline. A curated approach reduces supply chain exposure by enforcing controlled release workflows, defined approval gates, and separation of duties throughout the catalog lifecycle.

Each catalog entry is created, validated, signed, and approved through a controlled internal process before being made available to customers.

For more information on why curated catalogs are more secure than community-based catalogs, see our blog [Curated vs. Crowdsourced: Why Enterprise Software Catalogs Require Professional Curation](https://patchmypc.com/blog/curated-vs-crowdsourced/).

## Vendor Binary Acquisition and Validation

When a new third-party update is added to the catalog, the binary is downloaded directly from the vendor’s official distribution source.

The original download URL and cryptographic file hash are recorded in the catalog metadata. This hash becomes the authoritative reference used for later validation during publishing. Before release, binaries undergo malware and integrity validation. Files are uploaded to VirusTotal and scanned across dozens of antivirus engines.

See [Binary Validation](binary-validation.md) for more information on this aquision and validation process.

## Catalog Creation and Code Signing

After validation, catalog metadata is compiled into a CAB file. The catalog is then dual code-signed using a hardware-protected DigiCert code-signing certificate.

Signing keys are hardware-backed and access controlled. Catalog creation, signing, and approval are separated responsibilities. Individuals who build catalog entries are not the same individuals who sign and approve releases. Automated validation checks must pass before signing can occur.

This separation of duties reduces insider risk and strengthens release integrity.

## Secure Catalog Delivery and Integrity Protection

The Publisher retrieves the catalog over HTTPS on port 443 from api.patchmypc.com. Before the catalog is delivered, the API verifies the customer’s license to ensure only authorized customers can download it.

Once downloaded, the Publisher validates the catalog’s digital signature. The catalog CAB file is dual code-signed using a hardware-protected certificate. If the signature does not match Patch My PC’s trusted certificate, processing stops immediately and the catalog is discarded.

Because the catalog is cryptographically signed, any modification to the file invalidates the signature. If a malicious actor attempted to intercept, modify, or replace the catalog in transit, the signature validation would fail and the file would be rejected. The Publisher does not process unsigned or improperly signed catalog files.

The combination of encrypted HTTPS transport, license validation, and strict signature verification ensures catalog authenticity and protects against tampering or man-in-the-middle attacks before any catalog content is processed.

## Hash Verification During Publishing

Security validation continues inside the customer environment.

When publishing an update, the Publisher downloads the vendor binary directly from the official vendor source using the URL stored in the catalog metadata. It calculates the hash of the downloaded file and compares it to the original hash recorded during catalog creation.

Publishing proceeds only if the hashes match exactly. If a vendor distribution point were compromised or a file altered after initial validation, the hash comparison would fail and the update would not be published.

This ensures that the file deployed in the customer environment is byte-for-byte identical to the file originally obtained from the vendor and validated by the Patch My PC catalog team.

## Customer Environment Trust Boundary

For WSUS, updates are re-signed using the customer’s WSUS code-signing certificate before deployment. Client devices install only updates signed by a certificate trusted within their own environment.

For Intune environments, publishing operations are performed using a tenant-controlled [App Registration](../publisher-requirements/intune-requirements/entra-id-app-registration/) with Microsoft Graph permissions scoped to that tenant. The Enterprise Application used for the Custom Apps is used solely for user authentication and does not perform publishing operations.

These mechanisms ensure that customers maintain full control of trust within their own environment.

## Executive Security Summary for Risk and Compliance Review

Patch My PC Publisher is built around a defense-in-depth security model. Rather than relying on any single safeguard, multiple independent controls work together across the entire update lifecycle, from the moment a vendor's software is acquired through to installation on your endpoints.

Transport security comes first. All catalog delivery happens over encrypted HTTPS with license validation, protecting against interception in transit. The catalog itself is dual code-signed using hardware-backed keys, and Publisher enforces strict digital signature verification before the catalog is ever processed, so any tampering is caught immediately.

On the software supply chain side, vendor binaries are scanned for malware before release, and cryptographic hashes are recorded at catalog creation and verified again at publish time. This means even a compromise of a vendor's own distribution infrastructure won't go undetected. To further reduce insider risk, the catalog build, signing, and approval stages are handled with separation of duties, so no single person can push a change through unilaterally.

For customers using WSUS, Publisher adds one final layer. Mandatory customer-side re-signing is enforced before any update reaches a client machine, meaning nothing installs unless it has been explicitly trusted within your own PKI boundary.

Taken together, these controls are designed to protect against catalog tampering, man-in-the-middle attacks, vendor mirror compromise, unauthorized content injection, insider manipulation, and unauthorized client installation.

For detailed documentation of our broader security posture, compliance practices, and operational controls, please refer to the [Patch My PC Trust Center](https://trust.patchmypc.com/).

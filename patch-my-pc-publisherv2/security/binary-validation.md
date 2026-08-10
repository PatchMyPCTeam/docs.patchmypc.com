# Binary Validation

_Applies to: Patch My PC Publisher V2.x_

## Two-Phase Binary Validation Model

Binary validation within Patch My PC follows a _two-phase_ security model. Validation does not occur at a single checkpoint. Instead, it is enforced through 2 independent validation phases designed to protect against vendor distribution compromise, tampering, unauthorized file substitution, and post release modification.

The objective is straightforward. The file deployed to client devices must be byte for byte identical to the file originally obtained from the official vendor source and validated by Patch My PC.

Binary validation occurs in two distinct phases:

* **Phase 1: Pre release validation and catalog creation**\
  The vendor binary is acquired, hashed, malware scanned, validated, and recorded in catalog metadata prior to release. This ensures only verified content enters the catalog.
* **Phase 2: Runtime validation during publishing**\
  When a customer publishes an update, the binary is downloaded again directly from the vendor. Its cryptographic hash is recalculated and compared against the authoritative hash stored in the catalog. Publishing proceeds only if the hashes match exactly.

![Two-Phase Binary Validation Model](/_images/image-(4186).png "Two-Phase Binary Validation Model")

If either phase fails, the update does not proceed.

## Phase 1: Pre-release Validation and Catalog Creation

{% stepper %}
{% step %}
### Official Vendor Download

When a new third party update is added to the Patch My PC catalog, the binary is downloaded directly from the vendor’s official distribution source. This may be the vendor’s public download endpoint or official content delivery network.

At the time of acquisition, the following data is captured and recorded in the catalog metadata:

* The exact vendor download URL
* The cryptographic hash of the binary
* The version and associated metadata

The recorded hash becomes the authoritative integrity reference for that update. This hash is later used during publishing to ensure that the file downloaded inside a customer environment is byte for byte identical to the file originally obtained and validated.

If the file were modified at any point after acquisition, whether through vendor mirror compromise, tampering, or corruption, the hash value would change. A mismatch results in publishing being halted.

In the example below, the catalog metadata contains both the original vendor download URL and the base64 encoded cryptographic hash. These values are used later in the validation process to confirm integrity.

![Example of Binary URL and Hash in the Catalog](/_images/image-(4168).png "Example of Binary URL and Hash in the Catalog")

This integrity anchoring step establishes a cryptographic trust reference before the catalog is ever signed or distributed. Subsequent validation steps rely on this recorded hash to prevent altered or substituted binaries from being published.
{% endstep %}

{% step %}
### Malware and Reputation Scanning

Before the update is approved for release, the binary undergoes malware validation.

Where file size permits, the binary is uploaded to VirusTotal and scanned across dozens of antivirus engines. The results are reviewed as part of the validation process.

In the example below, the 1Password installer URL is analyzed by VirusTotal. The scan result shows 0 detections out of 94 engines, indicating that no participating security vendor flagged the file or URL as malicious at the time of analysis.

![VirusTotal results showing 0/94 detections](/_images/image-(4169).png "VirusTotal results showing 0/94 detections")

This multi engine scanning step provides broad threat intelligence coverage across commercial and open source detection platforms and reduces the risk of introducing malicious or compromised vendor content into the catalog.

#### Manual Review and Expert Validation

Automated scanning is only one layer of validation. If any antivirus engine flags a file in VirusTotal, the result triggers manual review by the catalog team.

It is not uncommon for one or two engines to flag a file while the majority report it as clean. This can happen due to:

* Heuristic or behavioral detections
* Machine learning false positives
* Reputation scoring anomalies
* Aggressive or overly sensitive signatures

When a detection occurs, the catalog team performs additional validation. This may include:

* Reviewing the detection name and severity
* Comparing results across engines to identify outliers
* Verifying the vendor’s digital signature
* Cross-checking the hash against the official vendor source
* Reviewing additional threat intelligence sources

This human validation step is a key benefit of a curated catalog model. Automated scanning alone cannot always distinguish between a false positive and a real risk. Expert review ensures flagged software is properly investigated before release.

If a detection represents genuine risk, the update does not proceed. If it is confirmed to be a false positive, it may proceed after validation.
{% endstep %}

{% step %}
### Catalog Creation

After validation:

* The binary’s metadata, hash, and download URL are embedded into the catalog metadata
* The catalog is compiled into a CAB file
* The catalog is dual code-signed using a hardware-backed DigiCert certificate

This signing step cryptographically protects the integrity of the metadata, including the stored hash values.

When a catalog has been signed and released, details of the addition, including VirusTotal results can be found at [https://patchmypc.com/catalog-release](https://patchmypc.com/catalog-release).

![https://patchmypc.com/catalog-release](/_images/image-(4170).png "https://patchmypc.com/catalog-release")

Before the catalog metadata is evaluated for publishing by the Publisher, its hash is validated. This can be observed in the PatchMyPC-PackageService.log

![PackageService.log](/_images/image-(4171).png "PackageService.log")
{% endstep %}
{% endstepper %}

## Phase 2: Runtime Validation During Publishing

{% stepper %}
{% step %}
### Vendor Binary Download at Publish Time

When a customer publishes an update, the Publisher downloads the binary directly from the official vendor source using the URL stored in the catalog metadata.

The file download process can be observed in the PatchMyPC.log

![PatchMyPC.log](/_images/image-(4172).png "PatchMyPC.log")
{% endstep %}

{% step %}
### Hash Verification

After downloading the binary, the Publisher calculates its cryptographic hash. That calculated hash is compared to the original hash recorded during catalog creation.

Publishing proceeds only if the hashes match exactly. Specifically, if:

* The vendor distribution point were compromised
* The file were altered after initial validation
* A malicious file were served from the same URL

The hash comparison would fail and publishing would stop. The update would not be published into WSUS, ConfigMgr, or Intune.

The hash (digest) verification can be observed in the PatchMyPC.log.

![PatchMyPC.log](/_images/image-(4173).png "PatchMyPC.log")
{% endstep %}
{% endstepper %}

## Supply Chain Integrity Controls

This two-phase validation model protects against several supply chain risks:

* Vendor mirror compromise
* Content tampering after initial release
* Man-in-the-middle content replacement
* Unauthorized file substitution

Even if a vendor server were compromised after catalog release, the stored hash prevents altered binaries from being published.

The catalog’s digital signature protects metadata integrity. The hash validation protects binary integrity.

Both controls must succeed for publishing to proceed.
# Download PMPC Code-Signing Certificates

_Applies to: Patch My PC Cloud_

## Overview

Patch My PC code-signing certificates are available from the [Patch My PC Community Scripts repository](https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Other/Code%20Signing). Each certificate folder includes a `.cer` file that contains the public code-signing certificate, along with PowerShell scripts that can be used to import or detect the certificate.

Use the `Current` folders for newly signed Patch My PC content.

Use the `Archived` folders only when devices need to continue trusting content signed with a previous Patch My PC certificate. This may be required if you are implementing an AllSigned PowerShell execution policy, WDAC, AppLocker, or similar controls after applications have already been deployed.

## Choose the Certificate to Download

Patch My PC uses separate code-signing certificates for different signed components. Download the `.cer` file that matches the content you need devices to trust.

* **Intune detection and requirement scripts**\
  Download the `.cer` file from `Patch My PC Cloud/Current`.
* **Patch My PC helper scripts**\
  Download the `.cer` file from `Patch My PC Apps/Current`.
* **PSAppDeployToolkit module**\
  Download the `.cer` file from `PSADT/Current`.

## Current and Archived Certificates

The `Current` folders contain the active Patch My PC code-signing certificates used for newly signed content.

The `Archived` folders contain previous Patch My PC code-signing certificates. These are retained because customers may still have deployed applications, scripts, or modules that were signed with an earlier certificate.

If you are only now implementing AllSigned, WDAC, AppLocker, or similar controls, some existing deployed content may have been signed with a previous Patch My PC certificate. In that instance, you may also need to download and deploy the relevant archived certificate.

Previously signed scripts are timestamped, so they are not expected to fail simply because the signing certificate expires. Archived certificates are provided for environments that still need to trust the signer used for previously signed content.

## Download a Certificate

1. Open the Patch My PC Community Scripts repository at [https://github.com/PatchMyPCTeam/Community-Scripts](https://github.com/PatchMyPCTeam/Community-Scripts)
2. Browse to `Other/Code Signing`.
3. Open the folder for the certificate you need:
   * `Patch My PC Cloud`
   * `Patch My PC Apps`
   * `PSADT`
4. Open the `Current` folder, or the relevant `Archived` folder if you need a previous certificate.
5. Select the `.cer` file.
6. Download the raw file and deploy it using your preferred certificate deployment method.

After downloading the certificate, you can deploy it using Intune, Group Policy or another certificate deployment method.

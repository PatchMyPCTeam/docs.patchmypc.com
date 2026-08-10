# Using a Script to Deploy a PMPC Certificate

_Applies to: Patch My PC Cloud_

You can use a script to deploy Patch My PC (PMPC) code-signing certificates to Intune-managed devices. The script imports the selected certificate into the local Trusted Publishers certificate store.

This can be deployed from Intune as a:

* [Platform Script](using-a-script-to-deploy-a-pmpc-certificate.md#deploy-the-certificate-with-a-platform-script)
* [Remediation Script](using-a-script-to-deploy-a-pmpc-certificate.md#using-a-remediation-script)

In environments where an AllSigned PowerShell execution policy is configured, or where script signature checking is enforced for Win32 apps in the Intune admin center, scripts must be signed by a trusted publisher. Deploying the relevant Patch My PC code-signing certificate allows PowerShell to trust scripts and modules signed by Patch My PC.

Download the required script from the Patch My PC Community Scripts repository:

[https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Other/Code%20Signing](https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Other/Code%20Signing)

Use the script from the relevant `Current` folder for newly signed Patch My PC content.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If you are implementing AllSigned, WDAC, AppLocker, or similar controls after applications have already been deployed, some existing deployed content may have been signed with a previous Patch My PC certificate. In that instance, you may also need to deploy the relevant archived certificate from the corresponding `Archived` folder.</p>
<p>Archived folders include the matching import and detection scripts for that certificate. When deploying an archived certificate using the script method, use the scripts from the archived folder rather than the scripts from the `Current` folder.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You can find out more details about these scripts and what they do by reviewing the <a href="https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Other/Code%20Signing#readme">ReadMe.md</a> file included with the scripts.</p>
</blockquote>

## Deploy the Certificate with a Platform Script

Use this section to deploy one of the Patch My PC certificate import scripts as an Intune platform script.

Select the tab that matches the certificate you want to deploy, then use the corresponding script and settings below when following [Create a script policy and assign it](https://learn.microsoft.com/en-us/mem/intune/apps/intune-management-extension#create-a-script-policy-and-assign-it).

{% tabs %}
{% tab title="Intune Detection and Requirement Scripts" %}
### “Platform scripts” tab

<table><thead><tr><th width="120.88885498046875">Field</th><th width="193">Value</th></tr></thead><tbody><tr><td>Add</td><td>Windows 10 and later</td></tr></tbody></table>

### “Basics” tab

<table><thead><tr><th width="121">Field</th><th>Value</th></tr></thead><tbody><tr><td>Name</td><td>A descriptive name for the policy. E.g. “Patch My PC Cloud Trusted Publisher Certificate”</td></tr><tr><td>Description</td><td>Enter an optional description for the policy</td></tr></tbody></table>

### “Script Settings” tab

<table><thead><tr><th width="369">Field</th><th>Value</th></tr></thead><tbody><tr><td>Script location</td><td>Browse to and select <strong>\Patch My PC Cloud\Current\Import-PMPCCloudTrustedPublisherCertificate.ps1</strong></td></tr><tr><td>Run this script using the logged on credentials</td><td>No</td></tr><tr><td>Enforce script signature check</td><td>No</td></tr><tr><td>Run script in 64 bit PowerShell Host</td><td>No</td></tr></tbody></table>

### “Scope tags” tab

Configure as required.

### “Assignments” tab

Assign the configuration template to the desired Entra ID group(s).

### “Review + add” tab

Double-check everything before clicking **Add**.
{% endtab %}

{% tab title="Patch My PC Helper Scripts" %}
### “Platform scripts” tab

<table><thead><tr><th width="120.88885498046875">Field</th><th width="193">Value</th></tr></thead><tbody><tr><td>Add</td><td>Windows 10 and later</td></tr></tbody></table>

### “Basics” tab

<table><thead><tr><th width="121">Field</th><th>Value</th></tr></thead><tbody><tr><td>Name</td><td>A descriptive name for the policy. E.g. “Patch My PC Apps Trusted Publisher Certificate”</td></tr><tr><td>Description</td><td>Enter an optional description for the policy</td></tr></tbody></table>

### “Script Settings” tab

<table><thead><tr><th width="369">Field</th><th>Value</th></tr></thead><tbody><tr><td>Script location</td><td>Browse to and select <strong>\Patch My PC Apps\Current\Import-PMPCAppsTrustedPublisherCertificate.ps1</strong></td></tr><tr><td>Run this script using the logged on credentials</td><td>No</td></tr><tr><td>Enforce script signature check</td><td>No</td></tr><tr><td>Run script in 64 bit PowerShell Host</td><td>No</td></tr></tbody></table>

### “Scope tags” tab

Configure as required.

### “Assignments” tab

Assign the configuration template to the desired Entra ID group(s).

### “Review + add” tab

Double-check everything before clicking **Add**.
{% endtab %}

{% tab title="PSAppDeployToolkit Module" %}
### “Platform scripts” tab

<table><thead><tr><th width="120.88885498046875">Field</th><th width="193">Value</th></tr></thead><tbody><tr><td>Add</td><td>Windows 10 and later</td></tr></tbody></table>

### “Basics” tab

<table><thead><tr><th width="121">Field</th><th>Value</th></tr></thead><tbody><tr><td>Name</td><td>A descriptive name for the policy. E.g. “PSAppDeployToolkit Module Trusted Publisher Certificate”</td></tr><tr><td>Description</td><td>Enter an optional description for the policy</td></tr></tbody></table>

### “Script Settings” tab

<table><thead><tr><th width="369">Field</th><th>Value</th></tr></thead><tbody><tr><td>Script location</td><td>Browse to and select <strong>\PSADT\Current\Import-PSADTTrustedPublisherCertificate.ps1</strong></td></tr><tr><td>Run this script using the logged on credentials</td><td>No</td></tr><tr><td>Enforce script signature check</td><td>No</td></tr><tr><td>Run script in 64 bit PowerShell Host</td><td>No</td></tr></tbody></table>

### “Scope tags” tab

Configure as required.

### “Assignments” tab

Assign the configuration template to the desired Entra ID group(s).

### “Review + add” tab

Double-check everything before clicking **Add**.
{% endtab %}
{% endtabs %}

## Deploy the Certificate with a Remediation Script

Use this section to deploy one of the Patch My PC certificate import scripts as an Intune remediation script.

Select the tab that matches the certificate you want to deploy, then use the corresponding detection script, remediation script, and settings below when following the the [Remediations](https://learn.microsoft.com/en-us/mem/intune/fundamentals/remediations) article.&#x20;

The Remediation scripts can be found in the following repoistory on GitHub [https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Other/Code%20Signing](https://github.com/PatchMyPCTeam/Community-Scripts/tree/main/Other/Code%20Signing)

{% tabs %}
{% tab title="Intune Detection and Requirement Scripts" %}
### “Basics” tab

<table><thead><tr><th width="115">Field</th><th width="414">Value</th></tr></thead><tbody><tr><td>Name</td><td>A descriptive name for the policy. E.g. “Patch My PC Cloud Trusted Publisher Certificate”</td></tr><tr><td>Description</td><td>Enter an optional description for the policy.</td></tr><tr><td>Publisher</td><td>Enter “Patch My PC”</td></tr></tbody></table>

### “Settings” tab

<table><thead><tr><th width="291">Field</th><th>Value</th></tr></thead><tbody><tr><td>Detection script file</td><td>Browse to and select <strong>\Patch My PC Cloud\Current\PMPCCloudTrustedPublisherCertificate_HealthScript_Detection.ps1</strong></td></tr><tr><td>Remediation script file</td><td>Browse to and select <strong>\Patch My PC Cloud\Current\Import-PMPCCloudTrustedPublisherCertificate.ps1</strong></td></tr><tr><td>Run this script using the logged on credentials</td><td>No</td></tr><tr><td>Enforce script signature check</td><td>No</td></tr><tr><td>Run script in 64 bit PowerShell Host</td><td>No</td></tr></tbody></table>

### “Scope tags” tab

Configure as required.

### “Assignments” tab

Assign the configuration template to the desired Entra ID group(s), then configure the frequency you want the Proactive Remediation to be executed on the targeted devices.

### “Review + create” tab

Double-check everything before clicking **Create**.
{% endtab %}

{% tab title="Patch My PC Helper Scripts" %}
### “Basics” tab

<table><thead><tr><th width="115">Field</th><th width="414">Value</th></tr></thead><tbody><tr><td>Name</td><td>A descriptive name for the policy. E.g. “Patch My PC Apps Trusted Publisher Certificate”</td></tr><tr><td>Description</td><td>Enter an optional description for the policy.</td></tr><tr><td>Publisher</td><td>Enter “Patch My PC”</td></tr></tbody></table>

### “Settings” tab

<table><thead><tr><th width="291">Field</th><th>Value</th></tr></thead><tbody><tr><td>Detection script file</td><td>Browse to and select <strong>\Patch My PC Apps\Current\PMPCAppsTrustedPublisherCertificate_HealthScript_Detection.ps1</strong></td></tr><tr><td>Remediation script file</td><td>Browse to and select <strong>\Patch My PC Apps\Current\Import-PMPCAppsTrustedPublisherCertificate.ps1</strong></td></tr><tr><td>Run this script using the logged on credentials</td><td>No</td></tr><tr><td>Enforce script signature check</td><td>No</td></tr><tr><td>Run script in 64 bit PowerShell Host</td><td>No</td></tr></tbody></table>

### “Scope tags” tab

Configure as required.

### “Assignments” tab

Assign the configuration template to the desired Entra ID group(s), then configure the frequency you want the Proactive Remediation to be executed on the targeted devices.

### “Review + create” tab

Double-check everything before clicking **Create**.
{% endtab %}

{% tab title="PSAppDeployToolkit Module" %}
### “Basics” tab

<table><thead><tr><th width="115">Field</th><th width="414">Value</th></tr></thead><tbody><tr><td>Name</td><td>A descriptive name for the policy. E.g. “PSAppDeployToolkit Module Trusted Publisher Certificate”</td></tr><tr><td>Description</td><td>Enter an optional description for the policy.</td></tr><tr><td>Publisher</td><td>Enter “Patch My PC”</td></tr></tbody></table>

### “Settings” tab

<table><thead><tr><th width="291">Field</th><th>Value</th></tr></thead><tbody><tr><td>Detection script file</td><td>Browse to and select <strong>\PSADT\Current\PSADTTrustedPublisherCertificate_HealthScript_Detection.ps1</strong></td></tr><tr><td>Remediation script file</td><td>Browse to and select <strong>\PSADT\Current\Import-PSADTTrustedPublisherCertificate.ps1</strong></td></tr><tr><td>Run this script using the logged on credentials</td><td>No</td></tr><tr><td>Enforce script signature check</td><td>No</td></tr><tr><td>Run script in 64 bit PowerShell Host</td><td>No</td></tr></tbody></table>

### “Scope tags” tab

Configure as required.

### “Assignments” tab

Assign the configuration template to the desired Entra ID group(s), then configure the frequency you want the Proactive Remediation to be executed on the targeted devices.

### “Review + create” tab

Double-check everything before clicking **Create**.
{% endtab %}
{% endtabs %}

## Post Processing

You can see the script being processed by the Intune Management Extension by looking in the **HealthScriptss.log** located at:

```
%ProgramData%\Microsoft\IntuneManagementExtension\Logs
```

Observe the **Proactive Remediation Device Status** blade.

![Observing the "Proactive Remediation Device Status" blade.](/_images/image-(1351).png "Observing the “Proactive Remediation Device Status” blade.")

The following log snippet shows the **HealthScripts.log** entry if the pre-remediation (detection) script found the certificate already installed in the local computer’s Trusted Publishers store.

!["HealthScripts.log" snippet showing if the pre-remediation (detection) script has found the certificate already installed in the local machine's Trusted Publishers store.](/_images/image-(1352).png "“HealthScripts.log” snippet showing if the pre-remediation (detection) script has found the certificate already installed in the local machine’s Trusted Publishers store.")

The following log snippet shows the **HealthScripts.log** entry if the pre-remediation (detection) script did not find the certificate already installed in the local machine’s Trusted Publishers store (the Exit code of the script is **1**).

!["HealthScripts.log" snippet showing if the pre-remediation (detection) script did not find the certificate already installed in the local machine's Trusted Publishers store (the Exit code of the script is 1).](/_images/image-(1353).png "“HealthScripts.log” snippet showing if the pre-remediation (detection) script did not find the certificate already installed in the local machine’s Trusted Publishers store (the Exit code of the script is 1).")

The following log snippet shows the **HealthScripts.log** entry if the pre-remediation (detection) script did not find the certificate already installed in the local machine’s Trusted Publishers store and the remediation script was run successfully (Exit code of the script is **0**).

!["HealthScripts.log" snippet showing the pre-remediation (detection) script did not find the certificate already installed in the local machine's Trusted Publishers store and the remediation script was run successfully (Exit code of the script is 0).](/_images/image-(1354).png "“HealthScripts.log” snippet showing the pre-remediation (detection) script did not find the certificate already installed in the local machine’s Trusted Publishers store and the remediation script was run successfully (Exit code of the script is 0).")
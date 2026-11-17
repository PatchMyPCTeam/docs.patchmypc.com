---
description: >-
  Install the Patch My PC Cloud Customer API PowerShell module, connect, and
  find the cmdlet for each task.
noIndex: true
noRobotsIndex: true
---

# PowerShell module

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

The `PatchMyPC.Cloud` PowerShell module lets you manage applications and deployments in the Patch My PC Cloud Customer API from a script, a scheduled task, or the PowerShell console. It has one cmdlet for each SDK method, and it calls the same service as the SDK and the REST API.

## Install the module

The module requires PowerShell 7.4 or later on Windows, macOS, or Linux. It's published to the PowerShell Gallery. To install it for your user account, run:

{% code collapsedlinecount="10" %}
```powershell
Install-Module PatchMyPC.Cloud -Scope CurrentUser
```
{% endcode %}

Then import it:

{% code collapsedlinecount="10" %}
```powershell
Import-Module PatchMyPC.Cloud
```
{% endcode %}

## Connect

Every cmdlet that calls the Cloud Customer API needs a connected session. Connect with a personal access token (PAT) that you created in the Patch My PC portal under **Settings** > **Access Tokens**. [Connect-PmpcCloudWithPat](connect-pmpccloudwithpat.md) exchanges the PAT for an access token, and exchanges the PAT again when the access token expires. Use `-Region` for the region your account is in.

{% code collapsedlinecount="10" %}
```powershell
$token = Read-Host -AsSecureString 'PAT'
Connect-PmpcCloudWithPat -Token $token -Region Us
Get-PmpcCustomerInfo
```
{% endcode %}

The session can do everything the token's scopes allow. To create a PAT, choose its scopes, or revoke it, use the portal; see [Create a personal access token](../create-a-personal-access-token.md).

## Get help offline

The help on these pages ships with the module, so `Get-Help` works without an internet connection. For example:

{% code collapsedlinecount="10" %}
```powershell
Get-Help New-PmpcDeployment -Full
Get-Help New-PmpcDeployment -Examples
```
{% endcode %}

## Cmdlets by area

### Session and authentication

| Cmdlet                                                  | Synopsis                                                               |
| ------------------------------------------------------- | ---------------------------------------------------------------------- |
| [Connect-PmpcCloudWithPat](connect-pmpccloudwithpat.md) | Authenticates using a personal access token.                           |
| [Disconnect-PmpcCloud](disconnect-pmpccloud.md)         | Signs out and tears down the module's session.                         |
| [Get-PmpcCloudSession](get-pmpccloudsession.md)         | Reports the module's current session state.                            |
| [Test-PmpcCloudHealth](test-pmpccloudhealth.md)         | Checks whether the Cloud Customer API responds to a heartbeat request. |
| [Get-PmpcSelectedCompany](get-pmpcselectedcompany.md)   | Gets the company the session is currently scoped to.                   |

### Customer and connections

| Cmdlet                                                      | Synopsis                                                            |
| ----------------------------------------------------------- | ------------------------------------------------------------------- |
| [Get-PmpcCustomerInfo](get-pmpccustomerinfo.md)             | Gets account information and usage limits for the current customer. |
| [Get-PmpcConnection](get-pmpcconnection.md)                 | Lists the Intune connections available to the selected company.     |
| [Set-PmpcConnection](set-pmpcconnection.md)                 | Selects the Intune connection that deployment commands act on.      |
| [Get-PmpcSelectedConnection](get-pmpcselectedconnection.md) | Gets the Intune connection the session is currently scoped to.      |

### Applications

| Cmdlet                                                | Synopsis                                                       |
| ----------------------------------------------------- | -------------------------------------------------------------- |
| [Find-PmpcApplication](find-pmpcapplication.md)       | Searches the Patch My PC public catalog.                       |
| [Get-PmpcApplication](get-pmpcapplication.md)         | Gets the details of a single public catalog application.       |
| [Get-PmpcApplicationFile](get-pmpcapplicationfile.md) | Lists the files that make up an application's current version. |

### Custom applications

| Cmdlet                                                          | Synopsis                                             |
| --------------------------------------------------------------- | ---------------------------------------------------- |
| [Find-PmpcCustomApplication](find-pmpccustomapplication.md)     | Searches the customer's custom applications catalog. |
| [Get-PmpcCustomApplication](get-pmpccustomapplication.md)       | Gets the details of a single custom application.     |
| [New-PmpcCustomApplication](new-pmpccustomapplication.md)       | Creates a custom application and uploads its files.  |
| [Update-PmpcCustomApplication](update-pmpccustomapplication.md) | Publishes a new version of an existing application.  |
| [Set-PmpcCustomApplication](set-pmpccustomapplication.md)       | Edits an application's current version in place.     |
| [Remove-PmpcCustomApplication](remove-pmpccustomapplication.md) | Deletes a custom application.                        |
| [New-PmpcDetectionRule](new-pmpcdetectionrule.md)               | Builds a detection rule set.                         |
| [New-PmpcFileRule](new-pmpcfilerule.md)                         | Builds a file or folder rule.                        |
| [New-PmpcRegistryRule](new-pmpcregistryrule.md)                 | Builds a registry rule.                              |
| [New-PmpcScriptRule](new-pmpcscriptrule.md)                     | Builds a script rule.                                |
| [New-PmpcRequirement](new-pmpcrequirement.md)                   | Builds an application's installation requirements.   |

### Deployments

| Cmdlet                                                                            | Synopsis                                                             |
| --------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| [Get-PmpcDeployment](get-pmpcdeployment.md)                                       | Gets an application's Intune deployments, or one deployment in full. |
| [Get-PmpcDeploymentDependencyCandidate](get-pmpcdeploymentdependencycandidate.md) | Lists deployments that can be used as a dependency.                  |
| [New-PmpcDeployment](new-pmpcdeployment.md)                                       | Creates an Intune deployment for an application.                     |
| [Set-PmpcDeployment](set-pmpcdeployment.md)                                       | Changes an existing Intune deployment.                               |
| [Remove-PmpcDeployment](remove-pmpcdeployment.md)                                 | Deletes an Intune deployment.                                        |
| [Restart-PmpcDeployment](restart-pmpcdeployment.md)                               | Forces a deployment to be recreated in Intune.                       |
| [Sync-PmpcDeployment](sync-pmpcdeployment.md)                                     | Syncs a deployment to its latest pending version.                    |
| [Suspend-PmpcDeployment](suspend-pmpcdeployment.md)                               | Pauses a deployment's scheduled sync.                                |
| [Resume-PmpcDeployment](resume-pmpcdeployment.md)                                 | Resumes a deployment's scheduled sync.                               |
| [New-PmpcDeploymentAssignment](new-pmpcdeploymentassignment.md)                   | Builds an assignment for a deployment.                               |
| [New-PmpcDeploymentConfiguration](new-pmpcdeploymentconfiguration.md)             | Builds a deployment's optional configuration block.                  |
| [New-PmpcDeploymentAppInfo](new-pmpcdeploymentappinfo.md)                         | Builds the catalogue metadata shown for a deployment.                |
| [New-PmpcDeploymentRequirement](new-pmpcdeploymentrequirement.md)                 | Builds a deployment's installation requirements.                     |
| [New-PmpcDeploymentReturnCode](new-pmpcdeploymentreturncode.md)                   | Builds one installer exit code and the outcome it maps to.           |

### Deployment templates

| Cmdlet                                                            | Synopsis                                            |
| ----------------------------------------------------------------- | --------------------------------------------------- |
| [Get-PmpcDeploymentTemplate](get-pmpcdeploymenttemplate.md)       | Lists deployment templates, or reads one in detail. |
| [New-PmpcDeploymentTemplate](new-pmpcdeploymenttemplate.md)       | Creates a deployment template.                      |
| [Set-PmpcDeploymentTemplate](set-pmpcdeploymenttemplate.md)       | Replaces the settings on a deployment template.     |
| [Remove-PmpcDeploymentTemplate](remove-pmpcdeploymenttemplate.md) | Deletes a deployment template.                      |

## Related pages

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)
* [SDK reference](../sdk/)
* [REST API reference](../rest-api/)

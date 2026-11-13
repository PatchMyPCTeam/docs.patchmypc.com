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

```powershell
Install-Module PatchMyPC.Cloud -Scope CurrentUser
```

Then import it:

```powershell
Import-Module PatchMyPC.Cloud
```

## Connect

Every cmdlet that calls the Cloud Customer API needs a connected session. Connect with a personal access token (PAT) that you created in the Patch My PC portal under **Settings** > **Access Tokens**. [Connect-PmpcCloudWithPat](connect-pmpccloudwithpat.md) exchanges the PAT for an access token, and exchanges the PAT again when the access token expires. Use `-Region` for the region your account is in.

```powershell
$token = Read-Host -AsSecureString 'PAT'
Connect-PmpcCloudWithPat -Token $token -Region Us
Get-PmpcCustomerInfo
```

The session can do everything the token's scopes allow. To create a PAT, choose its scopes, or revoke it, use the portal; see [Create a personal access token](../create-a-personal-access-token.md).

## Get help offline

The help on these pages ships with the module, so `Get-Help` works without an internet connection. For example:

```powershell
Get-Help New-PmpcDeployment -Full
Get-Help New-PmpcDeployment -Examples
```

## Cmdlets by area

Cmdlets marked as requiring enablement work only after the feature is enabled for your account. Until then they report the error code `FEATURE_NOT_ENABLED`.

### Session and authentication

| Cmdlet                                                  | Synopsis                                                               | Requires enablement |
| ------------------------------------------------------- | ---------------------------------------------------------------------- | ------------------- |
| [Connect-PmpcCloudWithPat](connect-pmpccloudwithpat.md) | Authenticates using a personal access token.                           | No                  |
| [Disconnect-PmpcCloud](disconnect-pmpccloud.md)         | Signs out and tears down the module's session.                         | No                  |
| [Get-PmpcCloudSession](get-pmpccloudsession.md)         | Reports the module's current session state.                            | No                  |
| [Test-PmpcCloudHealth](test-pmpccloudhealth.md)         | Checks whether the Patch My PC Cloud service is reachable and healthy. | No                  |
| [Get-PmpcSelectedCompany](get-pmpcselectedcompany.md)   | Gets the company the session is currently scoped to.                   | No                  |

### Customer and connections

| Cmdlet                                                      | Synopsis                                                            | Requires enablement |
| ----------------------------------------------------------- | ------------------------------------------------------------------- | ------------------- |
| [Get-PmpcCustomerInfo](get-pmpccustomerinfo.md)             | Gets account information and usage limits for the current customer. | No                  |
| [Get-PmpcConnection](get-pmpcconnection.md)                 | Lists the Intune connections available to the selected company.     | Yes                 |
| [Set-PmpcConnection](set-pmpcconnection.md)                 | Selects the Intune connection that deployment commands act on.      | Yes                 |
| [Get-PmpcSelectedConnection](get-pmpcselectedconnection.md) | Gets the Intune connection the session is currently scoped to.      | No                  |

### Applications

| Cmdlet                                                | Synopsis                                                       | Requires enablement |
| ----------------------------------------------------- | -------------------------------------------------------------- | ------------------- |
| [Find-PmpcApplication](find-pmpcapplication.md)       | Searches the Patch My PC public catalog.                       | Yes                 |
| [Get-PmpcApplication](get-pmpcapplication.md)         | Gets the details of a single public catalog application.       | Yes                 |
| [Get-PmpcApplicationFile](get-pmpcapplicationfile.md) | Lists the files that make up an application's current version. | Yes                 |

### Custom applications

| Cmdlet                                                          | Synopsis                                             | Requires enablement |
| --------------------------------------------------------------- | ---------------------------------------------------- | ------------------- |
| [Find-PmpcCustomApplication](find-pmpccustomapplication.md)     | Searches the customer's custom applications catalog. | Yes                 |
| [Get-PmpcCustomApplication](get-pmpccustomapplication.md)       | Gets the details of a single custom application.     | Yes                 |
| [New-PmpcCustomApplication](new-pmpccustomapplication.md)       | Creates a custom application and uploads its files.  | Yes                 |
| [Update-PmpcCustomApplication](update-pmpccustomapplication.md) | Publishes a new version of an existing application.  | Yes                 |
| [Set-PmpcCustomApplication](set-pmpccustomapplication.md)       | Edits an application's current version in place.     | Yes                 |
| [Remove-PmpcCustomApplication](remove-pmpccustomapplication.md) | Deletes a custom application.                        | Yes                 |
| [New-PmpcDetectionRule](new-pmpcdetectionrule.md)               | Builds a detection rule set.                         | No                  |
| [New-PmpcFileRule](new-pmpcfilerule.md)                         | Builds a file or folder rule.                        | No                  |
| [New-PmpcRegistryRule](new-pmpcregistryrule.md)                 | Builds a registry rule.                              | No                  |
| [New-PmpcScriptRule](new-pmpcscriptrule.md)                     | Builds a script rule.                                | No                  |
| [New-PmpcRequirement](new-pmpcrequirement.md)                   | Builds an application's installation requirements.   | No                  |

### Deployments

| Cmdlet                                                                            | Synopsis                                                             | Requires enablement |
| --------------------------------------------------------------------------------- | -------------------------------------------------------------------- | ------------------- |
| [Get-PmpcDeployment](get-pmpcdeployment.md)                                       | Gets an application's Intune deployments, or one deployment in full. | Yes                 |
| [Get-PmpcDeploymentDependencyCandidate](get-pmpcdeploymentdependencycandidate.md) | Lists deployments that can be used as a dependency.                  | Yes                 |
| [New-PmpcDeployment](new-pmpcdeployment.md)                                       | Creates an Intune deployment for an application.                     | Yes                 |
| [Set-PmpcDeployment](set-pmpcdeployment.md)                                       | Changes an existing Intune deployment.                               | Yes                 |
| [Remove-PmpcDeployment](remove-pmpcdeployment.md)                                 | Deletes an Intune deployment.                                        | Yes                 |
| [Restart-PmpcDeployment](restart-pmpcdeployment.md)                               | Forces a deployment to be recreated in Intune.                       | Yes                 |
| [Sync-PmpcDeployment](sync-pmpcdeployment.md)                                     | Syncs a deployment to its latest pending version.                    | Yes                 |
| [Suspend-PmpcDeployment](suspend-pmpcdeployment.md)                               | Pauses a deployment's scheduled sync.                                | Yes                 |
| [Resume-PmpcDeployment](resume-pmpcdeployment.md)                                 | Resumes a deployment's scheduled sync.                               | Yes                 |
| [New-PmpcDeploymentAssignment](new-pmpcdeploymentassignment.md)                   | Builds an assignment for a deployment.                               | No                  |
| [New-PmpcDeploymentConfiguration](new-pmpcdeploymentconfiguration.md)             | Builds a deployment's optional configuration block.                  | No                  |
| [New-PmpcDeploymentAppInfo](new-pmpcdeploymentappinfo.md)                         | Builds the catalogue metadata shown for a deployment.                | No                  |
| [New-PmpcDeploymentRequirement](new-pmpcdeploymentrequirement.md)                 | Builds a deployment's installation requirements.                     | No                  |
| [New-PmpcDeploymentReturnCode](new-pmpcdeploymentreturncode.md)                   | Builds one installer exit code and the outcome it maps to.           | No                  |

### Deployment templates

| Cmdlet                                                            | Synopsis                                            | Requires enablement |
| ----------------------------------------------------------------- | --------------------------------------------------- | ------------------- |
| [Get-PmpcDeploymentTemplate](get-pmpcdeploymenttemplate.md)       | Lists deployment templates, or reads one in detail. | Yes                 |
| [New-PmpcDeploymentTemplate](new-pmpcdeploymenttemplate.md)       | Creates a deployment template.                      | Yes                 |
| [Set-PmpcDeploymentTemplate](set-pmpcdeploymenttemplate.md)       | Replaces the settings on a deployment template.     | Yes                 |
| [Remove-PmpcDeploymentTemplate](remove-pmpcdeploymenttemplate.md) | Deletes a deployment template.                      | Yes                 |

## Related pages

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)
* SDK reference
* REST API reference

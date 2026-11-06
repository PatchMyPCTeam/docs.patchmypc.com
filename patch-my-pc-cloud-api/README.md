---
description: >-
  Search the Patch My PC catalog, publish custom applications, and manage
  deployments from your own tools and scripts.
hidden: true
noIndex: true
noRobotsIndex: true
---

# Patch My PC Cloud Customer API

The Patch My PC Cloud Customer API gives your own applications, scripts, and pipelines programmatic access to your Patch My PC cloud account. With the Cloud Customer API you can:

* **Search the Patch My PC catalog** and your own custom applications, and read application details.
* **Create and update custom applications**, including uploading the installer files.
* **Manage deployments** of applications to your Microsoft Intune connections—create, edit, sync, pause, redeploy, and delete them.
* **Automate without a person at the keyboard** by using personal access tokens (PATs) that carry only the scopes a job needs.

## Choose how to use the Cloud Customer API

You can reach the same operations in three ways. Pick the one that fits your tooling—all three use the same account, permissions, and rate limits.

| Surface                                      | Best for                                                                          | Authentication                                              |
| -------------------------------------------- | --------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| REST API                                     | Any language or platform that can send HTTPS requests                             | Access token obtained by exchanging a personal access token |
| .NET SDK (`pmpc.appcatbroker.sdk`)           | .NET 8 and .NET 10 applications                                                   | Personal access token                                       |
| PowerShell module (`PatchMyPC.AppCatBroker`) | Administrators and scripts on PowerShell 7.4 or later on Windows, macOS, or Linux | Personal access token                                       |

{% content-ref url="rest-api/" %}
[rest-api](rest-api/)
{% endcontent-ref %}

{% content-ref url="sdk/" %}
[sdk](sdk/)
{% endcontent-ref %}

{% content-ref url="powershell/" %}
[powershell](powershell/)
{% endcontent-ref %}

{% hint style="info" %}
Some operations—for example deployments and editing or deleting applications—must be enabled for your account before you can use them. The pages that describe those operations say so.
{% endhint %}

## Contents

### Start here

* [Getting started](getting-started.md) walks you through the prerequisites and your first call.
* [Authentication](authentication.md) explains how to exchange a personal access token for an access token and send it with each request.
* [Create a personal access token](create-a-personal-access-token.md) shows how to create, view, and revoke tokens in the Patch My PC portal.
* [Errors](errors.md) describes the status codes and error codes the Cloud Customer API returns.
* [Rate limits](rate-limits.md) describes how much traffic the Cloud Customer API accepts and how to retry.

### Guides

* [Search the catalog](guides/search-the-catalog.md)
* [Create a custom application](guides/create-a-custom-application.md)
* [Update an application](guides/update-an-application.md)
* [Deploy an application](guides/deploy-an-application.md)
* [Automate with a personal access token](guides/automate-with-a-personal-access-token.md)

### REST API

* REST API reference
  * [Authentication](rest-api/authentication.md)
  * [Applications](rest-api/applications.md)

### .NET SDK

* .NET SDK
  * [Install and configure the SDK](sdk/install-and-configure.md)
  * [Results and errors](sdk/results-and-errors.md)
  * [SDK authentication methods](sdk/authentication.md)
  * [Customer information and connections](sdk/customer-and-connections.md)
  * [Applications](sdk/applications.md)
  * [Custom applications](sdk/custom-applications.md)
  * [Deployments](sdk/deployments.md)
  * [Deployment templates](sdk/deployment-templates.md)

### PowerShell module

* PowerShell module
  * [Connect-PmpcBrokerWithPat](powershell/connect-pmpcbrokerwithpat.md)
  * [Disconnect-PmpcBroker](powershell/disconnect-pmpcbroker.md)
  * [Find-PmpcApplication](powershell/find-pmpcapplication.md)
  * [Find-PmpcCustomApplication](powershell/find-pmpccustomapplication.md)
  * [Get-PmpcApplication](powershell/get-pmpcapplication.md)
  * [Get-PmpcApplicationFile](powershell/get-pmpcapplicationfile.md)
  * [Get-PmpcBrokerSession](powershell/get-pmpcbrokersession.md)
  * [Get-PmpcConnection](powershell/get-pmpcconnection.md)
  * [Get-PmpcCustomApplication](powershell/get-pmpccustomapplication.md)
  * [Get-PmpcCustomerInfo](powershell/get-pmpccustomerinfo.md)
  * [Get-PmpcDeployment](powershell/get-pmpcdeployment.md)
  * [Get-PmpcDeploymentDependencyCandidate](powershell/get-pmpcdeploymentdependencycandidate.md)
  * [Get-PmpcDeploymentTemplate](powershell/get-pmpcdeploymenttemplate.md)
  * [Get-PmpcSelectedCompany](powershell/get-pmpcselectedcompany.md)
  * [Get-PmpcSelectedConnection](powershell/get-pmpcselectedconnection.md)
  * [New-PmpcCustomApplication](powershell/new-pmpccustomapplication.md)
  * [New-PmpcDeployment](powershell/new-pmpcdeployment.md)
  * [New-PmpcDeploymentAppInfo](powershell/new-pmpcdeploymentappinfo.md)
  * [New-PmpcDeploymentAssignment](powershell/new-pmpcdeploymentassignment.md)
  * [New-PmpcDeploymentConfiguration](powershell/new-pmpcdeploymentconfiguration.md)
  * [New-PmpcDeploymentRequirement](powershell/new-pmpcdeploymentrequirement.md)
  * [New-PmpcDeploymentReturnCode](powershell/new-pmpcdeploymentreturncode.md)
  * [New-PmpcDeploymentTemplate](powershell/new-pmpcdeploymenttemplate.md)
  * [New-PmpcDetectionRule](powershell/new-pmpcdetectionrule.md)
  * [New-PmpcFileRule](powershell/new-pmpcfilerule.md)
  * [New-PmpcRegistryRule](powershell/new-pmpcregistryrule.md)
  * [New-PmpcRequirement](powershell/new-pmpcrequirement.md)
  * [New-PmpcScriptRule](powershell/new-pmpcscriptrule.md)
  * [Remove-PmpcCustomApplication](powershell/remove-pmpccustomapplication.md)
  * [Remove-PmpcDeployment](powershell/remove-pmpcdeployment.md)
  * [Remove-PmpcDeploymentTemplate](powershell/remove-pmpcdeploymenttemplate.md)
  * [Restart-PmpcDeployment](powershell/restart-pmpcdeployment.md)
  * [Resume-PmpcDeployment](powershell/resume-pmpcdeployment.md)
  * [Set-PmpcConnection](powershell/set-pmpcconnection.md)
  * [Set-PmpcCustomApplication](powershell/set-pmpccustomapplication.md)
  * [Set-PmpcDeployment](powershell/set-pmpcdeployment.md)
  * [Set-PmpcDeploymentTemplate](powershell/set-pmpcdeploymenttemplate.md)
  * [Suspend-PmpcDeployment](powershell/suspend-pmpcdeployment.md)
  * [Sync-PmpcDeployment](powershell/sync-pmpcdeployment.md)
  * [Test-PmpcBrokerHealth](powershell/test-pmpcbrokerhealth.md)
  * [Update-PmpcCustomApplication](powershell/update-pmpccustomapplication.md)

### Reference

* [Cross-reference: cmdlets, SDK methods, and REST operations](cross-reference.md)

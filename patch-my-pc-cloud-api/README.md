---
description: >-
  Search the Patch My PC catalog, publish custom applications, and manage
  deployments from your own tools and scripts.
hidden: true
noIndex: true
noRobotsIndex: true
---

# Patch My PC Cloud Customer API

The Patch My PC Cloud Customer API (formerly AppCatBroker) gives your own applications, scripts, and pipelines programmatic access to your Patch My PC cloud account. With the Cloud Customer API you can:

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

## Start here

* [Getting started](getting-started.md) walks you through the prerequisites and your first call.
* [Authentication](authentication.md) explains how to create a personal access token and exchange it for an access token.
* [Errors](errors.md) and [Rate limits](rate-limits.md) describe how the Cloud Customer API reports failures and how much traffic it accepts.
* [Cmdlet, SDK, and REST cross-reference](cross-reference.md) maps every operation across the three surfaces.

{% hint style="info" %}
Some operations—for example deployments and editing or deleting applications—must be enabled for your account before you can use them. The pages that describe those operations say so.
{% endhint %}

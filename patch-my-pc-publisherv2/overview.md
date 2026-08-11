# Overview

_Applies to: Patch My PC Publisher V2.x_

## What is the Publisher?

Patch My PC Publisher is an on-premises publishing service that automates the creation, update, and lifecycle management of third-party applications and updates for Microsoft management platforms.

<figure><img src="../.gitbook/assets/image (4231).png" alt="Patch My PC Publisher" width="563"><figcaption></figcaption></figure>

The Publisher integrates with:

* Windows Server Update Services (WSUS)
* Microsoft Configuration Manager (ConfigMgr)
* Microsoft Intune

It allows organizations to deploy and maintain third-party software using the same native workflows they already use for Microsoft updates and applications.

## Capabilities

The Publisher downloads the Patch My PC catalog to retrieve curated third-party application metadata. Based on your configuration, it can:

* Publish third-party updates to WSUS
* Create and update applications in ConfigMgr
* Create and update Win32 apps (and updates) in Intune
* Maintain and update previously published third-party applications and updates

All publishing actions respect the native security, authentication, and deployment mechanisms of the target platform.

The Publisher does not replace WSUS, ConfigMgr, or Intune. It extends them by automating third-party application packaging and update publishing.

## Supported Scenarios

The Publisher can be used in several deployment models:

* **WSUS Standalone**\
  Publish third-party updates directly into WSUS for organizations not using ConfigMgr.
* **ConfigMgr**\
  Publish third-party updates to WSUS for synchronization into ConfigMgr, and create full ConfigMgr applications for software deployment through Software Center.
* **Intune**\
  Create and maintain Win32 apps (and updates) in Intune using Microsoft Graph.

Many organizations use the Publisher in hybrid scenarios where WSUS, ConfigMgr, and Intune coexist.

## How the Publisher Works

At a high level, the workflow is:

1. The Publisher downloads a [curated catalog](security/overview.md) from Patch My PC.
2. Administrators select which products to enable.
3. During synchronization, the Publisher:
   * Validates catalog integrity
   * Downloads vendor binaries
   * Verifies file hashes
   * Packages content according to customizations and platform requirements
   * Publishes to WSUS, ConfigMgr, and/or Intune
4. The management platform then distributes the update or application to client devices using its native mechanisms.

<figure><img src="../.gitbook/assets/image (4187).png" alt="How the Publisher Works" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

The Publisher is installed on a Windows device and operates within your existing infrastructure and security boundaries.

If you are soley publishing to Intune, we recommend our SaaS based solution, [Patch My PC Cloud](https://portal.patchmypc.com/).
{% endhint %}

## Next Steps

Before installing the Publisher, review [Getting Started](getting-started.md).

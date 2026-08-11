# Remote SUP Requirements

_Applies to: Patch My PC Publisher V2.x_

## Overview

When the SUP role is installed on a remote site system (separate from the site server), there are additional requirements to ensure third-party update publishing and certificate management function correctly.

## Network

When the Publisher is installed on a remote SUP, there are additional network requirements which can be found on the [ConfigMgr Requirements > Network](../network.md) page.

## Software

When the Publisher is installed on a remote SUP, it is important that the ConfigMgr Console is also installed on the remote SUP to facilitate interactions from the Publisher to ConfigMgr, through the ConfigMgr SDK, via the SMS Provider. More information can be found on the [ConfigMgr Requirements > Software](../software.md) page.

## ConfigMgr Security Role

When the Publisher is installed on the site server, it already has the required permissions to interact with ConfigMgr because the service runs under the SYSTEM account. When the Publisher is installed on a remote SUP, these permissions may not be present by default. In that case, the Publisher requires specific ConfigMgr permissions to create, modify, and distribute applications and updates. These permissions can be granted through a Security Role which can be created automatically by the Publisher or configured manually by an administrator.

{% hint style="warning" %}
**Important**

While the Publisher can create the necessary Security Role automatically, an administrator still needs to add the computer account of the remote SUP to that Security Role in the ConfigMgr console.
{% endhint %}

There are 2 options to ensure the Publisher, installed on a remote SUP, has the correct permissions.

### Option 1: Automatically Create the ConfigMger Security Role (Recommended)

Publisher has the ability to create a Security Role in ConfigMgr with the minimum required permissions to interact with the required ConfigMgr components. See [Connection and Source Options](../../../administration/configmgr-apps/options/connection-and-source-options.md) for configuration steps.

### Option 2: Manually Create the ConfigMgr Security Role

If your organization requires manual role creation or approval by a security team, you can create the role yourself and assign it to the computer account of the remote SUP.

The Publisher requires the following ConfigMgr permissions:

* **Application**\
  Read, Modify, Delete, Set Security Scope, Create, Move Object, Modify Folder
* **Distribution Point**\
  Read, Copy to Distribution Point
* **Distribution Point Group**\
  Read, Copy to Distribution Point Group
* **Folder Class**\
  Read, Modify, Create
* **Security Scopes**\
  Read
* **Site**\
  Read
* **Software Updates**\
  Read, Modify

<figure><img src="../../../../.gitbook/assets/image (378).png" alt="Security Role permissions required for the Publisher" width="563"><figcaption></figcaption></figure>

It is important that you also assign this role to the computer$ account of the remote SUP.

<figure><img src="../../../../.gitbook/assets/image (379).png" alt="Assign the role to the computer account of the remote SUP" width="563"><figcaption></figcaption></figure>

The Security Scopes should be assigned to **All instances of the objects that are related to the assigned security roles**.

<figure><img src="../../../../.gitbook/assets/image (380).png" alt="All instances of the objects that are related to the assigned security roles" width="392"><figcaption></figcaption></figure>

## WSUS SSL Requirements

SSL is required on the remote SUP WSUS instance if there is an expectation that ConfigMgr can retrieve the signing certificate and distribute it to client devices.

If WSUS on a remote SUP _is not_ configured for SSL, `wsyncmgr.log` will log the following warning during a SUP sync:

> `Remote WSUS connection is not HTTPS. This prevents software update point from getting the signing certificate for third-party updates`

<figure><img src="../../../../.gitbook/assets/image (381).png" alt="Remote WSUS connection is not HTTPS" width="563"><figcaption></figcaption></figure>

This warning indicates that ConfigMgr is unable to retrieve the WSUS signing certificate from the remote SUP. As a result, ConfigMgr cannot store the certificate in the site database or distribute it to client devices during a software update scan. To resolve this, WSUS on the remote SUP must be configured to use HTTPS (SSL) when Configuration Manager is set to manage the signing certificate.

For more information on enabling SSL for WSUS, see [https://learn.microsoft.com/en-us/intune/configmgr/sum/get-started/software-update-point-ssl](https://learn.microsoft.com/en-us/intune/configmgr/sum/get-started/software-update-point-ssl)

{% hint style="info" %}
**Note**

SSL is not a strict requirement in this scenario. However, when SSL is not enabled on a remote SUP, the code-signing certificate must be manually distributed to the site server, any other SUPs, and all client devices.&#x20;

The certificate must be placed in the **Trusted Publishers** (and the **Trusted Root Certification Authorities** store if its a self-signed certificate) using Group Policy or another certificate deployment method.&#x20;
{% endhint %}

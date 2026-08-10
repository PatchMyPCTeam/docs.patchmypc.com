---
description: >-
  When working with a WSUS or Configuration Manager implementation, proper
  certificate configuration is crucial.  Microsoft requires all updates to be
  signed.
---

# Certificate Configuration

_Applies to: On-premises Publisher_

## Certificates

When working with a Configuration Manager or WSUS implementation, proper certificate configuration is crucial. One way **Microsoft helps ensure an update is considered secure and from a trusted source** is through the utilization of a code signing certificate. This requirement means all custom updates must be code signed before injection into WSUS. We provide a couple of different ways to configure the certificate.

* [Creating the WSUS Signing Certificate using Patch My PC’s Publisher](https://patchmypc.com/wsus-signing-certificate-options-for-third-party-updates-in-configuration-manager#topic4)
* [Import a PKI Based Certificate Using Patch My PC’s Publisher](https://patchmypc.com/wsus-signing-certificate-options-for-third-party-updates-in-configuration-manager#topic5)

To read our in-depth guide on certificates click the link below.

{% embed url="https://patchmypc.com/wsus-signing-certificate-options-for-third-party-updates-in-configuration-manager" %}

In the steps below, we'll walk through creating a self-signed certificate using Patch My PC's Publisher.

### Create WSUS Signing Certificate Using the Patch My PC Publisher

1. Select **Generate a Self-Signed Certificate** in the Publisher.
2. By default, it will be set to 5 years but you can change the number of years the certificate is valid for.
3. The other configuration you get from the publisher is that by default we do allow the private key to be exported. The benefit with that is that you do have the ability, if you move to a different WSUS server, to export the code-signing certificate generated through our tool and import that with the private key. This would allow you to use the same WSUS signing certificate that you were using on the previous WSUS server. That way you do not have to worry about potential clients having to get the certificate redistributed and trusted. The downside, from a security perspective, is that some people may not want that to be exportable because it could allow somebody to use that key in other places.
4. Click **Generate Certificate**. Once that is done we should have the certificate created and we'll be ready to start publishing updates to WSUS.

> \*\*Note\*\*
>
> After the signing certificate is created, you will need to take two actions on the clients for the updates to install successfully:
>
> 1\. The generated code-signing certificate needs to be distributed to the \*\*Trusted Root\*\* and \*\*Trusted Publisher\*\* local machine certificate stores. You can distribute it using a GPO by following [this guide](https://patchmypc.com/how-to-deploy-the-wsus-signing-certificate-for-third-party-software-updates#topic2).\\
>
> If the code-signing certificate was issued from an internal Certification Authority, the certificate needs to be installed in the \*\*Trusted Publishers\*\* store only.
>
> 2\. Allow signed updates for an intranet Microsoft update service location.
>
> 1\. Open regedit.exe, and navigate to: \*\*HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\*\*
>
> 2\. Create a new REG\\\_DWORD value and name it \*\*AcceptTrustedPublisherCerts\*\*
>
> 3\. Set the value to \*\*1\*\*.

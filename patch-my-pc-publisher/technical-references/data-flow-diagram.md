# Data Flow Diagram for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Before looking at the full architecture flow, it is helpful to understand where the Patch My PC (PMPC) Publisher sits in the overall update workflow.

At a high level, Publisher acts as a publishing engine that prepares and delivers third-party updates to the management platforms already used in your environment.

Publisher does not deploy software directly to devices. Instead, it integrates with management platforms (such as Microsoft Intune, WSUS, and ConfigMgr), which remain responsible for policy assignment, update deployment, and device communication.

<figure><img src="../../.gitbook/assets/image (4209).png" alt="High-Level Data Flow" width="563"><figcaption></figcaption></figure>

The more detailed data flow diagram below illustrates how Publisher integrates with WSUS, ConfigMgr, Intune, PMPC Cloud, vendor content sources, and client devices.&#x20;

It represents logical communication flows between components and does not represent firewall rules, network boundaries, or required directional access paths.

{% hint style="info" %}
**Note**

Arrows in the diagram indicate the communication relationships between services. They are intended to show how data moves through the system during publishing, synchronization, and deployment operations. They should not be interpreted as strict one-way connections or prescriptive firewall requirements.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (4167).png" alt="More detailed data flow diagram" width="563"><figcaption></figcaption></figure>

## Core Publishing Flow

Publisher retrieves catalog metadata and configuration details from Patch My PC Cloud Services. When publishing products, installer content is downloaded directly from the vendor’s web servers to Publisher, which then packages the content and publishes it to the selected management platform.

The destination platform determines how the content is processed, synchronized, and delivered to client devices.

### WSUS Updates

When publishing updates to WSUS, Publisher:

* Downloads the update binaries from the vendor.
* Packages them into a CAB file.
* Signs the CAB file with the selected code-signing certificate.&#x20;
* Publishes the update into WSUS.

If WSUS is integrated with ConfigMgr, the update is synchronized from WSUS to ConfigMgr during a Software Update Point (SUP) synchronization. Clients receive the update through the standard WSUS or ConfigMgr software update workflow.

### ConfigMgr Applications

When publishing applications to ConfigMgr, Publisher creates or updates applications directly in the ConfigMgr environment.

Content is downloaded from the vendor, packaged, and distributed to the appropriate distribution points. Client devices then install applications using standard ConfigMgr deployment and Software Center processes.

### Intune Applications and Updates

When publishing to Intune, Publisher communicates with Microsoft Graph to create or update Win32 applications in Microsoft Intune.

Content is downloaded from the vendor, packaged as a Win32 app, and uploaded to Intune. Both Intune Apps and Updates use the native Win32 application model for delivery to endpoints.

## Custom Apps Flow

Customers can create and manage Custom Apps in their PMPC Cloud company. Publisher can connect to the Cloud company and retrieve Custom App definitions for publishing.

PMPC Cloud serves as the configuration layer, whilst Publisher performs packaging and publishing operations within the customer environment.

An Enterprise Application in Entra ID is required only to allow users to sign in to PMPC Cloud. This registration provides delegated permissions for authentication and identity verification.

It is included in the diagram to illustrate the authentication flow to PMPC Cloud. It does not indicate that the Enterprise Application is used to publish apps or updates to Intune.

## Client Flow

Client devices communicate only with their management platform, either WSUS, ConfigMgr, or Intune. They do not communicate directly with Publisher.

Publisher performs administrative publishing tasks, whilst clients consume content through native platform mechanisms.

# Platform Trust Model

_Applies to: Patch My PC Publisher V2.x_

## Overview

A trust model defines how a management platform determines whether software is allowed to install on managed devices. It establishes the security boundary between published content and endpoint installation.

While the Publisher validates vendor binaries before publishing, validation alone does not grant permission to install software. Each management platform must independently trust the content before it can be deployed to client devices. This separation ensures customers retain full control over installation and enforcement decisions.

The sections below describe how trust is established and enforced in different environments. These include the WSUS trust model, the ConfigMgr trust model, and the Intune trust model. Each platform uses its own security mechanisms, such as certificates, role based access control, device management identity, and policy enforcement, to determine whether validated content is permitted to install.

## WSUS Trust Model

In WSUS environments, trust enforcement is anchored in the customer’s own code-signing certificate and Windows certificate trust configuration.

After the Publisher validates the vendor binary and confirms its hash matches the catalog metadata, the update is packaged and published to WSUS. WSUS then re-signs the update using the customer’s WSUS code-signing certificate before it is made available to clients.

For a client device to install a third-party update from WSUS, 2 trust conditions must be met.

First, the Group Policy setting **Allow signed updates from an intranet Microsoft update service location** must be enabled. This policy allows Windows to trust updates that are not signed directly by Microsoft but are signed by a locally trusted publisher.

Second, the WSUS code-signing certificate must be trusted on the client device. The certificate must be present in the **Trusted Publishers** store of the Local Computer certificate store. Without this trust, the update will be rejected during installation.

If the WSUS signing certificate is issued by a public or enterprise certification authority that is already trusted by the device, no additional configuration is required. However, if a self-signed certificate is used, that certificate must also be present in the **Trusted Root Certification Authorities** store on the Local Computer. Without placement in both the Trusted Publishers and Trusted Root stores, signature validation will fail and the update will not install.

This creates a layered trust chain:

* Vendor binary.
* Validated and hash-anchored by Patch My PC.
* Re-signed by the customer’s WSUS certificate.
* Trusted and installed by the client only if certificate validation succeeds.

Patch My PC does not control this final trust boundary. The customer’s certificate and endpoint trust configuration ultimately determine whether installation is permitted.

For more information on the certificate requirements for WSUS, see [Certificates](../publisher-requirements/wsus-requirements/certificates.md).

## ConfigMgr Trust Model

In both of the following scenarios, publishing actions are authenticated and authorized within the customer’s ConfigMgr security boundary. Client devices never communicate directly with the Publisher. They communicate only with ConfigMgr site systems such as management points and distribution points, which enforce policy, content validation, and deployment controls.

### Updates

For software updates, ConfigMgr relies on WSUS as its update source. Updates published by the Publisher are first published into WSUS and then synchronized into ConfigMgr through the Software Update Point. As a result, ConfigMgr update installations inherit the WSUS trust model, including customer-side code-signing enforcement.

When ConfigMgr is integrated with WSUS for third-party updates, it can manage certificate trust and policy configuration centrally. Through Software Update Point configuration and client settings, ConfigMgr can deploy and manage the WSUS code-signing certificate to client devices. This includes ensuring the certificate is placed in the appropriate certificate stores required for third-party update installation.

When the Publisher service is installed on the ConfigMgr site server, it runs under the Local System account. In this configuration, the service inherently has the necessary permissions to interact with ConfigMgr. No additional role configuration is typically required.

If the Publisher is installed on a remote Software Update Point, the computer account of that server (for example, SERVERNAME$) must be granted appropriate permissions within ConfigMgr. This is done through ConfigMgr security roles and administrative user configuration. The remote computer account is added as an administrative user and assigned a role that provides the required application creation and management permissions. For more information, see [Remote SUP Requirements](../publisher-requirements/configmgr-requirements/site-system-role/remote-sup-requirements.md).

ConfigMgr clients receive policy from the management point, which includes software update configuration, intranet update service location settings, and certificate trust requirements. When properly configured, ConfigMgr can automatically handle the enablement of the required Group Policy equivalent settings that allow signed updates from an intranet Microsoft update service location.

This central management capability reduces administrative overhead compared to standalone WSUS deployments, as certificate distribution and policy enforcement can be controlled directly through ConfigMgr infrastructure.

For more information on ConfigMgr certificate management options, see [Choosing a Certificate](../administration/general/certificate-management/choosing-a-certificate.md).

### Applications

For ConfigMgr applications, the trust model differs from software updates. Applications are created directly in ConfigMgr and distributed to distribution points within the customer’s infrastructure. Installation trust is enforced through ConfigMgr’s content distribution system, client policy evaluation, and internal infrastructure security controls.

The Publisher communicates with ConfigMgr using the ConfigMgr SDK and interacts with the SMS Provider, following standard management practice. All operations occur through supported APIs and respect ConfigMgr’s role-based access control model.&#x20;

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The Publisher does not interact directly with the ConfigMgr site database, except for read-only access when [scanning application inventory](../administration/configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md).</p>
</blockquote>

When the Publisher service is installed on the ConfigMgr site server, it runs under the Local System account. In this configuration, the service inherently has the necessary permissions to interact with ConfigMgr because the site server’s computer account is already trusted within the ConfigMgr security boundary. No additional role configuration is typically required.

If the Publisher is installed on a remote server, the computer account of that server, for example SERVERNAME$, must be granted appropriate permissions within ConfigMgr. This is accomplished through ConfigMgr security roles and administrative user configuration. The remote computer account is added as an administrative user and assigned a role that provides the required application creation and management permissions.

In all scenarios, publishing actions are authenticated and authorized through ConfigMgr’s native security framework. Client devices never communicate directly with the Publisher. They communicate only with ConfigMgr components such as management points and distribution points, which enforce policy, content validation, and deployment controls.

#### PowerShell Script Signing Option&#xD;

For environments enforcing an AllSigned PowerShell execution policy, the Publisher provides the option to [sign generated scripts using a customer-supplied code-signing certificate](../administration/configmgr-apps/options/application-creation-options.md#code-sign-the-powershell-detection-method-script-using-the-wsus-signing-certificate).

This allows organizations with strict PowerShell execution controls to maintain compliance with internal security standards while still leveraging automated application and update deployment.

Script signing ensures that:

* Only trusted and signed scripts execute on endpoints.
* Execution aligns with customer-defined execution policies.
* No unsigned automation is introduced into the environment.

## Intune Trust Model

### App Registration and Authentication Model

In Intune environments, trust enforcement is anchored in the customer’s Entra ID tenant and Microsoft Graph authorization model. All publishing operations performed by the Publisher occur through a tenant-controlled App Registration.

The Publisher authenticates to Microsoft Graph using an [App Registration](../publisher-requirements/intune-requirements/entra-id-app-registration/) created within the customer’s Entra ID tenant. This registration is granted only the permissions required to create, modify, and assign Win32 applications.

For authentication, [certificate-based credential flow is recommended](../publisher-requirements/intune-requirements/entra-id-app-registration/client-credentials.md). Using a certificate instead of a client secret provides stronger security through:

* Asymmetric key authentication.
* Reduced risk of credential leakage.

The private key associated with the certificate remains under customer control. Microsoft Graph validates the certificate during token acquisition before permitting publishing operations.

### Win32 Application Security within Intune

When publishing to Intune, the validated vendor binary is packaged as a Win32 application and uploaded through Microsoft Graph.

Once uploaded, the application becomes part of the Intune management ecosystem. Trust at the endpoint is established through multiple layers:

* The device must be enrolled and managed by Intune.
* The device maintains an active MDM certificate.
* The device must be in a compliant state if Conditional Access policies require it.
* The user or device must successfully authenticate with Entra ID.
* Policy and application assignments are encrypted and securely delivered to the device.

The Intune Management Extension retrieves encrypted policy from the Intune service using the device’s MDM identity and user authentication token. The extension then decrypts and evaluates policy locally before installation proceeds.

Applications are installed only if:

* Assignment targeting matches.
* Requirement rules evaluate as applicable.
* Detection logic confirms installation state.
* Device compliance conditions are satisfied.

This ensures that installation occurs only on authorized, managed, and policy-compliant devices.

#### PowerShell Script Signing Option

For environments enforcing an **AllSigned** PowerShell execution policy, the Publisher provides the option to [sign generated scripts using a customer-supplied code-signing certificate](../administration/intune-apps-updates/options/application-options.md#digitally-sign-the-detection-method-script-and-enforce-signature-checking-on-the-application-in-intu).

This allows organizations with strict PowerShell execution controls to maintain compliance with internal security standards while still leveraging automated application and update deployment.

Script signing ensures that:

* Only trusted and signed scripts execute on endpoints.
* Execution aligns with customer-defined execution policies.
* No unsigned automation is introduced into the environment.
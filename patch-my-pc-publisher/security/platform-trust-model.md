# Platform Trust Model in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

A _trust model_ defines how a management platform determines whether software may be installed on managed devices. It establishes the security boundary between published content and endpoint installation.

Whilst Patch My PC (PMPC) Publisher validates vendor binaries before publishing, validation alone does not grant permission to install software.&#x20;

Each management platform must independently trust the content before it can be deployed to client devices. This separation ensures customers retain full control over installation and enforcement decisions.

The sections below describe how trust is established and enforced in different environments. These include the Microsoft:

* [WSUS trust model](platform-trust-model.md#wsus-trust-model)
* [ConfigMgr trust model](platform-trust-model.md#configmgr-trust-model)
* [Intune trust model](platform-trust-model.md#intune-trust-model)

Each platform uses its own security mechanisms, such as certificates, role-based access control, device management identity, and policy enforcement, to determine whether validated content is permitted to install.

## WSUS Trust Model

In WSUS environments, trust enforcement is anchored in the customer’s own code-signing certificate and Windows certificate trust configuration.

After Publisher validates the vendor binary and confirms its hash matches the catalog metadata, the update is packaged and published to WSUS. WSUS then re-signs the update using the customer’s WSUS code-signing certificate before making it available to clients.

For a client device to install a third-party update from WSUS, two trust conditions must be met:

1. The Group Policy setting **Allow signed updates from an intranet Microsoft update service location** must be enabled. \
   \
   This policy allows Windows to trust updates that are not signed directly by Microsoft but are signed by a locally trusted publisher.
2. The WSUS code-signing certificate must be trusted on the client device. The certificate must be present in the **Trusted Publishers** store of the Local Computer certificate store. Without this trust, the update will be rejected during installation.

If the WSUS signing certificate is issued by a public or enterprise certification authority that is already trusted by the device, no additional configuration is required.&#x20;

However, if a self-signed certificate is used, that certificate must also be present in the **Trusted Root Certification Authorities** store on the Local Computer.&#x20;

Without placement in both the Trusted Publishers and Trusted Root stores, signature validation will fail, and the update will not install.

This creates a layered trust chain:

* Vendor binary
* Validated and hash-anchored by Patch My PC
* Re-signed by the customer’s WSUS certificate
* Trusted and installed by the client only if certificate validation succeeds.

PMPC does not control this final trust boundary. The customer’s certificate and endpoint trust configuration ultimately determine whether installation is permitted.

{% hint style="info" %}
**Note**

See [Certificate Requirements](../requirements/certificate-requirements.md) for more information on the certificate requirements for WSUS.
{% endhint %}

## ConfigMgr Trust Model

In both [Updates](platform-trust-model.md#configmgr-updates) and [Applications](platform-trust-model.md#configmgr-applications) scenarios, publishing actions are authenticated and authorized within the customer’s ConfigMgr security boundary.&#x20;

Client devices never communicate directly with Publisher. They communicate only with ConfigMgr Site Systems (such as Management Points (MPs) and Distribution Points (DPs)), which enforce policy, content validation, and deployment controls.

### ConfigMgr Updates

For software updates, ConfigMgr relies on WSUS as its update source. Updates published by Publisher are first published into WSUS and then synchronized to ConfigMgr through the Software Update Point (SUP). As a result, ConfigMgr update installations inherit the WSUS trust model, including customer-side code-signing enforcement.

When ConfigMgr is integrated with WSUS for third-party updates, it can centrally manage certificate trust and policy configuration. Through SUP configuration and client settings, ConfigMgr can deploy and manage the WSUS code-signing certificate to client devices. This includes ensuring the certificate is placed in the appropriate certificate stores required for third-party update installation.

When the Publisher service is installed on the ConfigMgr Site Server, it runs under the Local System account. In this configuration, the service inherently has the necessary permissions to interact with ConfigMgr. No additional role configuration is typically required.

If Publisher is installed on a remote SUP, the server's computer account (for example, **SERVERNAME$**) must be granted appropriate permissions within ConfigMgr.

This is done through ConfigMgr security roles and administrative user configuration. The remote computer account is added as an administrative user and assigned a role that grants the required permissions for application creation and management.

{% hint style="info" %}
**Note**

See [Remote SUP Requirements](../requirements/configmgr-requirements/sup-requirements/remote-sup.md) for more information.
{% endhint %}

ConfigMgr clients receive policy from the MP, which includes software update configuration, intranet update service location settings, and certificate trust requirements.&#x20;

When properly configured, ConfigMgr can automatically enable the required Group Policy-equivalent settings that allow signed updates from an intranet Microsoft Update service location.

This central management capability reduces administrative overhead compared to standalone WSUS deployments, as certificate distribution and policy enforcement can be controlled directly through the ConfigMgr infrastructure.

{% hint style="info" %}
**Note**

See [Choosing a Certificate](../manage/wsus-updates-tab/wsus-options/certificate-management/choosing.md) for more information on ConfigMgr certificate management options.
{% endhint %}

### ConfigMgr Applications

For ConfigMgr applications, the trust model differs from software updates. Applications are created directly in ConfigMgr and distributed to DPs within the customer’s infrastructure.&#x20;

Installation trust is enforced through ConfigMgr’s content distribution system, client policy evaluation, and internal infrastructure security controls.

Publisher communicates with ConfigMgr via the ConfigMgr SDK and interacts with the SMS Provider, following standard management practices. All operations are performed through supported APIs and adhere to ConfigMgr’s role-based access control model.&#x20;

{% hint style="info" %}
**Note**

Publisher does not interact directly with the ConfigMgr site database, except for read-only access when [scanning application inventory](../manage/configmgr-apps-tab/scan-configmgr.md).
{% endhint %}

When the Publisher service is installed on the ConfigMgr Site Server, it runs under the Local System account. In this configuration, the service inherently has the necessary permissions to interact with ConfigMgr as the Site Server’s computer account is already trusted within the ConfigMgr security boundary. No additional role configuration is typically required.

If Publisher is installed on a remote server, the server's computer account (for example, **SERVERNAME$**) must be granted the appropriate permissions within ConfigMgr.&#x20;

This is accomplished through ConfigMgr security roles and the configuration of administrative users. The remote computer account is added as an administrative user and assigned a role that grants the required permissions for application creation and management.

In all scenarios, publishing actions are authenticated and authorized through ConfigMgr’s native security framework.&#x20;

Client devices never communicate directly with Publisher. They communicate only with ConfigMgr components such as MPs and DPs, which enforce policy, content validation, and deployment controls.

#### PowerShell Script Signing Option&#xD;

For environments enforcing an **AllSigned** PowerShell execution policy, Publisher provides the option to [sign generated scripts using a customer-supplied code-signing certificate](../manage/configmgr-apps-tab/base-install-options/application-creation-options.md#code-sign-the-powershell-detection-method-script-using-the-wsus-signing-certificate).

This allows organizations with strict PowerShell execution controls to maintain compliance with internal security standards whilst still leveraging automated application and update deployment.

Script signing ensures that:

* Only trusted and signed scripts execute on endpoints.
* Execution aligns with customer-defined execution policies.
* No unsigned automation is introduced into the environment.

## Intune Trust Model

### App Registration and Authentication Model

In Intune environments, trust enforcement is anchored in the customer’s Entra ID tenant and Microsoft Graph authorization model. All publishing operations performed by Publisher occur through a tenant-controlled App Registration.

Publisher authenticates to Microsoft Graph using an [App Registration](../requirements/intune-requirements/entra-id-app-registration/) created within the customer’s Entra ID tenant. This registration is granted only the permissions required to create, modify, and assign Win32 applications.

For authentication, [certificate-based credential flow is recommended](../requirements/intune-requirements/entra-id-app-registration/client-credentials.md). Using a certificate instead of a client secret provides stronger security through:

* Asymmetric key authentication.
* Reduced risk of credential leakage.

The private key associated with the certificate remains under the customer's control. Microsoft Graph validates the certificate during token acquisition before permitting publishing operations.

### Win32 Application Security within Intune

When publishing to Intune, the validated vendor binary is packaged as a Win32 application and uploaded through Microsoft Graph.

Once uploaded, the application becomes part of the Intune management ecosystem. Trust at the endpoint is established through multiple layers:

* The device must be enrolled and managed by Intune.
* The device maintains an active MDM certificate.
* The device must be in a compliant state if Conditional Access policies require it.
* The user or device must successfully authenticate with Entra ID.
* Policy and application assignments are encrypted and securely delivered to the device.

The Intune Management Extension retrieves an encrypted policy from the Intune service using the device’s MDM identity and the user's authentication token. The extension then decrypts and evaluates policy locally before installation proceeds.

Applications are installed only if:

* Assignment targeting matches.
* Requirement rules evaluate as applicable.
* Detection logic confirms installation state.
* Device compliance conditions are satisfied.

This ensures that installation occurs only on authorized, managed, and policy-compliant devices.

#### PowerShell Script Signing Option

For environments enforcing an **AllSigned** PowerShell execution policy, Publisher provides the option to [sign generated scripts using a customer-supplied code-signing certificate](../manage/configmgr-apps-tab/base-install-options/application-creation-options.md#code-sign-the-powershell-detection-method-script-using-the-wsus-signing-certificate).

This allows organizations with strict PowerShell execution controls to maintain compliance with internal security standards while still leveraging automated application and update deployment.

Script signing ensures that:

* Only trusted and signed scripts execute on endpoints.
* Execution aligns with customer-defined execution policies.
* No unsigned automation is introduced into the environment.

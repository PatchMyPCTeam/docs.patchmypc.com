# ConfigMgr Client Setting Requirements for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

For Microsoft ConfigMgr client devices to successfully scan for, trust, and install updates, specific Client Settings need to be configured. ConfigMgr's Software Update Client Settings configure core Windows Update Agent behavior on managed devices.

This client setting is typically already enabled if you manage Microsoft Updates through an existing Software Update Point (SUP). It handles setting the intranet update service location and related scan settings based on the SUP assigned through boundary group configuration. As a result, clients automatically know which SUP to scan against and where to obtain update metadata and content.

When third-party software updates are also enabled through Client Settings, ConfigMgr handles the additional requirements for third-party updates, such as allowing non-Microsoft–signed updates and distributing the WSUS code-signing certificate to clients, without requiring manual registry changes or manual certificate deployment.

> \*\*Important\*\*
>
> If you plan to deploy third-party update content through a Cloud Management Gateway (CMG), do \*\*NOT\*\* enable \*\*Allow clients to download delta content when available\*\* in the corresponding Client Settings for clients that connect to a CMG as their Management Point (MP) and SUP.
>
> When a CMG is used for content storage, third-party update content will fail to download to clients if the Download delta content when available client setting is enabled.
>
> For more information, see the [Allow clients to download delta content when available](https://learn.microsoft.com/en-us/intune/configmgr/core/clients/deploy/about-client-settings#allow-clients-to-download-delta-content-when-available) section of [About client settings in Configuration Manager](https://learn.microsoft.com/intune/configmgr/core/clients/deploy/about-client-settings).

![Software Update Client Settings](../../../.gitbook/assets/image-\(382\).png)

## **Enable Third-Party Software Updates**

To enable third-party software updates:

1. In the ConfigMgr console, navigate to **Administration | Client Settings**
2. Open **Default Client Settings** or a custom client settings policy.
3. Select **Software Updates**
4. Ensure the following settings are configured:
   * **Enable software updates on clients** = **Yes**
   * **Enable third party software updates** = **Yes**

> \*\*Note\*\*
>
> This Client Setting must apply to \*\*all devices\*\* that will scan for or install third-party updates.

When **Enable third party software updates** is set to **Yes**, ConfigMgr configures the client to:

* Allow the Windows Update Agent to download and install non-Microsoft–signed update&#x73;**.**
* Attempt to retrieve the **code-signing certificate** from ConfigMgr during a software update scan.
* Trust updates signed with that third-party certificate by placing the certificate(s) into the appropriate certificate stores.

Without this Client Setting enabled, client devices will not trust third-party updates, even if they are correctly published and deployed. This client setting configures local policy on the device, including setting the following registry value:

`HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate`\
`AcceptTrustedPublisherCerts = 1`

![Accept Trusted Publisher Certificates](../../../.gitbook/assets/image-\(383\).png)

If you are not using ConfigMgr Client Settings to manage this behavior, the same configuration can be applied using:

* Group Policy
* Manual registry configuration
* Intune Settings Catalog

# Intune Network Requirements for  Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

In addition to the [core network requirements](../core-requirements.md#network), Patch My PC (PMPC) Publisher requires outbound connectivity to Microsoft Entra ID and Microsoft Graph to authenticate and manage applications in Microsoft Intune. These endpoints are used for OAuth 2.0 client-credential authentication, token acquisition, and creating, updating, and assigning Win32 applications.

{% hint style="info" %}
**Note**

These URLs can be updated in Publisher from the **Options** button in either the **Intune Apps** or **Intune Updates** tabs. See [Microsoft Graph API Settings](entra-id-app-registration/) for more details.
{% endhint %}

The exact endpoints depend on the cloud environment your Intune tenant is hosted in, as outlined in the scenarios below.

## Intune Reports

Publisher retrieves Intune report exports by using the Microsoft Graph reports export API at **deviceManagement/reports/exportJobs**. When an export job completes, Microsoft Graph returns a temporary download URL hosted in Azure Blob Storage.&#x20;

Use the Azure Storage endpoint for the cloud environment in which your Intune tenant is hosted. The required endpoints are listed in the following table.

## **Scenario 1: Public/Commercial Cloud**

This is the default and most common configuration and applies to the majority of Patch My PC customers using standard Microsoft 365 and Intune tenants. Use this configuration unless your tenant is explicitly hosted in a government or sovereign cloud.

<table><thead><tr><th valign="top">Setting</th><th valign="top">Value</th></tr></thead><tbody><tr><td valign="top">Authority</td><td valign="top"><code>https://login.microsoftonline.com</code></td></tr><tr><td valign="top">Authentication URL</td><td valign="top"><code>https://graph.microsoft.com</code></td></tr><tr><td valign="top">Graph Base URL</td><td valign="top"><code>https://graph.microsoft.com/beta</code></td></tr><tr><td valign="top">Intune Reports Storage URL</td><td valign="top"><code>*.blob.core.windows.net</code></td></tr></tbody></table>

The table above lists the primary authentication and Microsoft Graph endpoints required by Publisher. In addition, Microsoft Intune and Azure rely on a broader set of Azure service endpoints.&#x20;

{% hint style="info" %}
**Note**

See [Allow the Azure portal URLs on your firewall or proxy server](https://learn.microsoft.com/azure/azure-portal/azure-portal-safelist-urls?tabs=public-cloud) for the authoritative list of Azure portal URLs, domains, and service dependencies.

These endpoints are required for authentication flows, token issuance, and service interactions used by Intune.
{% endhint %}

## **Scenario 2: GCC High (US Government)**

Use this configuration if your organization operates in the GCC High (U.S. Government) cloud. These tenants use separate authentication and Microsoft Graph endpoints that differ from the commercial cloud and must be configured explicitly.

{% hint style="info" %}
**Note**

If your tenant is not explicitly documented as GCC High or 21Vianet, you should use the Public/Commercial Cloud endpoints. GCC and other non-sovereign government tenants (such as GCC non-High) continue to use the commercial cloud endpoints.
{% endhint %}

<table><thead><tr><th valign="top">Setting</th><th valign="top">Value</th></tr></thead><tbody><tr><td valign="top">Authority</td><td valign="top"><code>https://login.microsoftonline.us</code></td></tr><tr><td valign="top">Authentication URL</td><td valign="top"><code>https://graph.microsoft.us</code></td></tr><tr><td valign="top">Graph Base URL</td><td valign="top"><code>https://graph.microsoft.us/beta</code></td></tr><tr><td valign="top">Intune Reports Storage URL</td><td valign="top"><code>*.blob.core.usgovcloudapi.net</code></td></tr></tbody></table>

The table above lists the primary authentication and Microsoft Graph endpoints required by Publisher. In addition, Microsoft Intune and Azure rely on a broader set of Azure service endpoints.&#x20;

{% hint style="info" %}
**Note**

See [Allow the Azure portal URLs on your firewall or proxy server](https://learn.microsoft.com/azure/azure-portal/azure-portal-safelist-urls?tabs=us-government-cloud) for the full, authoritative list of Azure portal URLs, domains, and service dependencies, refer to Microsoft’s documentation.

These endpoints are required for authentication flows, token issuance, and service interactions used by Intune.
{% endhint %}

## **Scenario 3: 21Vianet (China)**

Use this configuration only if your Intune tenant is hosted in Microsoft 21Vianet (China). This sovereign cloud operates independently from the commercial and government clouds and requires region-specific endpoints.

<table><thead><tr><th valign="top">Setting</th><th valign="top">Value</th></tr></thead><tbody><tr><td valign="top">Authority</td><td valign="top"><code>https://login.chinacloudapi.cn</code></td></tr><tr><td valign="top">Authentication URL</td><td valign="top"><code>https://microsoftgraph.chinacloudapi.cn</code></td></tr><tr><td valign="top">Graph Base URL</td><td valign="top"><code>https://microsoftgraph.chinacloudapi.cn/beta</code></td></tr><tr><td valign="top">Intune Reports Storage URL</td><td valign="top"><code>*.blob.core.chinacloudapi.cn</code></td></tr></tbody></table>

The table above lists the primary authentication and Microsoft Graph endpoints required by Publisher. In addition, Microsoft Intune and Azure rely on a broader set of Azure service endpoints.&#x20;

{% hint style="info" %}
**Note**

See [Allow the Azure portal URLs on your firewall or proxy server](https://learn.microsoft.com/azure/azure-portal/azure-portal-safelist-urls?tabs=azure-china-cloud) for the full, authoritative list of Azure portal URLs, domains, and service dependencies, refer to Microsoft’s documentation.

These endpoints are required for authentication flows, token issuance, and service interactions used by Intune.
{% endhint %}

# Network

_Applies to: Patch My PC Publisher V2.x_

## Overview

As well as the [core network requirements](../core-requirements.md#network), the Publisher requires outbound connectivity to Microsoft Entra ID and Microsoft Graph to authenticate and manage applications in Intune. These endpoints are used for OAuth 2.0 client credential authentication, token acquisition, and for creating, updating, and assigning Win32 applications.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>These URLs can be updated in the Publisher from the Options button in either the Intune Apps or Intune Updates tabs. See [Microsoft Graph API Settings](entra-id-app-registration/) for more details.</p>
</blockquote>

The exact endpoints depend on the cloud environment your Intune tenant is hosted in, as outlined in the different scenarios below.

## Intune Reports

The Publisher retrieves Intune report exports by using the Microsoft Graph reports export API at `deviceManagement/reports/exportJobs`. When an export job completes, Microsoft Graph returns a temporary download URL hosted in Azure Blob Storage.&#x20;

Use the Azure Storage endpoint for the cloud environment your Intune tenant is hosted in. The required endpoints are listed in the table below.

## **Scenario 1: Public / Commercial Cloud**

This is the default and most common configuration and applies to the majority of Patch My PC customers using standard Microsoft 365 and Intune tenants. Use this configuration unless your tenant is explicitly hosted in a government or sovereign cloud.

| Setting                        | Value                               |
| ------------------------------ | ----------------------------------- |
| **Authority**                  | `https://login.microsoftonline.com` |
| **Authentication URL**         | `https://graph.microsoft.com`       |
| **Graph Base URL**             | `https://graph.microsoft.com/beta`  |
| **Intune Reports Storage URL** | `*.blob.core.windows.net`           |

The table above lists the primary authentication and Microsoft Graph endpoints required by the Publisher. In addition to these, Microsoft Intune and Azure rely on a broader set of Azure service endpoints. For the full, authoritative list of Azure portal URLs, domains, and service dependencies, refer to Microsoft’s documentation:

* [https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-safelist-urls?tabs=public-cloud](https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-safelist-urls?tabs=public-cloud)

These endpoints are required for authentication flows, token issuance, and service interactions used by Intune.

## **Scenario 2: GCC High (US Government)**

Use this configuration if your organization operates in the GCC High (U.S. Government) cloud. These tenants use separate authentication and Microsoft Graph endpoints that differ from the commercial cloud and must be configured explicitly.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If your tenant is not explicitly documented as GCC High or 21Vianet, you should use the Public / Commercial Cloud endpoints. GCC and other non-sovereign government tenants (such as GCC non-High) continue to use the commercial cloud endpoints.</p>
</blockquote>

| Setting                        | Value                              |
| ------------------------------ | ---------------------------------- |
| **Authority**                  | `https://login.microsoftonline.us` |
| **Authentication URL**         | `https://graph.microsoft.us`       |
| **Graph Base URL**             | `https://graph.microsoft.us/beta`  |
| **Intune Reports Storage URL** | `*.blob.core.usgovcloudapi.net`    |

The table above lists the primary authentication and Microsoft Graph endpoints required by the Publisher. In addition to these, Microsoft Intune and Azure rely on a broader set of Azure service endpoints. For the full, authoritative list of Azure portal URLs, domains, and service dependencies, refer to Microsoft’s documentation:

* [https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-safelist-urls?tabs=us-government-cloud](https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-safelist-urls?tabs=us-government-cloud)

These endpoints are required for authentication flows, token issuance, and service interactions used by Intune.

## **Scenario 3: 21Vianet (China)**

Use this configuratio only if your Intune tenant is hosted in Microsoft 21Vianet (China). This sovereign cloud operates independently from the commercial and government clouds and requires region-specific endpoints.

| Setting                        | Value                                          |
| ------------------------------ | ---------------------------------------------- |
| **Authority**                  | `https://login.chinacloudapi.cn`               |
| **Authentication URL**         | `https://microsoftgraph.chinacloudapi.cn`      |
| **Graph Base URL**             | `https://microsoftgraph.chinacloudapi.cn/beta` |
| **Intune Reports Storage URL** | `*.blob.core.chinacloudapi.cn`                 |

The table above lists the primary authentication and Microsoft Graph endpoints required by the Publisher. In addition to these, Microsoft Intune and Azure rely on a broader set of Azure service endpoints. For the full, authoritative list of Azure portal URLs, domains, and service dependencies, refer to Microsoft’s documentation:

* [https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-safelist-urls?tabs=azure-china-cloud](https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-safelist-urls?tabs=azure-china-cloud)

These endpoints are required for authentication flows, token issuance, and service interactions used by Intune.
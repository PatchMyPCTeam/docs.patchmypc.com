# Authentication Settings

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Authentication Settings** section defines how the Publisher authenticates with Entra ID and communicates to Microsoft Intune using a Microsoft Entra ID application registration. These settings are required before the Publisher can create, update, or manage Win32 applications and updates in Intune.

This section establishes the trust relationship between the Publisher and your Intune tenant by configuring the tenant authority, application identifier, and authentication method. Authentication can be performed by using either a client secret or a certificate, depending on your organization security requirements.

<figure><img src="../../../../.gitbook/assets/image (248).png" alt="Authentication Settings" width="563"><figcaption></figcaption></figure>

## Tenant Friendly name

The friendly name is a descriptive label for the app registration configuration. This value is shown only in the Publisher and is used to help identify the tenant connection when reviewing settings.

## Authority

The **Authority** URL is constructed by using the Microsoft sign in endpoint and your tenant name. The supported endpoint is:

[`https://login.microsoftonline.com`](https://login.microsoftonline.com)

To complete the authority value, append your tenant name to the URL. The tenant name can be found in the [**Tenant status**](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/TenantAdminMenu/~/tenantStatus) page in the Intune admin center.

<figure><img src="../../../../.gitbook/assets/image (244).png" alt="Find the Tenant Name in the Intune admin center" width="563"><figcaption></figcaption></figure>

The completed authority value should follow this format:

`https://login.microsoftonline.com/tenantname.onmicrosoft.com`

<figure><img src="../../../../.gitbook/assets/image (245).png" alt="Full Authority URL" width="498"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The tenant name used in the authority value does not have to be the onmicrosoft.com domain. Any verified domain name associated with the tenant can be used, as all verified domains resolve to the same authentication endpoint and identify the same tenant.
{% endhint %}

## Authentication URL

Defines the Microsoft Graph endpoint used for authentication and token acquisition. The default URL is `https://graph.microsoft.com`.

{% hint style="info" %}
**Note**

These values may need to be changed only when your Intune tenant is hosted in a government or sovereign cloud, such as GCC High or Microsoft 21Vianet (China), which use different authentication and Microsoft Graph endpoints than the public commercial cloud.

\
If your tenant is hosted in the standard commercial Microsoft 365 cloud, you should continue using the default values. For details on the specific endpoints required for each cloud environment, refer to the [Intune speciifc Network requirements](../../../publisher-requirements/intune-requirements/network.md).
{% endhint %}

## Graph Base URL

Defines the Microsoft Graph endpoint used for Intune and application management operations. The default Graph base URL is `https://graph.microsoft.com/beta`.

## Restore

The **Restore** button resets the Authentication URL or the Graph base URL to the recommended default values.

## Application (Client) ID

The **Application ID** field must contain the Application client ID from your Entra ID app registration.

To obtain this value, select **App registrations** in the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade/quickStartType~/null/sourceType/Microsoft_AAD_IAM), and copy the **Application (client) ID** value.

<figure><img src="../../../../.gitbook/assets/image (3778).png" alt="Application (Client) ID" width="563"><figcaption></figcaption></figure>

For more details on how to create an Entra ID App Registration for use with the Publisher, see: [Entra ID App Registration](../../../publisher-requirements/intune-requirements/entra-id-app-registration/).

## Application Certificate or Application Secret

The authentication method is determined by the [credentials configured on the app registration](../../../publisher-requirements/intune-requirements/entra-id-app-registration/client-credentials.md).

If [certificate based authentication](../../../publisher-requirements/intune-requirements/entra-id-app-registration/client-credentials.md#use-a-certificate-for-authentication) is used, select the **Certificate** option and browse the Local Machine certificate Personal store to select the appropriate certificate.

If [client secret authentication](../../../publisher-requirements/intune-requirements/entra-id-app-registration/client-credentials.md#use-a-client-secret-for-authentication) is used, select the **Application Secret** option and enter the client secret value that was generated during app registration setup.

For more information, and to help decide which client credential method to use if you have not already chosen one, see: [Client Credentials](../../../publisher-requirements/intune-requirements/entra-id-app-registration/client-credentials.md).

Whichever client credential method is used, the Intune Options form displays the credential expiration date below the credential field.

<figure><img src="../../../../.gitbook/assets/image (249).png" alt="Credential expiration date" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

Certificate-based authentication is the recommended client credential to use for an app registration.
{% endhint %}

## Test Connection

Press the **Test Connection** button to validate authentication, connectivity, and the required API permissions.

The test confirms that the Publisher can successfully connect to the Intune tenant via Microsoft Graph and that all required Microsoft Graph permissions are available. When the test completes successfully and all permissions show as enabled, the Publisher is ready to publish applications and updates to Intune.

<figure><img src="../../../../.gitbook/assets/image (250).png" alt="App Registration Connection Status" width="563"><figcaption></figcaption></figure>

For more information about the API permissions required for the Publisher, see: [API Permissions](../../../publisher-requirements/intune-requirements/entra-id-app-registration/api-permissions.md).

{% hint style="warning" %}
**Important**

If the test fails, review the authority value, application (client) ID, and client credntial method used before proceeding.
{% endhint %}


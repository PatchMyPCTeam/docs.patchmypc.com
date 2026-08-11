# Intune Apps Requirements

_Applies to: Intune Apps for Cloud_

To use Intune Apps for Cloud (Intune Apps), you need:

* An Internet connection that can access Microsoft Azure services and the Patch My PC (PMPC) Cloud Platform ([https://portal.patchmypc.com/](https://portal.patchmypc.com/)).
* An Intune tenant.

{% hint style="info" %}
Note

We currently do not support [GCC High tenants](https://learn.microsoft.com/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc) for Intune Apps. You can help us prioritize this [feature](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-4260).&#x20;
{% endhint %}

* An Enterprise Plus or Enterprise Premium Patch My PC subscription.

{% hint style="warning" %}
**Important**

We no longer allow customers whose Entra ID domain starts with "m365x" to start a Patch My PC (PMPC) Cloud trial. Such customers no longer see the option to start PMPC Cloud Trial and will either need to enter a PMPC Cloud license key or activate their license using their on-premises Publisher license key.

Managed Service Providers (MSPs) cannot activate the Cloud Portal using a standard MSP subscription, as an MSP Plus subscription is required.

See [Features by plan](https://patchmypc.com/product/msp#pricing) for more information on our different subscription levels.&#x20;
{% endhint %}

* A minimum of two users, who will be granted [**Access Management**](https://docs.patchmypc.com/patch-my-pc-cloud/administration/managing-users/modify-a-user#managing-access-management-privileges-for-a-user) privileges within PMPC Cloud.
* An account with the **Global Administrator** role in Entra ID to approve our enterprise app. See [Permissions required for the Intune Apps](https://docs.patchmypc.com/installation-guides/patch-my-pc-cloud/administration/manage-users/permissions-reference/permissions-required-for-intune-apps) for more details.

{% hint style="info" %}
**Note**

See [Features by plan](https://patchmypc.com/request-quote#feature-comparison) for more information on our different subscription levels.

You also do not need a copy of our OnPrem Publisher if you only plan to deploy Intune Apps to Intune clients.
{% endhint %}

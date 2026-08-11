# Prerequisites for Patch My PC Cloud

_Applies to: Patch My PC Cloud_

To use Patch My PC (PMPC) Cloud, you need:

* An Internet connection that can access Microsoft Azure services and the Patch My PC (PMPC) Cloud Platform ([https://portal.patchmypc.com/](https://portal.patchmypc.com/)).
* A Microsoft Entra ID tenant

{% hint style="info" %}
Note

We currently do not support [GCC High tenants](https://learn.microsoft.com/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc) for Patch My PC Cloud. You can help us prioritize this [feature](https://ideas.patchmypc.com/ideas/PATCHMYPC-I-4260).&#x20;

Patch My PC Cloud supports authentication through Microsoft Entra ID only. Direct SSO with third-party identity providers such as Okta or PingFederate is not currently supported.

Patch My PC Cloud does not expose SAML or OIDC endpoints for customer-managed third-party IdP integrations. As a result, third-party IdPs cannot federate directly with Patch My PC Cloud, and Patch My PC Cloud cannot directly consume or validate assertions, tokens, or MFA claims issued by those providers.
{% endhint %}

* An Enterprise Plus, Enterprise Premium, or Managed Service Provider (MSP) Plus subscription.

{% hint style="info" %}
**Note**

With an MSP Plus subscription, you can manage any number of devices. However, there is a minimum monthly charge based on 50 devices per tenant.
{% endhint %}

{% hint style="warning" %}
**Important**

We no longer allow customers whose Entra ID domain starts with "m365x" to start a Patch My PC (PMPC) Cloud trial. Such customers no longer see the option to start PMPC Cloud Trial and will either need to enter a PMPC Cloud license key or activate their license using their on-premises Publisher license key.

See [Features by plan](https://patchmypc.com/request-quote#feature-comparison) for more information on our different subscription levels.&#x20;
{% endhint %}

* A minimum of two users, who will be granted [**Access Management**](https://docs.patchmypc.com/patch-my-pc-cloud/administration/managing-users/modify-a-user#managing-access-management-privileges-for-a-user) privileges within PMPC Cloud.

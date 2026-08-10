# Intune Apps Requirements

_Applies to: Intune Apps for Cloud_

To use Intune Apps for Cloud (Intune Apps), you need:

* An Internet connection that can access Microsoft Azure services and the Patch My PC (PMPC) Cloud Platform ([https://portal.patchmypc.com/](https://portal.patchmypc.com/)).
* An Intune tenant.

<blockquote class="wp-block-quote">
<p>Note</p>
<p>We currently do not support <a href="https://learn.microsoft.com/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc">GCC High tenants</a> for Intune Apps. You can help us prioritize this <a href="https://ideas.patchmypc.com/ideas/PATCHMYPC-I-4260">feature</a>.&#x20;</p>
</blockquote>

* An Enterprise Plus or Enterprise Premium Patch My PC subscription.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>We no longer allow customers whose Entra ID domain starts with "m365x" to start a Patch My PC (PMPC) Cloud trial. Such customers no longer see the option to start PMPC Cloud Trial and will either need to enter a PMPC Cloud license key or activate their license using their on-premises Publisher license key.</p>
<p>Managed Service Providers (MSPs) cannot activate the Cloud Portal using a standard MSP subscription, as an MSP Plus subscription is required.</p>
<p>See <a href="https://patchmypc.com/product/msp#pricing">Features by plan</a> for more information on our different subscription levels.&#x20;</p>
</blockquote>

* A minimum of two users, who will be granted [**Access Management**](https://docs.patchmypc.com/patch-my-pc-cloud/administration/managing-users/modify-a-user#managing-access-management-privileges-for-a-user) privileges within PMPC Cloud.
* An account with the **Global Administrator** role in Entra ID to approve our enterprise app. See [Permissions required for the Intune Apps](https://docs.patchmypc.com/installation-guides/patch-my-pc-cloud/administration/manage-users/permissions-reference/permissions-required-for-intune-apps) for more details.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See <a href="https://patchmypc.com/request-quote#feature-comparison">Features by plan</a> for more information on our different subscription levels.</p>
<p>You also do not need a copy of our OnPrem Publisher if you only plan to deploy Intune Apps to Intune clients.</p>
</blockquote>
# Multiple Domain Support in Patch My PC Cloud

_Applies to: Patch My PC (PMPC) Cloud_

The _Multiple domains_ feature of Patch My PC (PMPC) Cloud allows you to configure multiple Entra ID custom domains for your PMPC Cloud company. This then allows any users within the configured custom domains to request access to your PMPC Cloud company. It also allows users within those domains to be invited to join your PMPC Cloud company.

To configure your PMPC Cloud Company for multiple domains:

1\. Add the relevant custom domain to your tenant.

{% hint style="info" %}
**Note**

See [Add your custom domain name to your tenant](https://learn.microsoft.com/en-us/entra/fundamentals/add-custom-domain) for more information.

Also, you cannot add a domain to Entra ID using the portal.
{% endhint %}

2. Ensure your PMPC Cloud company is [connected to Intune](/broken/pages/RoXhXa1jcXhIcPcKJk05#connecting-to-an-intune-tenant).
3. Sign in to your PMPC Cloud company using a user account that has the **Full Admin with Access Management** role (other roles cannot use this feature).
4. Navigate to **Settings | Company**

<figure><img src="../../../../../.gitbook/assets/image (559).png" alt="Navigating to ‘Settings | Company’" width="563"><figcaption></figcaption></figure>

5. Click the **Domains** tab.

<figure><img src="../../../../../.gitbook/assets/image (560).png" alt="Clicking the ‘Domains’ tab" width="563"><figcaption></figcaption></figure>

The list of custom domains configured for your tenant is displayed. If a domain is listed with a **Status** of **Available**, it means any users within that domain can request access to your PMPC Cloud Company.

{% hint style="info" %}
**Note**

Whenever a new custom domain is added, it will be automatically enabled within PMPC Cloud.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (569).png" alt="List of configured domains" width="563"><figcaption></figcaption></figure>

6. Complete the relevant task:
   1. [Enable a domain](enable-domain.md)
   2. [Disable a domain](disable-domain.md)

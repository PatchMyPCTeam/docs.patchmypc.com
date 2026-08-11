# Multiple Domain Support in Patch My PC Cloud

_Applies to: Patch My PC (PMPC) Cloud_

The _Multiple domains_ feature of Patch My PC (PMPC) Cloud allows you to configure multiple Entra ID custom domains for your PMPC Cloud company. This then allows any users within the configured custom domains to request access to your PMPC Cloud company. It also allows users within those domains to be invited to join your PMPC Cloud company.

To configure your PMPC Cloud Company for multiple domains:

1\. Add the relevant custom domain to your tenant.

> \*\*Note\*\*
>
> See [Add your custom domain name to your tenant](https://learn.microsoft.com/en-us/entra/fundamentals/add-custom-domain) for more information.
>
> Also, you cannot add a domain to Entra ID using the portal.

2. Ensure your PMPC Cloud company is [connected to Intune](/broken/pages/RoXhXa1jcXhIcPcKJk05#connecting-to-an-intune-tenant).
3. Sign in to your PMPC Cloud company using a user account that has the **Full Admin with Access Management** role (other roles cannot use this feature).
4. Navigate to **Settings | Company**

![Navigating to ‘Settings | Company'](/_images/image-(567 "Navigating to ‘Settings | Company'") (1).png>)

5. Click the **Domains** tab.

![Clicking the ‘Domains' tab](/_images/image-(568 "Clicking the ‘Domains' tab") (1).png>)

The list of custom domains configured for your tenant is displayed. If a domain is listed with a **Status** of **Available**, it means any users within that domain can request access to your PMPC Cloud Company.

> \*\*Note\*\*
>
> Whenever a new custom domain is added, it will be automatically enabled within PMPC Cloud.

![List of configured domains](/_images/image-(569 "List of configured domains") (1).png>)

6. Complete the relevant task:
   1. [Enable a domain](enable-domain.md)
   2. [Disable a domain](disable-domain.md)
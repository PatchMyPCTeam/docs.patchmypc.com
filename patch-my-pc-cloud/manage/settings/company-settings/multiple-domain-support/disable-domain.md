# Disable a Domain in Patch My PC Cloud

_Applies to: Patch My PC (PMPC) Cloud_

To disable an Entra ID Custom Domain for your Patch My PC (PMPC) Cloud company:

{% hint style="info" %}
**Note**

If a Custom domain is deleted from your tenant, it will show with a **Status** of **Deleted** on the **Domains** tab and the checkbox beside it will automatically be unchecked.
{% endhint %}

1. Sign in to your PMPC Cloud company using a user account that has the **Full Admin with Access Management** role.
2. Navigate to **Settings | Company**

<figure><img src="../../../../../.gitbook/assets/image (563).png" alt="Navigating to ‘Settings | Company’" width="563"><figcaption></figcaption></figure>

3. Click the **Domains** tab.

<figure><img src="../../../../../.gitbook/assets/image (564).png" alt="Clicking the ‘Domains’ tab" width="563"><figcaption></figcaption></figure>

4. Uncheck the checkbox beside the relevant domain(s) you want to disable and click **Save**

<figure><img src="../../../../../.gitbook/assets/image (565).png" alt="Unchecking the checkbox beside the relevant domain you want to disable and clicking ‘Save’" width="563"><figcaption></figcaption></figure>

The **Success – Domains updated** notification is shown.

<figure><img src="../../../../../.gitbook/assets/image (566).png" alt="‘Success – Domains updated’ notification" width="250"><figcaption></figcaption></figure>

Once the domain has been disabled, your PMPC Cloud Company will no longer appear on the **Sign In** page for any users in that domain.

{% hint style="info" %}
**Note**

You cannot delete a domain. You can only disable it, and at least one domain must be enabled.

Also, disabling a domain only prevents any new users from that domain from requesting access to your company. It does not revoke access for any existing users in your PMPC Cloud company from the removed domain. If you decide to remove a domain, you should also review the list of users and groups with access to your PMPC company to ensure only the relevant users have access to your PMPC Cloud Company.
{% endhint %}

# Overview

_Applies to: Patch My PC Publisher V2.x_

Patch My PC supports managing multiple Intune tenants from a single instance of the Publisher. This capability is designed for managed service providers who require centralized control while maintaining tenant-level separation.

<figure><img src="../../../../.gitbook/assets/image (4107).png" alt="Multi-tenancy in the Publisher" width="545"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The multi-tenant form controls shown in the image above are visible only when the Publisher is licensed with an MSP or MSP Plus license.
{% endhint %}

{% hint style="warning" %}
**Important**

For managed service providers, Patch My PC Cloud is the recommended solution. It reduces infrastructure requirements and removes the need to maintain a Publisher installation.

See [Managed Service Provider Overview](../../../../patch-my-pc-cloud/managed-service-provider-feature/managed-service-provider-overview.md) for more information.
{% endhint %}

{% hint style="success" %}
**Tip**

The Publisher still remains useful in scenarios where customers operate in sovereign or government cloud environments. In these cases, the Publisher allows you to modify Microsoft Graph endpoints to ensure publishing targets the appropriate cloud environment.
{% endhint %}

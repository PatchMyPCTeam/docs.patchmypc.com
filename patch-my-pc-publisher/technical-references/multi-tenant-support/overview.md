# Overview of Multitenant Support in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*IMPORTANT\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

Multiple Intune tenants can be supported from a single instance of the Patch My PC (PMPC) Publisher. This capability is designed for managed service providers who require centralized control while maintaining tenant-level separation.

> \*\*Important\*\*
>
> The multi-tenant form controls are only visible if Publisher is licensed with an MSP or MSP Plus license.

![Multi-tenancy in the Publisher](/_images/image-(4107).png)

> \*\*Important\*\*
>
> For managed service providers, Patch My PC Cloud is the recommended solution. It reduces infrastructure requirements and removes the need to maintain a Publisher installation.
>
> See \[Managed Service Provider Overview]\(../../../patch-my-pc-cloud/managed-service-provider-feature/managed-service-provider-overview.md) for more information.

> \*\*Tip\*\*
>
> Publisher still remains useful in scenarios where customers operate in sovereign or government cloud environments. In these cases, the Publisher allows you to modify Microsoft Graph endpoints to ensure publishing targets the appropriate cloud environment.
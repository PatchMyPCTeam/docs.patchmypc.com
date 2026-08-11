# Cloud Connection support for Multi-tenants in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Cloud** tab of Patch My PC (PMPC) Publisher allows you to connect the Publisher to your Patch My PC Cloud company. This connection enables the use of custom applications created in Patch My PC Cloud within the Publisher.

![Cloud Tab](../../../.gitbook/assets/image-\(4120\).png)

> \*\*Important\*\*
>
> The cloud connection is established between the Publisher instance and a single Patch My PC Cloud company. It is not configured per tenant. In multi-tenant environments, all tenants within the Publisher share the same cloud connection.

> \*\*Note\*\*
>
> The App Migration feature is not available for MSP or MSP Plus licenses. Although the Cloud tab is visible in the Publisher, the App Migration option is not displayed for these license types.
>
> Customers who have previously seen App Migration under different licensing scenarios may expect it to appear on this page. Its absence is expected behavior for MSP and MSP Plus licenses.

The primary purpose of the Cloud tab in MSP, multi-tenant, scenarios is to enable custom apps created in Patch My PC Cloud to be published through the Publisher.

## Considerations for MSPs

An **MSP** license does not enable use of the [Custom Apps](../../../patch-my-pc-cloud/custom-apps/) feature in Patch My PC Cloud.

While an MSP can create a Patch My PC Cloud company, the custom apps capability cannot be licensed or used with a standard **MSP** license.

> \*\*Note\*\*
>
> To use custom apps in Patch My PC Cloud, an \*\*MSP Plus\*\*, \*\*Enterprise Plus\*\*, or \*\*Enterprise Premium\*\* license is required.

**MSP Plus** customers will typically use Patch My PC Cloud to deliver applications and updates directly to their customers. However, there may be scenarios where an MSP Plus customer still requires the Publisher instance for a specific customer or use case. In this scenario, the recommended approach is:

* Create and manage custom applications in the MSP parent Patch My PC Cloud company. See the Publisher [Cloud page](../../../patch-my-pc-publisherv2/administration/cloud.md) for more details on hot to connect the Publisher to a Patch My PC Cloud Company.
* Once connected, the Publisher can access and publish the custom applications created in the MSP Cloud company.
* This model ensures that custom apps are centrally managed in Patch My PC Cloud while still allowing publication through the Publisher when required.

## Custom App Availability

All custom applications created in the MSP parent Patch My PC Cloud company are made available in the Publisher under the [All Custom Products](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md) node. These custom applications are visible in both the Intune Apps and Intune Updates tabs.

Because the Cloud connection is established at the Publisher instance level and not per tenant, the same set of custom applications is visible across all tenants configured in the Publisher.

Selection and configuration of custom applications remains tenant specific. You can enable, disable, and customize each custom application independently for each tenant by selecting the appropriate tenant from the tenant drop down list before making changes.

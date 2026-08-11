# Manage Security Scopes option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Manage security scopes** right-click option in Patch My PC (PMPC) Publisher allows you to control which ConfigMgr security scopes are applied to applications created by the Publisher.

During each synchronization, the Publisher applies the selected security scopes to any applications it creates in ConfigMgr. This ensures that applications are visible and manageable only by administrators with access to the assigned scopes.

The list of available security scopes is pulled directly from your ConfigMgr environment. You can refresh the list using the refresh button in the top right corner.

![Selecting a Security Scope](../../../.gitbook/assets/image-\(115\).png)

The list supports filtering using the **Filter items** field, and the visible columns can be customized by right-clicking the column headers.

## Enforce Security Scopes

You can optionally enable **Enforce selected security scopes**.

When enforcement is enabled, the Publisher ensures that only the selected scopes remain assigned to the application. If additional scopes are added manually in the ConfigMgr console, the Publisher will remove those scopes during the next synchronization.

This option is useful when you want to maintain strict control over application visibility and prevent scope drift caused by manual changes.

> \*\*Important\*\*
>
> When the Publisher runs on the ConfigMgr site server, no additional permissions are required. The Local System account already has the necessary rights to read and assign security scopes.
>
> Additional permissions are required only when the Publisher is installed on a remote server and connects to ConfigMgr.
>
> If you are using a custom ConfigMgr security role for the Publisher in a remote deployment, that role must include the following permissions:
>
> \* Application > Set Security Scope
>
> \* Security Scopes > Read
>
> If you are using the Patch My PC security role that is created when \[configuring the SMS Provider]\(../../../patch-my-pc-publisherv2/publisher-reference/configure-the-sms-provider-connection.md#option-2-import-security-roles) integration, these permissions are already included.

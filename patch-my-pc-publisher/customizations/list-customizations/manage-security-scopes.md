# Manage Security Scopes option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

The **Manage Security Scopes** right-click option in Patch My PC (PMPC) Publisher allows you to control which Microsoft Configuration Manager (ConfigMgr) security scopes are applied to applications created by Publisher.

During each synchronization, Publisher applies the selected security scopes to any applications it creates in ConfigMgr. This ensures that applications are visible and manageable only by administrators with access to the assigned scopes.

## To configure security scope tags:

1. Right-click the relevant item and select **Manage Security Scopes**. The list of available security scopes is retrieved directly from your ConfigMgr environment.

<figure><img src="../../../.gitbook/assets/image (956).png" alt="Select Security Scopes" width="450"><figcaption></figcaption></figure>

2. On the **Select Security Scopes** screen, check the relevant checkboxes beside the security scopes you want to configure.

{% hint style="success" %}
**Tip**

The list supports filtering using the **Filter items** field, and you can customize the visible columns by right-clicking the column headers.

You can also refresh the list using the refresh button in the top right corner.
{% endhint %}

3. You can optionally enable **Enforce selected Security Scopes** (see [Enforcing Security Scopes](manage-security-scopes.md#enforcing-security-scopes) for more information).
4. Click **OK**

## Enforcing Security Scopes

When enforcement is enabled, Publisher ensures that only the selected security scopes remain assigned to the application. If you manually add additional scopes in the ConfigMgr console, Publisher will remove them during the next synchronization.

This option is useful when you want strict control over application visibility and want toprevent scope drift caused by manual changes.

{% hint style="danger" %}
**Important**

When Publisher runs on the ConfigMgr Site Server, no additional permissions are required. The Local System account already has the necessary rights to read and assign security scopes.

Additional permissions are required only when Publisher is installed on a remote server and connects to ConfigMgr.

If you are using a custom ConfigMgr security role for Publisher in a remote deployment, that role must include the following permissions:

* **Application | Set Security Scope**
* **Security Scopes | Read**

If you are using the Patch My PC security role that is created when [configuring the SMS Provider](../../technical-references/configure-sms-provider.md) integration, these permissions are already included.
{% endhint %}

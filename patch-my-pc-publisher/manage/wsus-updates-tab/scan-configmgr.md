# Scan ConfigMgr in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Scan ConfigMgr** feature of Patch My PC (PMPC) Publisher requires access to your Microsoft Configuration Manager (ConfigMgr) site database to inventory installed applications via a Hardware Inventory Collection (HINV) and determine which third-party products are present in your environment.&#x20;

The scan results are then compared against the Patch My PC catalog to identify matches, helping you make informed decisions about which products to enable on the **WSUS Updates** tab to ensure the applications detected receive the patches they require.

{% hint style="info" %}
**Note**

The **Scan ConfigMgr** option applies only to ConfigMgr environments. WSUS does not natively maintain an application inventory of what is installed on client devices, so this scan cannot be performed in WSUS-only environments.
{% endhint %}

{% hint style="danger" %}
**Important**

The **Scan ConfigMgr** option is shared with the same option available under the [ConfigMgr Apps tab](../configmgr-apps-tab/) and behaves identically in both locations. As a result, this option under the **WSUS Updates** tab can be used to configure the same option under the **ConfigMgr Apps** tab, and vice versa.

Whilst the option itself is shared, manually selecting products in the [query](../configmgr-apps-tab/scan-configmgr.md#query) results only enables them on the tab from which the **Scan ConfigMgr** option was launched.

For example, launching **Scan ConfigMgr** from the **WSUS Updates** tab enables products for WSUS updates, whereas launching it from the **ConfigMgr Apps** tab enables products as applications.
{% endhint %}

{% hint style="info" %}
**Note**

See [Scan ConfigMgr](../configmgr-apps-tab/scan-configmgr.md) for more detailed information.
{% endhint %}

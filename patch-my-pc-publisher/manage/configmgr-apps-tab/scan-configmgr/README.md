# Scan ConfigMgr in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Scan ConfigMgr** tab of Patch My PC (PMPC) Publisher requires access to your ConfigMgr site database to inventory installed applications via a Hardware Inventory Collection (HINV) to determine which third-party products are present in your environment.

The scan results are then compared against the PMPC catalog to identify matches, helping you make informed decisions about which products to enable on the **ConfigMgr Apps** tab for deploying newer versions of those applications through Software Center, task sequences, or manual deployments.

{% hint style="info" %}
**Note**

The **Scan ConfigMgr** tab is shared with the tab of the same name under the **WSUS Updates** tab and behaves identically in both locations. As a result, you can use the **Scan ConfigMgr** tab under the **ConfigMgr Apps** tab to configure and control auto-publishing behavior on the **WSUS Updates** tab, and vice versa.

Although the tab is shared, manually selecting products in the [query](./#query-button) results enables them only on the tab from which **Scan ConfigMgr** was launched. For example, launching the scan wizard from the **WSUS Updates** tab enables products for updates, whereas launching it from the **ConfigMgr Apps** tab enables products as applications.
{% endhint %}

The following actions can be configured from the **Scan ConfigMgr** tab:

* [Configure SQL](sql-configuration.md)
* [Configure Auto-Publishing Rules](auto-publishing-rules.md)
* [Configure Filters](filters-discovered-products.md)
* [Perform a Query](filters-discovered-products.md#query-button)
* [Export to a CSV file](filters-discovered-products.md#export-to-csv-button)

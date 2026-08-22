# Scan Intune in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Scan Intune** tab of Patch My PC (PMPC) Publisher requires access to your Intune tenant through Microsoft Graph. It inventories installed applications to determine which third-party products are present in your environment.

The scan results are compared against Publisher's catalog to identify supported products. This information helps you decide which products to enable on the Intune Apps or Intune Updates tab for deploying newer versions of applications and updates through Intune as Win32 apps.

{% hint style="info" %}
**Note**

The **Scan Intune** tab is shared between the **Intune Apps** and the **Intune Updates** tab and behaves identically in both locations. As a result, the settings on the **Intune Apps** tab can be used to configure and control auto-publishing behavior on the **Intune Updates** tab, and vice versa.

While the form control itself is shared, manually selecting products in the query results only enables them on the tab from which the form was launched. For example, launching the scan wizard from the Intune Apps tab enables products for applications, whereas launching it from the Intune Updates tab enables products as updates.
{% endhint %}

{% hint style="success" %}
**Tip**

This form control will use the Entra ID App Registration, configured from the [Intune Options](../intune-options/) tab, to connect to Microsoft Graph to retrieve data from the Intune Reporting Endpoint. For more details about the required API permissions and authentication options, see [Entra ID App Registration](../../../requirements/intune-requirements/entra-id-app-registration/).
{% endhint %}

The following actions can be configured from the **Scan Intune** tab:

* [Configure Auto-Publishing Rules](auto-publishing-rules.md)
* [Configure Filters](filters.md)
* [Perform a Query](query-button.md)
* [Export to a CSV file](export-csv-button.md)

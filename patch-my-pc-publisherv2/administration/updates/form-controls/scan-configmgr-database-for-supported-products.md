# Scan ConfigMgr Database for Supported Products

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Scan ConfigMgr Database for Supported Products** form control requires access to your ConfigMgr site database to inventory installed applications, via a Hardware Inventory Collection (HINV) and determine which third-party products are present in your environment. The scan results are then compared against the Patch My PC catalog to identify matches, helping you make informed decisions about which products to enable on the **Updates** tab to ensure the applications detected receive the patches they require.

![Scan ConfigMgr Database for Supported Products](../../../../.gitbook/assets/image-\(3923\).png)

> \*\*Note\*\*
>
> The \*\*Scan ConfigMgr Database for Supported Products\*\* form control is only applicable for ConfigMgr environments. WSUS does not natively maintain an application inventory of what is installed on client devices, so this scan cannot be performed in WSUS-only environments.

> \*\*Important\*\*
>
> The \*\*Scan ConfigMgr Database for Supported Products\*\* form control is shared with the same form control available on the \[ConfigMgr Apps tab]\(../../configmgr-apps/) and behaves identically in both locations. As a result, the form control on the Updates tab can be used to configure and control auto-publishing behavior on the ConfigMgr Apps tab, and vice versa.
>
> While the form control itself is shared, manually selecting products in the \[query]\(scan-configmgr-database-for-supported-products.md#query) results only enables them on the tab from which the form was launched. For example, launching the scan wizard from the Updates tab enables products for updates, whereas launching it from the ConfigMgr Apps tab enables products as applications.

For more detailed instructions on using this form control, see [Scan ConfigMgr Database for Supported Products](../../configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md) under the [ConfigMgr Apps tab](../../configmgr-apps/) documentation.

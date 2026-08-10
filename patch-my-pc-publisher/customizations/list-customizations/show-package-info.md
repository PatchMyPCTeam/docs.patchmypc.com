# Show Package Info option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Products, Vendor, Product_\
_Available on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Show Package Info** right-click option in Patch My PC (PMPC) Publisher displays detailed update information for the currently synchronized catalog in Publisher. This information is read-only and reflects the latest metadata available from the Patch My PC catalog.

When selected for a single product, the option displays the specific package information for that product as defined in the PMPC catalog.&#x20;

When selected at the **All Products** or **Vendor** level, the package information for all applicable products within the scope is shown. This allows you to review and update details across multiple products at once.

## Package Details window

When you right-click a supported object in the Product Tree and select **Show Package Info**, the **Package Details** dialog displays the package metadata for the selected items.&#x20;

<figure><img src="../../../.gitbook/assets/image (4787).png" alt="&#x27;Package Details&#x27; dialog" width="563"><figcaption></figcaption></figure>

The grid shows one row per available package based on the current Product Tree selection. The information shown reflects what is in the latest PMPC catalog.

{% hint style="success" %}
**Tip**

Use the filtering options at the top of this dialog to help navigate it if you have selected several products/vendors.
{% endhint %}

<table><thead><tr><th width="138" valign="top">Field</th><th valign="top">Shows the...</th></tr></thead><tbody><tr><td valign="top">Vendor</td><td valign="top">Software publisher associated with the update.</td></tr><tr><td valign="top">Title</td><td valign="top">Product name, version, and architecture of the update package.</td></tr><tr><td valign="top">File</td><td valign="top">Installer file name that will be downloaded and used during deployment.</td></tr><tr><td valign="top">File Size</td><td valign="top">Size of the installer file.</td></tr><tr><td valign="top">Command-Line</td><td valign="top">Silent installation arguments Publisher will use when installing or updating the application.</td></tr><tr><td valign="top">Digest</td><td valign="top">Base64 encoded SHA1 file hash used to validate the integrity of </td></tr></tbody></table>

{% hint style="info" %}
**Note**

This information is useful when validating that you have the correct installer file while publishing a binary-free application and manually placing the installer in the [Staged Content Repository](../../manage/advanced-tab/staged-content-repository.md).
{% endhint %}

At the bottom of the window, the status text confirms the currently selected product scope.

You can use the **Export** button to export the details to a .CSV file for reference and the **Close** button to close the **Show Package Info** window.

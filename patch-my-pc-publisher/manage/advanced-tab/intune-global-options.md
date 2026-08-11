# Intune Global Options section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Intune Global Options** section of Patch My PC (PMPC) Publisher controls how the Publisher interacts with Microsoft Intune at a global level. They are primarily used to support advanced scenarios such as content extraction from Intune packages and tuning Microsoft Graph query behavior for large tenants.

![Intune Global Options](../../../.gitbook/assets/image-\(161\).png)

## Store encryption information locally to allow extraction of Win32 .intunewin files

The Publisher can store the encryption information used when creating Intune Win32 package files with the .intunewin extension. When this option is enabled, the encryption keys are retained locally and can later be used to download and extract the contents of Intune applications and updates.

This capability is required if you want to use the [Intune Application Manager](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/form-controls/intune-application-manager.md) to extract content from applications or updates that were published by the Publisher.

To enable encryption key storage, follow these steps.

1. Open the Publisher.
2. Navigate to the Advanced tab.
3. Under Intune Global Options, enable the setting labeled **Store encryption information locally to allow extraction of Win32 .intunewin files**.
4. Click Apply or Save and Close.

> \*\*Important\*\*
>
> Encryption information is only available for apps created after this option is enabled. You cannot extract content from Intune apps or updates that were created before the option was turned on.

### Extract Content

Once **Store encryption information locally to allow extraction of Win32 .intunewin files** is enabled, you can extract content for apps and updates created _after_ the setting was turned on by using the [Intune Application Manager](../../../patch-my-pc-publisherv2/administration/intune-apps-updates/form-controls/intune-application-manager.md).

To extract the content for eligible Win32 apps:

1. Open the Intune Apps or Intune Updates tab.
2. Launch the Intune Application Manager.
3. Right click an application or update.
4. Select **Extract Package**.

![Extract Package](../../../.gitbook/assets/image-\(3954\).png)

5. Specify an output path or browse to a folder.
6. Click Extract.

![Extraction Complete](../../../.gitbook/assets/image-\(3955\).png)

After extraction completes, File Explorer opens to the selected directory and displays the extracted content.

> \*\*Note\*\*
>
> If the Extract Content option is unavailable or greyed out, the encryption information was not collected at publish time. This typically occurs when the setting was enabled after the application or update was originally published.

## Number of items returned from Microsoft Graph

The Number of items to be returned when the Graph API returns paged results setting controls how many Intune objects are returned per page when the Publisher queries Microsoft Graph.

This option is useful in environments with a large number of applications, updates, or assignments. Lower values reduce the size of each response, which can help in slow or constrained network conditions. Higher values reduce the number of requests required to retrieve all data, which can improve performance in well connected environments.

* Default value: 20 items
* Minimum value: 1 item
* Maximum value: 999 items

In most scenarios, the default value of **20** is recommended. Adjust this setting only if you are troubleshooting performance or scalability issues related to Graph queries.

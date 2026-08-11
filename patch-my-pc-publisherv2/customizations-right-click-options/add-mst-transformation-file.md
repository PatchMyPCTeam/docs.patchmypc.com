# Add MST Transformation File

_Applies to: Patch My PC Publisher V2.x_

_Available at level: Product (only for MSI and MSP installers)_\
_&#x41;vailable on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

The **Add MST Transform File** option allows you to apply an MST transform to products that use an MSI based installer.

![Add MST Transformation File](/_images/image-(4020).png)

An MST transform modifies data stored in the MSI installer database and is commonly used to customize installation behavior, set properties, or adjust default settings. This functionality also applies to MSP based installers because MSP files are patch packages built on top of an MSI database. In both cases, the transform is applied during installation in the same manner.

## Using the MST Transform Files Dialog

In the MST Transform Files dialog, select the MST file you want to apply during installation. If the transform requires additional files, you can also select an optional supporting CAB file.

![MST Transform Files Dialog](/_images/image-(4021).png)

The selected MST and CAB files are automatically included when the application or update is published. You do not need to add these files separately as additional content.

> \*\*Note\*\*
>
> For ConfigMgr applications, Intune applications, and Intune updates, the MST and CAB files are placed in the application content directory. For WSUS and ConfigMgr updates, the files are packaged inside the update CAB file.

Once configured, these selections persist across future updates. The same transform continues to be applied automatically when newer versions of the product are published.

## Important Considerations

Some vendors require a new MST file for each new version of the application or installer. In these cases, an MST created for an earlier version may not be compatible with a newer installer.

The Publisher does not detect whether a vendor requires version specific MST files or whether an existing transform is no longer compatible. Because the selected MST is automatically carried forward to newer versions, it is important to review vendor documentation and validate transform compatibility after upgrades.

If a vendor requires version specific transforms, additional testing may be necessary. You may choose to use a longer testing or pilot period for deployments that rely on MST files to identify issues caused by outdated transforms before broader deployment. This may require balancing compliance timelines with the risk of transform related installation failures.
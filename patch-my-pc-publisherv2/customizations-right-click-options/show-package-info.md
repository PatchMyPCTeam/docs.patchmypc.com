# Show Package Info

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: All Products, Vendor, Product_\
_&#x41;vailable on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

## Overview

The **Show package info** option displays detailed update information for the currently synchronized catalog in the Publisher. This information is read only and reflects the latest metadata available from the Patch My PC catalog.

![Show Package Info](../../.gitbook/assets/image-\(157\).png)

When selected for a single product, the option displays the specific package information for that product as defined in the Patch My PC catalog.

When selected at the All Products or Vendor level, the option shows package information for all applicable products within the scope. This allows you to review update details across multiple products at once.

## Package Details window

The Package Details window displays the package metadata for the selected scope in the Publisher. This view is opened when the Show package info option is selected.

![Package Details](../../.gitbook/assets/image-\(159\).png)

The grid shows one row per available package based on the current product tree selection. The information shown reflects what is in the latest Patch My PC catalog.

* **Vendor** shows the software publisher associated with the update.
* **Title** shows the product name, version, and architecture of the update package.
* **File** shows the installer file name that will be downloaded and used during deployment.
* **File Size** shows the size of the installer file.
* **Command Line** shows the silent installation arguments that the Publisher will use when installing or updating the application.
* **Digest** shows the Base64 encoded SHA1 file hash used to validate the integrity of the installer.

> \*\*Note\*\*
>
> This information is useful when validating that you have the correct installer file while publishing a binary free application and manually placing the installer in the \[Local Content Repository]\(../administration/advanced/local-content-repository.md).

At the bottom of the window, the status text confirms the currently selected product scope. The **Export** button allows the package details to be saved for reference. The **Close** button exits the window.

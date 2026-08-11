# About

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **About** tab provides version and support information for the Publisher. The primary area of interest on this tab is Version Details. The remaining sections provide quick links to helpful resources on our website.

![About Tab](../../.gitbook/assets/image-\(167\).png)

## Version Details

**Currently Installed Version**\
The version shown indicates the version of the Publisher that is installed.

### **Latest Available Preview Version**

The version shown indicates the most recent preview build available for installation. Preview builds are early candidate releases for production. They may include new features, private or public preview functionality, or targeted fixes for known issues.

### **Last check for a new version**

The date shown indicates the date and time when the Publisher last checked for updates.

### **Disable self updates is (Not Recommended)**

This option can be used in controlled environments where version changes are managed through internal risk groups or formal change control processes. When this option is enabled, the Publisher will not automatically update to a newer version.

> \*\*Important\*\*
>
> If a critical fix or required feature is released, updates must be installed manually. In these scenarios, ensure operational procedures are in place to regularly review available updates so important releases are not missed.

### Install preview builds

This option controls whether preview versions are offered and installed. When enabled, the Publisher can install preview builds automatically.

Most environments should remain on production builds. In some cases, support may ask you to install a preview build to resolve a specific issue or to enable a feature under preview. If a preview build is installed for this purpose, it is recommended to return to the production channel once a new production release becomes available. To do this, clear the Install preview builds option.

## Restart service

The **Restart service** button restarts the Publishing Service and displays the current service state. This is useful after configuration changes or troubleshooting scenarios.

## Upgrade now

If a newer version of the Publisher is available and assigned to your update ring, the **Upgrade now** button becomes available. The Publisher uses a ringed deployment model, which means updates may be available on demand depending on your assigned ring.

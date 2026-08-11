# Version Details section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Version Details** section of the **About** tab of Patch My PC (PMPC) Publisher key version information for Publisher.

!['Version Details' section](/_images/image-(4832).png)

This section consists of the following areas:

* [Currently Installed Version](version-details.md#currently-installed-version)
* [Latest Version](version-details.md#latest-version)
* [Last Check for New Version](version-details.md#last-check-for-new-version)
* [Disable self-updates is (not recommended)](version-details.md#disable-self-updates-not-recommended)
* [Install preview builds](version-details.md#install-preview-builds)
* [Restart Service](version-details.md#restart-service-button)
* [Upgrade Now](version-details.md#upgrade-now-button)

## **Currently Installed Version**

Shows the version of Publisher currently installed.

## **Latest Version**

Shows the latest available version of Publisher.

## **Last Check for New Version**

Shows the last date and time that Publisher checked for a new version.

## **Disable self-updates (not recommended)**

This option can be used in controlled environments where version changes are managed by internal risk groups or formal change-control processes.

If checked, Publisher will not automatically update to a newer version.

> \*\*Important\*\*
>
> If a critical fix or required feature is released, updates must be installed manually. In these scenarios, ensure operational procedures are in place to regularly review available updates so important releases are not missed.

## Install preview builds

This option controls whether preview versions of Publisher are offered and installed.

When checked, the **Latest Available Preview Version** line appears, showing you the version number of the latest available preview version.

Most environments should remain on production builds. In some cases, support may ask you to install a preview build to resolve a specific issue or to enable a feature under preview.

If a preview build is installed for this purpose, it is recommended to return to the production channel once a new production release becomes available. To do this, uncheck the **Install preview builds** checkbox.

## Restart Service button

When clicked, the **Restart Service** button restarts the Publishing Service and displays the current service state. This is useful after configuration changes or troubleshooting scenarios.

## Upgrade Now button

If a newer version of Publisher is available and assigned to your update ring, the **Upgrade Now** button is available. Patch My PC uses a ringed deployment model for Publisher, which means updates may be available on demand depending on your assigned ring.
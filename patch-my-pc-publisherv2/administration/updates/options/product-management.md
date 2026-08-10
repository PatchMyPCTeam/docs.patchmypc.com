# Product Management

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Product Management** section is used to manage the Patch My PC update category within ConfigMgr. This category must be enabled for third-party updates published by Patch My PC to be synchronized by the Software Update Point (SUP).

![ConfigMgr/WSUS Product Management](../../../../.gitbook/assets/image-\(88\).png)

Selecting the **Selected in ConfigMgr** checkbox (or leaving it selected if it is already enabled) ensures that the corresponding Patch My PC product category is also selected in the **ConfigMgr Console > Administration > Site Configuration > Sites > {site} > Settings > Configure Site Components > Software Update Point > Products**. This guarantees that Patch My PC third-party updates are evaluated during a SUP sync.

![](../../../../.gitbook/assets/image-\(464\).png)

> [Important](https://learn.microsoft.com/en-us/intune/configmgr/develop/sum/about-synchronizing-the-software-update-point)
>
> In some environments, you may see two \*\*Patch My PC\*\* product categories. This most commonly occurs after an operating system upgrade (for example, Windows Server 2012 to 2019), where Microsoft changed how update categories are hashed. When this happens, the existing Patch My PC category is effectively re-hashed, causing ConfigMgr to detect it as a new category. As a result, both categories may appear with the same display name.
>
> In this scenario, both Patch My PC categories should be enabled in Publisher and under Software Update Point Component Properties > Products. This ensures that all Patch My PC updates continue to synchronize correctly, regardless of which category ID they are associated with.

Selecting the **Selected in WSUS** checkbox (or leaving it selected if it is already enabled) ensures that the corresponding Patch My PC product category is also selected in the **WSUS Console > Products and Classifications**.

![WSUS Products and Classifications](../../../../.gitbook/assets/image-\(89\).png)

## When does the Patch My PC category become visible?

Once the Publisher is installed, the **Patch My PC** product category is not visible immediately in ConfigMgr.

Typically, the category becomes available only after:

1. The first Patch My PC update is published to WSUS.
2. A SUP synchronization occurs.
3. ConfigMgr discovers the new third-party update category.

## Faster onboarding when the Publisher is on the site server

If the Publisher is installed on the ConfigMgr site server, you can evaluate the SUP component product categories immediately without having to wait for, or initiate, a SUP sync.

To acheive this:

* Restart the WCM (WSUS Configuration Manager) component from the Pubisher.
* This forces ConfigMgr to immediately re-evaluate WSUS categories
* The Patch My PC category becomes visible straight away

This functionality is documented in the [ConfigMgr Component Management](configmgr-component-management.md) section and is useful during initial setup to speed up onboarding.

## Logging

Patch My PC product information obtained from the SUP component properties in ConfigMgr, and the result of toggling the checkbox, are recorded in the _%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-SmsProviderConfigMgrRepository.log_

![%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-SmsProviderConfigMgrRepository.log](../../../../.gitbook/assets/image-\(465\).png)

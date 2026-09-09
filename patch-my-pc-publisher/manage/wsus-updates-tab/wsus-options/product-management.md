# Product Management section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Product Management** section on the **WSUS Options** tab of Patch My PC (PMPC) Publisher manages the **Patch My PC** update category in Microsoft Configuration Manager (ConfigMgr). This category must be enabled for third-party updates published by PMPC to be synchronized by the Software Update Point (SUP).

<figure><img src="../../../../.gitbook/assets/image (1008).png" alt="&#x27;Product Management&#x27; section" width="563"><figcaption></figcaption></figure>

Checking the **Selected in ConfigMgr** checkbox (or leaving it selected if it is already checked) ensures that the corresponding **Patch My PC** product category is also selected in the **ConfigMgr Console** under:

**Administration | Site Configuration | Sites |&#x20;**_**\<site>**_**&#x20;| Settings | Configure Site Components | Software Update Point | Products**.&#x20;

This guarantees that PMPC third-party updates are evaluated during a SUP sync.

<figure><img src="../../../../.gitbook/assets/image (464).png" alt="SUP Component Properties > Products" width="563"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

In some environments, you may see two **Patch My PC** product categories. This most commonly occurs after an operating system upgrade (for example, Windows Server 2012 to 2019), where Microsoft changed how update categories are hashed.&#x20;

When this happens, the existing Patch My PC category is effectively re-hashed, causing ConfigMgr to detect it as a new category. As a result, both categories may appear with the same display name.

In this scenario, enable both **Patch My PC** categories in Publisher and under **Software Update Point Component Properties | Products**. This ensures that all PMPC updates continue to synchronize correctly, regardless of which category ID they are associated with.
{% endhint %}

Checking the **Selected in WSUS** checkbox (or leaving it selected if it is already checked) ensures that the corresponding **Patch My PC** product category is also selected in the **WSUS Console** under **Products and Classifications**.

<figure><img src="../../../../.gitbook/assets/image (89).png" alt="WSUS Products and Classifications" width="347"><figcaption></figcaption></figure>

## When does the Patch My PC category become visible?

Once Publisher is installed, the **Patch My PC** product category is not visible in ConfigMgr immediately. It typically becomes available only after:

1. The first PMPC update is published to WSUS.
2. A SUP synchronization occurs.
3. ConfigMgr discovers the new third-party update category.

## Faster onboarding when Publisher is on the Site Server

If Publisher is installed on the ConfigMgr Site Server, you can evaluate the SUP component product categories immediately without waiting for or initiating a SUP sync.

To achieve this:

* Restart the WCM (WSUS Configuration Manager) component from Publisher.

{% hint style="info" %}
**Note**

See [ConfigMgr Component Management](configmgr-component-management.md) section for more information.
{% endhint %}

* This forces ConfigMgr to immediately re-evaluate WSUS categories.
* The **Patch My PC** category becomes visible straight away

## Logging

PMPC product information obtained from the SUP component properties in ConfigMgr, and the result of toggling the checkbox, are recorded in the **PatchMyPC-SmsProviderConfigMgrRepository.log** located at:

_**%ProgramFiles%**_**\Patch My PC\Patch My PC Publishing Service\Logs**

<figure><img src="../../../../.gitbook/assets/image (465).png" alt="%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-SmsProviderConfigMgrRepository.log" width="563"><figcaption></figcaption></figure>

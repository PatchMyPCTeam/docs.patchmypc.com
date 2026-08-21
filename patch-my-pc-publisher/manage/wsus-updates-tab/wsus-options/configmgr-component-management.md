# ConfigMgr Component Management section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **ConfigMgr Component Management** section in Patch My PC (PMPC) Publisher provides visibility into the **WSUS Configuration Manager (WCM)** component status. This section is primarily used during initial onboarding and troubleshooting scenarios where ConfigMgr needs to immediately re-evaluate WSUS configuration data.

<figure><img src="../../../../.gitbook/assets/image (87).png" alt="ConfigMgr Component Management" width="563"><figcaption></figcaption></figure>

When you publish your first Patch My PC update, the update is written to WSUS, but ConfigMgr does not become aware of the new Patch My PC product category until it re-processes WSUS configuration data. Normally, this happens during a Software Update Point (SUP) synchronization.

Restarting the WCM component triggers this re-evaluation without the need to perform a SUP sync. As a result, the Patch My PC product category becomes visible in the SUP component properties immediately.

The available actions are:

* Click **Query** to retrieve the current WCM component status from ConfigMgr. This action refreshes the status shown in the Publisher field **WCM Component Status** and does not make any configuration changes.
* Click **Restart** to restart the WCM component to force ConfigMgr to immediately re-evaluate the WSUS configuration on the site server. This includes subscribed products, classifications, and third party update categories.

{% hint style="info" %}
**Note**

We automatically attempt to restart the WCM component after the first Patch My PC update is published to ensure the new product category is properly recognized in ConfigMgr immediately.

The WCM component typically configures the WSUS server once every hour automatically to ensure that the settings configured in WSUS match the setting specified in the ConfigMgr console.
{% endhint %}

## Logging

These actions are logged in the _%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-ConfigMgrClient.log_ log.

<figure><img src="../../../../.gitbook/assets/image (467).png" alt="%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-ConfigMgrClient.log" width="563"><figcaption></figcaption></figure>

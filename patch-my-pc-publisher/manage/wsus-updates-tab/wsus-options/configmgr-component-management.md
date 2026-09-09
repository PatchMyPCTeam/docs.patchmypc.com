# ConfigMgr Component Management section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **ConfigMgr Component Management** section on the **WSUS Options** tab of Patch My PC (PMPC) Publisher shows the **WSUS Configuration Manager (WCM)** component status. This section is primarily used during initial onboarding and troubleshooting scenarios where Microsoft Configuration Manager (ConfigMgr) needs to immediately re-evaluate WSUS configuration data.

<figure><img src="../../../../.gitbook/assets/image (1007).png" alt="&#x27;ConfigMgr Component Management&#x27; section" width="563"><figcaption></figcaption></figure>

When you publish your first Patch My PC update, the update is written to WSUS, but ConfigMgr does not become aware of the new PMPC product category until it reprocesses WSUS configuration data. Normally, this happens during a Software Update Point (SUP) synchronization.

Restarting the WCM component triggers this re-evaluation without needing a SUP sync. As a result, the PMPC product category becomes visible in the SUP component properties immediately.

## Query button

Clicking **Query** retrieves the current WCM component status from ConfigMgr. This action refreshes the status shown in the Publisher field **WCM Component Status**, and does not make any configuration changes.

## Restart button

Clicking **Restart** restarts the WCM component, forcing ConfigMgr to immediately re-evaluate the WSUS configuration on the Site Server. This includes subscribed products, classifications, and third party update categories.

{% hint style="info" %}
**Note**

There is no UI displayed when you click **Restart**, only the spinning circle is displayed whilst Publisher does this.

We automatically attempt to restart the WCM component after the first PMPC update is published to ensure ConfigMgr recognizes the new product category immediately.

The WCM component typically configures the WSUS server once every hour automatically to ensure that the settings configured in WSUS match the settings specified in the ConfigMgr console.
{% endhint %}

## Logging

These actions are logged in:

_**%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-ConfigMgrClient.log**_

<figure><img src="../../../../.gitbook/assets/image (467).png" alt="%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-ConfigMgrClient.log" width="563"><figcaption></figcaption></figure>

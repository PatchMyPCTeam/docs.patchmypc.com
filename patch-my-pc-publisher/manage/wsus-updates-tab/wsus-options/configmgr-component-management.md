# ConfigMgr Component Management section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This article has not been updated for Version 3.x. Once it has, this banner will be removed.</p>
</blockquote>

The **ConfigMgr Component Management** section in Patch My PC (PMPC) Publisher provides visibility into the **WSUS Configuration Manager (WCM)** component status. This section is primarily used during initial onboarding and troubleshooting scenarios where ConfigMgr needs to immediately re-evaluate WSUS configuration data.

![ConfigMgr Component Management](/_images/image-(87).png "ConfigMgr Component Management")

When you publish your first Patch My PC update, the update is written to WSUS, but ConfigMgr does not become aware of the new Patch My PC product category until it re-processes WSUS configuration data. Normally, this happens during a Software Update Point (SUP) synchronization.

Restarting the WCM component triggers this re-evaluation without the need to perform a SUP sync. As a result, the Patch My PC product category becomes visible in the SUP component properties immediately.

The available actions are:

* Click **Query** to retrieve the current WCM component status from ConfigMgr. This action refreshes the status shown in the Publisher field **WCM Component Status** and does not make any configuration changes.
* Click **Restart** to restart the WCM component to force ConfigMgr to immediately re-evaluate the WSUS configuration on the site server. This includes subscribed products, classifications, and third party update categories.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>We automatically attempt to restart the WCM component after the first Patch My PC update is published to ensure the new product category is properly recognized in ConfigMgr immediately.&#x20;</p>
<p>The WCM component typically configures the WSUS server once every hour automatically to ensure that the settings configured in WSUS match the setting specified in the ConfigMgr console.</p>
</blockquote>

## Logging

These actions are logged in the _%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-ConfigMgrClient.log_ log.

![%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-ConfigMgrClient.log](/_images/image-(467).png "%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-ConfigMgrClient.log")
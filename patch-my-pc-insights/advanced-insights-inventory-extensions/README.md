# Advanced Insights Inventory Extensions

_Applies to: Patch My PC Advanced and Patch Insights_

Several features of Advanced Insights (this is not relevant for Patch Insights) require the deployment of our Inventory Extensions. This process adds additional reports and functionality to Configuration Manager.

To setup the Inventory Extensions, there are **two** actions to complete:

***

## ⚙ Extend ConfigMgr's Hardware Inventory Schema

1. Navigate to the **Administration** > **Settings** page&#x20;
2. Select the **Advanced Insights Inventory Extensions** tab
3. Select whether to collect **Microsoft Update** Compliance Data [see here for more information](../advanced-insights-and-microsoft-updates-inventory.md)
4. Click <mark style="color:green;">**Update Hardware Inventory via Advanced Insights**</mark>

![](/_images/Inventory_Extensions_Settings)

***

### ⚙ <mark style="color:yellow;">Manual</mark> Steps to Extend Hardware Inventory Schema

<blockquote class="wp-block-quote">
<p>Seeing this message suggests you need to configure [Configuration Manager Permissions](../insights-configuration-manager-permission-requirements.md). We recommend configuring permissions instead of proceeding with a manual install.</p>
</blockquote>

![](/_images/image002-(2).png)

{% file src="../..//_images/AdvancedInsights_SMS_DEF-(1).mof" %}
For manual import of Inventory Extension Classes into Hardware Inventory
{% endfile %}

1. Download **AdvancedInsights\_SMS\_DEF.mof**
2. In the ConfigMgr Console, navigate to **Administration** > **Client Settings** > **Default Client Settings** > **Hardware Inventory** > **Set Classes...**
3. From this page click **Import...** and select the **AdvancedInsights\_SMS\_DEF.mof**
4. Tick/untick the imported Inventory Classes as required

![](/_images/image-(1258).png "Inventory Classes displayed In Hardware Inventory Client Settings")

***

## 💿 Deploy the Inventory Extensions MSI to clients

<blockquote class="wp-block-quote">
<p>If you have previously deployed the "**PMPC Data Collection**" PowerShell Package, please ensure you delete its deployment before deploying the new **InventoryExtensions.msi**</p>
</blockquote>

![](/_images/image-(1325).png "ConfigMgr package \"PMPC Data Collection (LEGACY)\" to remove")

<blockquote class="wp-block-quote">
<p>After removing the deployment for the legacy PMPC Data Collection package, the **InventoryExtensions.msi** must be installed on clients you wish to collect inventory data from.</p>
</blockquote>

### Client-Side Requirements for the Inventory Extensions MSI

* Windows 10/11, Windows Server 2012 - 2022 (64-bit)
* .NET Framework 4.8

### To deploy the Advanced Insights Inventory Extensions from the Patch My PC Publisher

You can deploy the **Inventory Extensions** product via <mark style="color:green;">**Patch My PC Publishing Service**</mark>

1\. Open the Patch My PC Publisher, navigate to the ConfigMgr/Intune Apps tab and select **Patch My PC >** **Advanced Insights Inventory Extensions (MSI-x64)**

![](/_images/image-(1321).png "Advanced Insights Inventory Extensions app in the PMPC Publisher")

2\. To quickly sync this app to ConfigMgr/Intune without having to wait for all other selected apps and updates in the Publisher to evaluate and process, right click the **Advanced Insights Inventory Extensions (MSI-x64)** app and select **Publish this product during the next manual sync. (Selective sync).**

![](/_images/image-(1326).png "Choose \"Selective sync\" to publish the MSI quickly to ConfigMgr")

3\. On the **Sync Schedule** tab, click **Run Publishing Service Sync.**

![](/_images/image-(1327).png "Publisher Sync")

4\. Verify the **Inventory Extensions x.x.x.x (MSI-x64)** application was created and deploy it to your desired collection(s).

![](/_images/image-(1329).png "Inventory Extensions app created successfully")

<blockquote class="wp-block-quote is-note">
<p>We also recommend that you enable the Advanced Insights Inventory Extensions (MSI-x64) WSUS/Intune **UPDATE** to ensure your clients receive newer versions of the Inventory Extensions as they are released.</p>
</blockquote>

***

<blockquote class="wp-block-quote is-note">
<p>The Advanced Insights Inventory Extensions will add approximately 0.5 MB per-client to the Configuration Manager database. We recommend increasing the acceptable inventory file size from the default of 5MB to a minimum of 10MB.&#x20;</p>
<p>To do so, edit the below registry value on the ConfigMgr site server:</p>
<p>* **Registry key:** HKLM\Software\Microsoft\SMS\Components\SMS\_INVENTORY\_DATA\_LOADER</p>
<p>* **Registry value:** Max MIF Size&#x20;</p>
<p>* **Data:** 10485760 (decimal) / a00000 (hexadecimal)&#x20;</p>
</blockquote>
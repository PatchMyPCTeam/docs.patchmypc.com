# Advanced Insights Inventory Extensions

_Applies to: Patch My PC Advanced Insights_

Several features of Advanced Insights (this is not relevant for Patch Insights) require the deployment of our Inventory Extensions. This process adds additional reports and functionality to Configuration Manager.

To setup the Inventory Extensions, there are **two** actions to complete:

***

## ⚙ Extend ConfigMgr's Hardware Inventory Schema

1. Navigate to the **Administration** > **Settings** page
2. Select the **Advanced Insights Inventory Extensions** tab
3. Select whether to collect **Microsoft Update** Compliance Data [see here for more information](../advanced-insights-and-microsoft-updates-inventory.md)
4. Click <mark style="color:green;">**Update Hardware Inventory via Advanced Insights**</mark>

![](<../../.gitbook/assets/Inventory_Extensions_Settings (1)>)

***

### ⚙ Manual Steps to Extend Hardware Inventory Schema

> Seeing this message suggests you need to configure \[Configuration Manager Permissions]\(../insights-configuration-manager-permission-requirements.md). We recommend configuring permissions instead of proceeding with a manual install.

![](../../.gitbook/assets/image002-\(2\).png)

{% file src="../../.gitbook/assets/AdvancedInsights_SMS_DEF-(4).mof" %}
For manual import of Inventory Extension Classes into Hardware Inventory
{% endfile %}

1. Download **AdvancedInsights\_SMS\_DEF.mof**
2. In the ConfigMgr Console, navigate to **Administration** > **Client Settings** > **Default Client Settings** > **Hardware Inventory** > **Set Classes...**
3. From this page click **Import...** and select the **AdvancedInsights\_SMS\_DEF.mof**
4. Tick/untick the imported Inventory Classes as required

![](../../.gitbook/assets/image-\(1960\).png)

***

## 💿 Deploy the Inventory Extensions MSI to clients

> If you have previously deployed the "\*\*PMPC Data Collection\*\*" PowerShell Package, please ensure you delete its deployment before deploying the new \*\*InventoryExtensions.msi\*\*

![](../../.gitbook/assets/image-\(2027\).png)

> After removing the deployment for the legacy PMPC Data Collection package, the \*\*InventoryExtensions.msi\*\* must be installed on clients you wish to collect inventory data from.

### Client-Side Requirements for the Inventory Extensions MSI

* Windows 10/11, Windows Server 2012 - 2022 (64-bit)
* .NET Framework 4.8

### To deploy the Advanced Insights Inventory Extensions from the Patch My PC Publisher

You can deploy the **Inventory Extensions** product via <mark style="color:green;">**Patch My PC Publishing Service**</mark>

1\. Open the Patch My PC Publisher, navigate to the ConfigMgr/Intune Apps tab and select **Patch My PC >** **Advanced Insights Inventory Extensions (MSI-x64)**

![](../../.gitbook/assets/image-\(2023\).png)

2\. To quickly sync this app to ConfigMgr/Intune without having to wait for all other selected apps and updates in the Publisher to evaluate and process, right click the **Advanced Insights Inventory Extensions (MSI-x64)** app and select **Publish this product during the next manual sync. (Selective sync).**

![](../../.gitbook/assets/image-\(2028\).png)

3\. On the **Sync Schedule** tab, click **Run Publishing Service Sync.**

![](../../.gitbook/assets/image-\(2029\).png)

4\. Verify the **Inventory Extensions x.x.x.x (MSI-x64)** application was created and deploy it to your desired collection(s).

![](../../.gitbook/assets/image-\(2031\).png)

> \*\*Note\*\*
>
> We also recommend that you enable the Advanced Insights Inventory Extensions (MSI-x64) WSUS/Intune \*\*UPDATE\*\* to ensure your clients receive newer versions of the Inventory Extensions as they are released.

***

> \*\*Note\*\*
>
> The Advanced Insights Inventory Extensions will add approximately 0.5 MB per-client to the Configuration Manager database. We recommend increasing the acceptable inventory file size from the default of 5MB to a minimum of 10MB.
>
> To do so, edit the below registry value on the ConfigMgr site server:
>
> \* \*\*Registry key:\*\* HKLM\Software\Microsoft\SMS\Components\SMS\\\_INVENTORY\\\_DATA\\\_LOADER
>
> \* \*\*Registry value:\*\* Max MIF Size
>
> \* \*\*Data:\*\* 10485760 (decimal) / a00000 (hexadecimal)

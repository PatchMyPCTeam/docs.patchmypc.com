# "Intune" Page of the Patch My PC Advanced/Patch Insights for Intune Dashboard

_Applies to: Advanced/Patch Insights for Intune_

All Intune dashboard views are populated with data obtained from the customer's Microsoft Intune tenant via Microsoft Graph API.

The **Intune** dashboard page consists of the following five tabs, each containing a collection of dashboard items.

> \*\*Important\*\*
>
> We store your Intune data in a secure database for a total of three (3) hours, after which it is automatically deleted from our systems.
>
> For a detailed explanation on how we collect and process your Intune data, see \[Intune Data Collection]\(../technical-references/data-collected.md).

<table data-header-hidden><thead><tr><th width="122" align="center" valign="top"></th><th width="143.99993896484375" align="center" valign="top"></th><th width="128.77783203125" align="center" valign="top"></th><th width="145.77783203125" align="center" valign="top"></th><th width="172.6961669921875" align="center" valign="top"></th></tr></thead><tbody><tr><td align="center" valign="top"><a href="intune-page.md#devices-tab">Devices tab</a></td><td align="center" valign="top"><a href="intune-page.md#applications-tab">Applications tab</a></td><td align="center" valign="top"><a href="intune-page.md#compliance-tab">Compliance tab</a></td><td align="center" valign="top"><a href="intune-page.md#configuration-tab">Configuration tab</a></td><td align="center" valign="top"><a href="intune-page.md#operating-systems-tab">Operating Systems tab</a></td></tr></tbody></table>

![Intune tabs](../../../.gitbook/assets/image-\(269\).png)

> \*\*Note\*\*
>
> All views across all tabs apply only to Windows and macOS information.

## Devices tab

All dashboard items in this view are populated using properties from managed devices.

!['Devices' tab](../../../.gitbook/assets/image-\(22\).png)

### Managed Devices (Dash-stat)

Provides a total count of all Windows and macOS devices. The footer item uses the **complianceState** property to show a count of non-compliant devices.

![Managed Devices (Dash-stat)](../../../.gitbook/assets/image-\(273\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

**General** tab shows managed device properties.

!['General' tab](../../../.gitbook/assets/image-\(4404\).png)

**Apps** tab shows the managed app installation states for the specific device. The additional tabs (**Required Apps** and **Available Apps**), show lists of apps based on their install intent, which is read from the **assignments** property. Each item in the list can be clicked to launch the specific app modal.

!['App' tab](../../../.gitbook/assets/image-\(4402\).png)

**Discovered apps** tab shows a list of discovered apps from Intune device inventory.

!['Discovered apps' tab](../../../.gitbook/assets/image-\(4403\).png)

Each item in the list can be clicked to launch the specific discovered app modal.

### Low Disk Space % (Dash-stat)

Provides a count of all Windows and macOS devices with less than 20% free space of the system drive. This item uses both the **totalStorageSpaceInBytes** and **freeStorageSpaceInBytes** properties to calculate the counts.

![Low Disk Space % (Dash-stat)](../../../.gitbook/assets/image-\(277\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can be clicked to launch the specific device modal.

### Device Encryption (Dash-stat)

Provides a count of the encryption status of all Windows and macOS devices, and uses the **isEncrypted** property for the count.

![Device Encryption (Dash-stat)](../../../.gitbook/assets/image-\(259\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Stale Devices (Dash-stat)

Provides a count of all Windows and macOS devices that have not reported a successful Intune device check-in for over 45 days. This item uses the **lastSyncDateTime** property for the count.

![Stale Devices (Dash-stat)](../../../.gitbook/assets/image-\(260\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Device Types (Donut chart)

Provides a count of Windows and macOS managed device types. This uses the **deviceOperatingSystemSummary** property from the **ManagedDeviceOverview** endpoint.

![Device Types (Donut chart)](../../../.gitbook/assets/image-\(261\).png)

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Each device listed in the table can be clicked to open the corresponding device modal.

### Device Details (Donut chart)

Provides a count of Windows and macOS managed device models, and uses the **model** for the counts.

![Device Details](../../../.gitbook/assets/image-\(4287\).png)

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Each device listed in the table can be clicked on to launch the specific device modal.

You can also switch between **Device Manufacturer** and **Device Model** by clicking the hamburger menu for this donut.

### Managed Devices - Last Check-in (Donut chart)

Provides a count of Windows and macOS managed device last check-in data/time. This uses the **lastSyncDateTime** for **Today**, **Last 3 Days**, **Over 7 Days**, **Over 14 Days**, and **Over 30 Days** counts.

![Managed Devices - Last Check-in (Donut chart)](../../../.gitbook/assets/image-\(265\).png)

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Each device listed in the table can be clicked on to launch the specific device modal.

### Devices Not Encrypted (Table list)

Provides a table list view for all Windows and macOS managed devices that are not encrypted. This uses the **isEncrypted** property equals **false**. Clicking on any item in the table list launches the specific device modal.

![Devices Not Encrypted (Table list)](../../../.gitbook/assets/image-\(267\).png)

## Applications tab

All dashboard items in this view are populated using properties from managed apps (Windows and macOS) and the install state data from the Intune tenant.

![Applications tab](../../../.gitbook/assets/image-\(3861\).png)

![Applications tab 2](../../../.gitbook/assets/image-\(3862\).png)

### Managed Apps (Dash-stat)

Provides a count of all Windows and macOS managed apps. The footer item uses the **isAssigned** property to show a count of unassigned apps.

![Managed Apps (Dash-stat)](../../../.gitbook/assets/image-\(3863\).png)

Clicking this item loads a table list view of the full dataset. Each app listed in the table can also be clicked to launch the specific app modal.

**App modal Example:**

The **General** tab shows managed app properties, assignment, and device install state counts. Items in this view are not currently clickable.

![App modal Example](../../../.gitbook/assets/image-\(4380\).png)

The **Install State** tab displays a donut chart of device install state, and two additional tabs show lists of device and user install states. Items in this view are not currently clickable.

!['Install State' tab](../../../.gitbook/assets/image-\(3865\).png)

### Modified App – Last 24hrs (Dash-stat)

Provides a count of all Windows and macOS managed apps modified in the last 24hrs. This item uses the **lastModifiedDateTime** property for the count.

![Modified App – Last 24hrs (Dash-stat)](../../../.gitbook/assets/image-\(3866\).png)

Clicking this item loads a table list view of the full dataset. Each app listed in the table can also be clicked to launch the specific app modal.

### Unassigned Apps (Dash-stat)

Provides a count of all Windows and macOS managed apps that are unassigned. This item uses the **isAssigned** property for the count.

![Unassigned Apps (Dash-stat)](../../../.gitbook/assets/image-\(3867\).png)

Clicking this item loads a table list view of the full dataset. Each app listed in the table can also be clicked to launch the specific app modal.

### App Install Failed (Dash-stat)

Provides a count of all Windows and macOS managed apps that reporting a failed install state. This item uses the **FailedDeviceCount** property for the count. The footer item displays additional data from a slightly different perspective, showing how many apps are reporting **success** (**InstalledDeviceCount**) Vs how many apps have an active assignment (**isAssigned** is **true**).

![App Install Failed (Dash-stat)](../../../.gitbook/assets/image-\(3868\).png)

In this example:

* 108 apps have **active** assignments
* Of those 108 apps, 32 are reporting **success**
* Of those 108 apps, 9 are reporting **failed**.

Clicking this item loads a table list view of the full dataset. Each app listed in the table can also be clicked to launch the specific app modal.

### Managed Apps (Table list)

Provides a table list view for all Windows and macOS managed apps. Clicking any item in the table list launches the specific app modal.

![Managed Apps (Table list)](../../../.gitbook/assets/image-\(3869\).png)

### Managed App Types (Donut chart)

Provides a count of managed app types for Windows and macOS. This item uses the **platform** property for the count.

![Managed App Types (Donut chart)](../../../.gitbook/assets/image-\(3870\).png)

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Each app listed in the table can also be clicked to launch the specific app modal. For example:

![Table list view of the full dataset related to the clicked item](../../../.gitbook/assets/image-\(3871\).png)

### Managed App Install States (Donut chart)

Provides a count of Windows and macOS managed app install states, using the following properties for the count:

* **FailedDeviceCount**
* **FailedUserCount**
* **InstalledDeviceCount**
* **InstalledUserCount**
* **PendingInstallDeviceCount**
* **PendingInstallUserCount**
* **NotApplicableDeviceCount**
* **NotApplicableUserCount**
* **NotInstalledDeviceCount**
* **NotInstalledUserCount**

In this example, the active selection of the donut chart shows that there are a total of 44 devices reporting **failed install status** across all apps.

![Managed App Install States (Donut chart)](../../../.gitbook/assets/image-\(3872\).png)

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. The table view shows the **failed device count** grouped by app.

Each app listed in the table can also be clicked to launch the specific app modal. For example:

![Table view showing the failed device count grouped by app](../../../.gitbook/assets/image-\(3873\).png)

### Discovered Apps (Dash-stat)

Provides a count of all discovered apps, collected by Intune Inventory.

![Discovered Apps (Dash-stat)](../../../.gitbook/assets/image-\(3874\).png)

Clicking this item loads a table list view of the full dataset. Each discovered app listed in the table can also be clicked to launch the specific discovered app modal.

### Managed Devices - Discovered Apps (Table list)

Provides a table list view of all discovered apps, which are collected by Intune Inventory.

![Managed Devices - Discovered Apps (Table list)](../../../.gitbook/assets/image-\(3875\).png)

Clicking any item in the table list launches the specific discovered app list view which shows all devices where the specific app has been discovered. For example:

![Discovered app details example](../../../.gitbook/assets/image-\(3876\).png)

## Compliance tab

All dashboard items in this view are populated using properties from a collection of Intune objects, including managed device compliance state and compliance policy information.

![Compliance tab](../../../.gitbook/assets/image-\(3880\).png)

### Managed Devices (Dash-stat)

Provides a total count of all Windows and macOS devices. The footer item uses the **complianceState** property to show a count of non-compliant devices.

![Managed Devices (Dash-stat)](../../../.gitbook/assets/image-\(3881\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Non-compliant devices (Dash-stat)

Provides a total count of all Windows and macOS devices that are reporting a device compliance state not equal to **Compliant**. This item uses the **complianceState** property for the count.

![Non-compliant devices (Dash-stat)](../../../.gitbook/assets/image-\(3882\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Non-compliant policies (Dash-stat)

Provides a total count of compliance policies targeting Windows and macOS devices that have one or more devices reporting non-compliant against the specific policy.

![Non-compliant policies (Dash-stat)](../../../.gitbook/assets/image-\(3883\).png)

Clicking this item loads a table list view of the full dataset. Items in the table list cannot be clicked.

![Table list view of the full dataset](../../../.gitbook/assets/image-\(3884\).png)

### Intune compliance policies (Dash-stat)

Provides a total count of compliance policies targeting Windows and macOS devices.

![Intune compliance policies (Dash-stat)](../../../.gitbook/assets/image-\(3885\).png)

Clicking this item loads a table list view of the full dataset. Items in table list cannot be clicked.

### Device Compliance State (Donut chart)

Provides a count of Windows and macOS managed devices and their compliance state. This item uses the **complianceState** property for the count.

![Device Compliance State (Donut chart)](../../../.gitbook/assets/image-\(3886\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Device Compliance By Type (Donut chart)

Provides a count of Windows and macOS managed devices and their compliance state grouped by device type. This item uses the **operatingSystem** and **complianceState** property for the counts.

![Device Compliance By Type (Donut chart)](../../../.gitbook/assets/image-\(3887\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Policy Non-Compliant By Platforms (Donut chart)

Provides a total count of compliance policies targeting Windows and macOS devices that have one or more devices reporting non-compliant against the specific policy. The donut chart data is grouped by compliance policy platform targeted type property (**UnifiedPolicyPlatformType**).

![Policy Non-Compliant By Platforms (Donut chart)](../../../.gitbook/assets/image-\(3888\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Items in the table list cannot be clicked.

### Compliance Policies By Platforms (Donut chart)

Provides a total count of compliance policies targeting Windows and macOS devices. The donut chart data is grouped by compliance policy platform, targeted type, and property (**windows10CompliancePolicy** or **macOSCompliancePolicy**).

![Compliance Policies By Platforms (Donut chart)](../../../.gitbook/assets/image-\(3889\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Items in the table list cannot be clicked.

### Non-Compliant devices (Table list)

Provides a table list view including properties of Windows and macOS managed devices that have their **complianceState** property not equal to **Compliant**. Clicking any item in the table list launches the specific device modal.

![Non-Compliant devices (Table list)](../../../.gitbook/assets/image-\(3890\).png)

## Configuration tab

All dashboard items in this view are populated from properties of a collection of Intune objects, including managed device properties, Autopilot state events, and Windows Defender properties.

![Configuration tab](../../../.gitbook/assets/image-\(4289\).png)

### Managed Devices (Dash-stat)

Provides a total count of all Windows and macOS devices. The footer item uses the **complianceState** property to show a count of non-compliant devices.

![Managed Devices (Dash-stat)](../../../.gitbook/assets/image-\(3892\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Device Configuration Profile Issues (Dash-stat)

Provides a total count of all device configuration profiles (targeting Windows and macOS devices) that have either **conflict** or **error** assignment status.

![Device Configuration Profile Issues (Dash-stat)](../../../.gitbook/assets/image-\(3893\).png)

Clicking this item loads a table list view of the full dataset. The table lists the policy name and the number of devices reporting ‘conflict’ or ‘error’ assignment status. Items in the table list cannot be clicked.

![Table list view of the full dataset](../../../.gitbook/assets/image-\(3894\).png)

### Autopilot Events (Dash-stat)

Provides a total count of all Autopilot events. The footer item uses the **DeploymentState** property with the value **Failure** to show the count of events reporting **failure**.

![Autopilot Events (Dash-stat)](../../../.gitbook/assets/image-\(151\).png)

Clicking this item loads a table list view of the full dataset. Items in the table list cannot be clicked on in the current release.

![Example table list](../../../.gitbook/assets/image-\(152\).png)

### Autopilot Devices (Dash-stat)

Provides the total count of Autopilot-registered devices.

![Autopilot Devices (Dash-stat)](../../../.gitbook/assets/image-\(153\).png)

Clicking this item loads a table list view of the full dataset. Items in the table list cannot be clicked on in the current release.

![Example table](../../../.gitbook/assets/image-\(154\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Clicking any item in the table opens the corresponding device modal.

### Device Encryption Summary (Donut chart)

Provides a total count of managed device encryption status. The donut chart data is grouped by **EncryptionStatus** property.

![Device Encryption Summary (Donut chart)](../../../.gitbook/assets/image-\(4356\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Clicking any item in the table list launches the specific device modal.

Also, clicking the hamburger menu allows you to switch between **Encryption Status** and **Encryption Readiness**.

### Configuration Profile Issues (Donut chart)

Provides a total count of all device configuration profile types (targeting Windows and macOS devices) that have either **conflict** or **error** assignment events; grouped by policy type.

![Configuration Profile Issues (Donut chart)](../../../.gitbook/assets/image-\(3968\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. The table lists the policy name and the number of devices reporting ‘conflict’ or ‘error’ assignment status. Items in the table cannot be clicked.

![Example table](../../../.gitbook/assets/image-\(3969\).png)

### Autopilot Deployment States (Donut chart)

Provides a total count of Autopilot events. The donut chart data is grouped by **DeploymentState** property.

![Autopilot Deployment States (Donut chart)](../../../.gitbook/assets/image-\(3970\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Items in the table list cannot be clicked.

![Example table](../../../.gitbook/assets/image-\(3971\).png)

### Autopilot Device Enrollment States (Donut chart)

Provides a total count of Autopilot events. The donut chart data is grouped by **EnrollmentState** property.

![Autopilot Device Enrollment States (Donut chart)](../../../.gitbook/assets/image-\(3972\).png)

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Items in the table list cannot be clicked.

![Example table](../../../.gitbook/assets/image-\(3973\).png)

### Unhealthy Defender Agents (Donut chart)

Provides a total count of specific properties reported in the **Unhealthy endpoints** dataset from Intune (**Endpoint security > Antivirus**).

The donut chart data is grouped by the following properties:

* **MalwareProtectionEnabled**
* **NetworkInspectionSystemEnabled**
* **RealTimeProtectionEnabled**
* **SignatureUpdateOverdue**

![Unhealthy Defender Agents (Donut chart)](../../../.gitbook/assets/image-\(3975\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Clicking any item in the table opens the corresponding device modal.

![Example table](../../../.gitbook/assets/image-\(3976\).png)

### Device Enrollment Types (Donut chart)

Provides a count based on the **DeviceEnrollmentType** property for Windows and macOS managed devices. Clicking any segment opens the corresponding device modal.

![](../../../.gitbook/assets/image-\(4291\).png)

### Autopilot Enrollment Profile States (Donut chart)

Provides a total count of Autopilot devices by enrolment profile assignment state. The donut chart data is grouped by **DeploymentProfileAssignmentStatus** property.

![Autopilot Enrollment Profile States (Donut chart)](../../../.gitbook/assets/image-\(3977\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Items in the table list cannot be clicked.

![Example table](../../../.gitbook/assets/image-\(3978\).png)

## Operating Systems tab

All dashboard items in this view are populated using values from managed device properties.

![Operating Systems tab](../../../.gitbook/assets/image-\(139\).png)

### Managed Devices (Dash-stat)

Provides a total count of all Windows and macOS devices. The footer item uses the **complianceState** property to show a count of non-compliant devices.

![Managed Devices (Dash-stat)](../../../.gitbook/assets/image-\(140\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 11 Devices (Dash-stat)

Provides a total count of all Windows 11 devices. The footer item uses the OSVersion value and total count of all devices.

![Windows 11 Devices (Dash-stat)](../../../.gitbook/assets/image-\(141\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 10 Devices (Dash-stat)

Provides a total count of all Windows 10 devices. The footer item uses the OSVersion value and total count of all devices.

![Windows 10 Devices (Dash-stat)](../../../.gitbook/assets/image-\(142\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### macOS Devices (Dash-stat)

Provides a total count of all macOS devices.

![macOS Devices (Dash-stat)](../../../.gitbook/assets/image-\(143\).png)

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows OS SKU (Donut chart)

Provides a count of Windows-managed device OS editions, using the **skuFamily** and **OSVersion** properties for grouping and counting.

![Windows OS SKU (Donut chart)](../../../.gitbook/assets/image-\(144\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 11 OS Builds (Donut chart)

Provides a count of Windows-managed device OS versions, using the **osVersion** property for grouping and counts. Using the **OSVersion** property, we are able to translate that to the OS display name and build-friendly name.

![Windows 11 OS Builds (Donut chart)](../../../.gitbook/assets/image-\(145\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 10 OS Builds (Donut chart)

Provides a count of Windows-managed device OS versions, grouping by the **osVersion** property. By using this property, we are able to translate that to the OS display name and build-friendly name.

![Windows 10 OS Builds (Donut chart)](../../../.gitbook/assets/image-\(146\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### macOS Versions Count (Donut chart)

Provides a count of macOS-managed device OS versions, using the **osVersion** property for grouping and counting.

![macOS Versions Count (Donut chart)](../../../.gitbook/assets/image-\(147\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 11 Readiness Checks (Donut chart)

Provides a count of Windows devices and their Windows 11 readiness state, using the **UpgradeEligibility** property for the counts. The donut chart data is grouped by the following **UpgradeEligibility** values:

* **NotCapable**
* **Upgraded**’
* **Capable**
* **Unknown**

![Windows 11 Readiness Checks (Donut chart)](../../../.gitbook/assets/image-\(148\).png)

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

![Example table](../../../.gitbook/assets/image-\(149\).png)

### Supported Windows Versions

This data table is populated with Windows OS support lifecycle information, including release and end of support dates for Windows 10 and 11 operating systems. The data is obtained directly from Microsoft.

![Supported Windows Versions](../../../.gitbook/assets/image-\(150\).png)

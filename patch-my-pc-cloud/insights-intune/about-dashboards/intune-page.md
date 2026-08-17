# "Intune" Page of the Patch My PC Advanced/Patch Insights for Intune Dashboard

_Applies to: Advanced/Patch Insights for Intune_

All Intune dashboard views are populated with data obtained from the customer's Microsoft Intune tenant via Microsoft Graph API.

The **Intune** dashboard page consists of the following five tabs, each containing a collection of dashboard items.

{% hint style="danger" %}
**Important**

We store your Intune data in a secure database for a total of three (3) hours, after which it is automatically deleted from our systems.

For a detailed explanation on how we collect and process your Intune data, see [Intune Data Collection](../technical-references/data-collected.md).
{% endhint %}

<table data-header-hidden><thead><tr><th width="122" align="center" valign="top"></th><th width="143.99993896484375" align="center" valign="top"></th><th width="128.77783203125" align="center" valign="top"></th><th width="145.77783203125" align="center" valign="top"></th><th width="172.6961669921875" align="center" valign="top"></th></tr></thead><tbody><tr><td align="center" valign="top"><a href="intune-page.md#devices-tab">Devices tab</a></td><td align="center" valign="top"><a href="intune-page.md#applications-tab">Applications tab</a></td><td align="center" valign="top"><a href="intune-page.md#compliance-tab">Compliance tab</a></td><td align="center" valign="top"><a href="intune-page.md#configuration-tab">Configuration tab</a></td><td align="center" valign="top"><a href="intune-page.md#operating-systems-tab">Operating Systems tab</a></td></tr></tbody></table>

<figure><img src="../../../.gitbook/assets/image (268).png" alt="Intune tabs" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

All views across all tabs apply only to Windows and macOS information.
{% endhint %}

## Devices tab

All dashboard items in this view are populated using properties from managed devices.

<figure><img src="../../../.gitbook/assets/image (22).png" alt="&#x27;Devices&#x27; tab" width="563"><figcaption></figcaption></figure>

### Managed Devices (Dash-stat)

Provides a total count of all Windows and macOS devices. The footer item uses the **complianceState** property to show a count of non-compliant devices.

<figure><img src="../../../.gitbook/assets/image (140).png" alt="Managed Devices (Dash-stat)" width="442"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

**General** tab shows managed device properties.

<figure><img src="../../../.gitbook/assets/image (4404).png" alt="&#x27;General&#x27; tab" width="563"><figcaption></figcaption></figure>

**Apps** tab shows the managed app installation states for the specific device. The additional tabs (**Required Apps** and **Available Apps**), show lists of apps based on their install intent, which is read from the **assignments** property. Each item in the list can be clicked to launch the specific app modal.

<figure><img src="../../../.gitbook/assets/image (4402).png" alt="&#x27;App&#x27; tab" width="563"><figcaption></figcaption></figure>

**Discovered apps** tab shows a list of discovered apps from Intune device inventory.

<figure><img src="../../../.gitbook/assets/image (4403).png" alt="&#x27;Discovered apps&#x27; tab" width="563"><figcaption></figcaption></figure>

Each item in the list can be clicked to launch the specific discovered app modal.

### Low Disk Space % (Dash-stat)

Provides a count of all Windows and macOS devices with less than 20% free space of the system drive. This item uses both the **totalStorageSpaceInBytes** and **freeStorageSpaceInBytes** properties to calculate the counts.

<figure><img src="../../../.gitbook/assets/image (277).png" alt="Low Disk Space % (Dash-stat)" width="438"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can be clicked to launch the specific device modal.

### Device Encryption (Dash-stat)

Provides a count of the encryption status of all Windows and macOS devices, and uses the **isEncrypted** property for the count.

<figure><img src="../../../.gitbook/assets/image (259).png" alt="Device Encryption (Dash-stat)" width="438"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Stale Devices (Dash-stat)

Provides a count of all Windows and macOS devices that have not reported a successful Intune device check-in for over 45 days. This item uses the **lastSyncDateTime** property for the count.

<figure><img src="../../../.gitbook/assets/image (260).png" alt="Stale Devices (Dash-stat)" width="438"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Device Types (Donut chart)

Provides a count of Windows and macOS managed device types. This uses the **deviceOperatingSystemSummary** property from the **ManagedDeviceOverview** endpoint.

<figure><img src="../../../.gitbook/assets/image (261).png" alt="Device Types (Donut chart)" width="434"><figcaption></figcaption></figure>

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Each device listed in the table can be clicked to open the corresponding device modal.

### Device Details (Donut chart)

Provides a count of Windows and macOS managed device models, and uses the **model** for the counts.

<figure><img src="../../../.gitbook/assets/image (4287).png" alt="Device Details" width="196"><figcaption></figcaption></figure>

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Each device listed in the table can be clicked on to launch the specific device modal.

You can also switch between **Device Manufacturer** and **Device Model** by clicking the hamburger menu for this donut.

### Managed Devices - Last Check-in (Donut chart)

Provides a count of Windows and macOS managed device last check-in data/time. This uses the **lastSyncDateTime** for **Today**, **Last 3 Days**, **Over 7 Days**, **Over 14 Days**, and **Over 30 Days** counts.

<figure><img src="../../../.gitbook/assets/image (265).png" alt="Managed Devices - Last Check-in (Donut chart)" width="439"><figcaption></figcaption></figure>

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Each device listed in the table can be clicked on to launch the specific device modal.

### Devices Not Encrypted (Table list)

Provides a table list view for all Windows and macOS managed devices that are not encrypted. This uses the **isEncrypted** property equals **false**. Clicking on any item in the table list launches the specific device modal.

<figure><img src="../../../.gitbook/assets/image (267).png" alt="Devices Not Encrypted (Table list)" width="563"><figcaption></figcaption></figure>

## Applications tab

All dashboard items in this view are populated using properties from managed apps (Windows and macOS) and the install state data from the Intune tenant.

<figure><img src="../../../.gitbook/assets/image (3861).png" alt="Applications tab" width="563"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (3862).png" alt="Applications tab 2" width="563"><figcaption></figcaption></figure>

### Managed Apps (Dash-stat)

Provides a count of all Windows and macOS managed apps. The footer item uses the **isAssigned** property to show a count of unassigned apps.

<figure><img src="../../../.gitbook/assets/image (3863).png" alt="Managed Apps (Dash-stat)" width="438"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each app listed in the table can also be clicked to launch the specific app modal.

**App modal Example:**

The **General** tab shows managed app properties, assignment, and device install state counts. Items in this view are not currently clickable.

<figure><img src="../../../.gitbook/assets/image (4380).png" alt="App modal Example" width="563"><figcaption></figcaption></figure>

The **Install State** tab displays a donut chart of device install state, and two additional tabs show lists of device and user install states. Items in this view are not currently clickable.

<figure><img src="../../../.gitbook/assets/image (3865).png" alt="&#x27;Install State&#x27; tab" width="563"><figcaption></figcaption></figure>

### Modified App – Last 24hrs (Dash-stat)

Provides a count of all Windows and macOS managed apps modified in the last 24hrs. This item uses the **lastModifiedDateTime** property for the count.

<figure><img src="../../../.gitbook/assets/image (3866).png" alt="Modified App – Last 24hrs (Dash-stat)" width="436"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each app listed in the table can also be clicked to launch the specific app modal.

### Unassigned Apps (Dash-stat)

Provides a count of all Windows and macOS managed apps that are unassigned. This item uses the **isAssigned** property for the count.

<figure><img src="../../../.gitbook/assets/image (3867).png" alt="Unassigned Apps (Dash-stat)" width="443"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each app listed in the table can also be clicked to launch the specific app modal.

### App Install Failed (Dash-stat)

Provides a count of all Windows and macOS managed apps that reporting a failed install state. This item uses the **FailedDeviceCount** property for the count. The footer item displays additional data from a slightly different perspective, showing how many apps are reporting **success** (**InstalledDeviceCount**) Vs how many apps have an active assignment (**isAssigned** is **true**).

<figure><img src="../../../.gitbook/assets/image (3868).png" alt="App Install Failed (Dash-stat)" width="441"><figcaption></figcaption></figure>

In this example:

* 108 apps have **active** assignments
* Of those 108 apps, 32 are reporting **success**
* Of those 108 apps, 9 are reporting **failed**.

Clicking this item loads a table list view of the full dataset. Each app listed in the table can also be clicked to launch the specific app modal.

### Managed Apps (Table list)

Provides a table list view for all Windows and macOS managed apps. Clicking any item in the table list launches the specific app modal.

<figure><img src="../../../.gitbook/assets/image (3869).png" alt="Managed Apps (Table list)" width="563"><figcaption></figcaption></figure>

### Managed App Types (Donut chart)

Provides a count of managed app types for Windows and macOS. This item uses the **platform** property for the count.

<figure><img src="../../../.gitbook/assets/image (3870).png" alt="Managed App Types (Donut chart)" width="443"><figcaption></figcaption></figure>

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Each app listed in the table can also be clicked to launch the specific app modal. For example:

<figure><img src="../../../.gitbook/assets/image (3871).png" alt="Table list view of the full dataset related to the clicked item" width="563"><figcaption></figcaption></figure>

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

<figure><img src="../../../.gitbook/assets/image (3872).png" alt="Managed App Install States (Donut chart)" width="447"><figcaption></figcaption></figure>

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. The table view shows the **failed device count** grouped by app.

Each app listed in the table can also be clicked to launch the specific app modal. For example:

<figure><img src="../../../.gitbook/assets/image (3873).png" alt="Table view showing the failed device count grouped by app" width="563"><figcaption></figcaption></figure>

### Discovered Apps (Dash-stat)

Provides a count of all discovered apps, collected by Intune Inventory.

<figure><img src="../../../.gitbook/assets/image (3874).png" alt="Discovered Apps (Dash-stat)" width="438"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each discovered app listed in the table can also be clicked to launch the specific discovered app modal.

### Managed Devices - Discovered Apps (Table list)

Provides a table list view of all discovered apps, which are collected by Intune Inventory.

<figure><img src="../../../.gitbook/assets/image (3875).png" alt="Managed Devices - Discovered Apps (Table list)" width="563"><figcaption></figcaption></figure>

Clicking any item in the table list launches the specific discovered app list view which shows all devices where the specific app has been discovered. For example:

<figure><img src="../../../.gitbook/assets/image (3876).png" alt="Discovered app details example" width="563"><figcaption></figcaption></figure>

## Compliance tab

All dashboard items in this view are populated using properties from a collection of Intune objects, including managed device compliance state and compliance policy information.

<figure><img src="../../../.gitbook/assets/image (3880).png" alt="Compliance tab" width="563"><figcaption></figcaption></figure>

### Managed Devices (Dash-stat)

Provides a total count of all Windows and macOS devices. The footer item uses the **complianceState** property to show a count of non-compliant devices.

<figure><img src="../../../.gitbook/assets/image (140).png" alt="Managed Devices (Dash-stat)" width="442"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Non-compliant devices (Dash-stat)

Provides a total count of all Windows and macOS devices that are reporting a device compliance state not equal to **Compliant**. This item uses the **complianceState** property for the count.

<figure><img src="../../../.gitbook/assets/image (3882).png" alt="Non-compliant devices (Dash-stat)" width="443"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Non-compliant policies (Dash-stat)

Provides a total count of compliance policies targeting Windows and macOS devices that have one or more devices reporting non-compliant against the specific policy.

<figure><img src="../../../.gitbook/assets/image (3883).png" alt="Non-compliant policies (Dash-stat)" width="442"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Items in the table list cannot be clicked.

<figure><img src="../../../.gitbook/assets/image (3884).png" alt="Table list view of the full dataset" width="563"><figcaption></figcaption></figure>

### Intune compliance policies (Dash-stat)

Provides a total count of compliance policies targeting Windows and macOS devices.

<figure><img src="../../../.gitbook/assets/image (3885).png" alt="Intune compliance policies (Dash-stat)" width="443"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Items in table list cannot be clicked.

### Device Compliance State (Donut chart)

Provides a count of Windows and macOS managed devices and their compliance state. This item uses the **complianceState** property for the count.

<figure><img src="../../../.gitbook/assets/image (3886).png" alt="Device Compliance State (Donut chart)" width="363"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Device Compliance By Type (Donut chart)

Provides a count of Windows and macOS managed devices and their compliance state grouped by device type. This item uses the **operatingSystem** and **complianceState** property for the counts.

<figure><img src="../../../.gitbook/assets/image (3887).png" alt="Device Compliance By Type (Donut chart)" width="362"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Policy Non-Compliant By Platforms (Donut chart)

Provides a total count of compliance policies targeting Windows and macOS devices that have one or more devices reporting non-compliant against the specific policy. The donut chart data is grouped by compliance policy platform targeted type property (**UnifiedPolicyPlatformType**).

<figure><img src="../../../.gitbook/assets/image (3888).png" alt="Policy Non-Compliant By Platforms (Donut chart)" width="443"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Items in the table list cannot be clicked.

### Compliance Policies By Platforms (Donut chart)

Provides a total count of compliance policies targeting Windows and macOS devices. The donut chart data is grouped by compliance policy platform, targeted type, and property (**windows10CompliancePolicy** or **macOSCompliancePolicy**).

<figure><img src="../../../.gitbook/assets/image (3889).png" alt="Compliance Policies By Platforms (Donut chart)" width="442"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Items in the table list cannot be clicked.

### Non-Compliant devices (Table list)

Provides a table list view including properties of Windows and macOS managed devices that have their **complianceState** property not equal to **Compliant**. Clicking any item in the table list launches the specific device modal.

<figure><img src="../../../.gitbook/assets/image (3890).png" alt="Non-Compliant devices (Table list)" width="563"><figcaption></figcaption></figure>

## Configuration tab

All dashboard items in this view are populated from properties of a collection of Intune objects, including managed device properties, Autopilot state events, and Windows Defender properties.

<figure><img src="../../../.gitbook/assets/image (4289).png" alt="Configuration tab" width="563"><figcaption></figcaption></figure>

### Managed Devices (Dash-stat)

Provides a total count of all Windows and macOS devices. The footer item uses the **complianceState** property to show a count of non-compliant devices.

<figure><img src="../../../.gitbook/assets/image (140).png" alt="Managed Devices (Dash-stat)" width="442"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Device Configuration Profile Issues (Dash-stat)

Provides a total count of all device configuration profiles (targeting Windows and macOS devices) that have either **conflict** or **error** assignment status.

<figure><img src="../../../.gitbook/assets/image (3893).png" alt="Device Configuration Profile Issues (Dash-stat)" width="411"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. The table lists the policy name and the number of devices reporting ‘conflict’ or ‘error’ assignment status. Items in the table list cannot be clicked.

<figure><img src="../../../.gitbook/assets/image (3894).png" alt="Table list view of the full dataset" width="563"><figcaption></figcaption></figure>

### Autopilot Events (Dash-stat)

Provides a total count of all Autopilot events. The footer item uses the **DeploymentState** property with the value **Failure** to show the count of events reporting **failure**.

<figure><img src="../../../.gitbook/assets/image (151).png" alt="Autopilot Events (Dash-stat)" width="359"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Items in the table list cannot be clicked on in the current release.

<figure><img src="../../../.gitbook/assets/image (152).png" alt="Example table list" width="563"><figcaption></figcaption></figure>

### Autopilot Devices (Dash-stat)

Provides the total count of Autopilot-registered devices.

<figure><img src="../../../.gitbook/assets/image (153).png" alt="Autopilot Devices (Dash-stat)" width="359"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Items in the table list cannot be clicked on in the current release.

<figure><img src="../../../.gitbook/assets/image (154).png" alt="Example table" width="563"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Clicking any item in the table opens the corresponding device modal.

### Device Encryption Summary (Donut chart)

Provides a total count of managed device encryption status. The donut chart data is grouped by **EncryptionStatus** property.

<figure><img src="../../../.gitbook/assets/image (4356).png" alt="Device Encryption Summary (Donut chart)" width="211"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Clicking any item in the table list launches the specific device modal.

Also, clicking the hamburger menu allows you to switch between **Encryption Status** and **Encryption Readiness**.

### Configuration Profile Issues (Donut chart)

Provides a total count of all device configuration profile types (targeting Windows and macOS devices) that have either **conflict** or **error** assignment events; grouped by policy type.

<figure><img src="../../../.gitbook/assets/image (3968).png" alt="Configuration Profile Issues (Donut chart)" width="355"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. The table lists the policy name and the number of devices reporting ‘conflict’ or ‘error’ assignment status. Items in the table cannot be clicked.

<figure><img src="../../../.gitbook/assets/image (3969).png" alt="Example table" width="563"><figcaption></figcaption></figure>

### Autopilot Deployment States (Donut chart)

Provides a total count of Autopilot events. The donut chart data is grouped by **DeploymentState** property.

<figure><img src="../../../.gitbook/assets/image (3970).png" alt="Autopilot Deployment States (Donut chart)" width="438"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Items in the table list cannot be clicked.

<figure><img src="../../../.gitbook/assets/image (3971).png" alt="Example table" width="563"><figcaption></figcaption></figure>

### Autopilot Device Enrollment States (Donut chart)

Provides a total count of Autopilot events. The donut chart data is grouped by **EnrollmentState** property.

<figure><img src="../../../.gitbook/assets/image (3972).png" alt="Autopilot Device Enrollment States (Donut chart)" width="356"><figcaption></figcaption></figure>

Clicking any item in the donut chart loads a table list view of the full dataset related to the clicked item. Items in the table list cannot be clicked.

<figure><img src="../../../.gitbook/assets/image (3973).png" alt="Example table" width="563"><figcaption></figcaption></figure>

### Unhealthy Defender Agents (Donut chart)

Provides a total count of specific properties reported in the **Unhealthy endpoints** dataset from Intune (**Endpoint security > Antivirus**).

The donut chart data is grouped by the following properties:

* **MalwareProtectionEnabled**
* **NetworkInspectionSystemEnabled**
* **RealTimeProtectionEnabled**
* **SignatureUpdateOverdue**

<figure><img src="../../../.gitbook/assets/image (3975).png" alt="Unhealthy Defender Agents (Donut chart)" width="416"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Clicking any item in the table opens the corresponding device modal.

<figure><img src="../../../.gitbook/assets/image (3976).png" alt="Example table" width="563"><figcaption></figcaption></figure>

### Device Enrollment Types (Donut chart)

Provides a count based on the **DeviceEnrollmentType** property for Windows and macOS managed devices. Clicking any segment opens the corresponding device modal.

<figure><img src="../../../.gitbook/assets/image (4291).png" alt=""><figcaption></figcaption></figure>

### Autopilot Enrollment Profile States (Donut chart)

Provides a total count of Autopilot devices by enrolment profile assignment state. The donut chart data is grouped by **DeploymentProfileAssignmentStatus** property.

<figure><img src="../../../.gitbook/assets/image (3977).png" alt="Autopilot Enrollment Profile States (Donut chart)" width="363"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Items in the table list cannot be clicked.

<figure><img src="../../../.gitbook/assets/image (3978).png" alt="Example table" width="563"><figcaption></figcaption></figure>

## Operating Systems tab

All dashboard items in this view are populated using values from managed device properties.

<figure><img src="../../../.gitbook/assets/image (139).png" alt="Operating Systems tab" width="563"><figcaption></figcaption></figure>

### Managed Devices (Dash-stat)

Provides a total count of all Windows and macOS devices. The footer item uses the **complianceState** property to show a count of non-compliant devices.

<figure><img src="../../../.gitbook/assets/image (140).png" alt="Managed Devices (Dash-stat)" width="442"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 11 Devices (Dash-stat)

Provides a total count of all Windows 11 devices. The footer item uses the OSVersion value and total count of all devices.

<figure><img src="../../../.gitbook/assets/image (141).png" alt="Windows 11 Devices (Dash-stat)" width="413"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 10 Devices (Dash-stat)

Provides a total count of all Windows 10 devices. The footer item uses the OSVersion value and total count of all devices.

<figure><img src="../../../.gitbook/assets/image (142).png" alt="Windows 10 Devices (Dash-stat)" width="405"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### macOS Devices (Dash-stat)

Provides a total count of all macOS devices.

<figure><img src="../../../.gitbook/assets/image (143).png" alt="macOS Devices (Dash-stat)" width="416"><figcaption></figcaption></figure>

Clicking this item loads a table list view of the full dataset. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows OS SKU (Donut chart)

Provides a count of Windows-managed device OS editions, using the **skuFamily** and **OSVersion** properties for grouping and counting.

<figure><img src="../../../.gitbook/assets/image (144).png" alt="Windows OS SKU (Donut chart)" width="415"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 11 OS Builds (Donut chart)

Provides a count of Windows-managed device OS versions, using the **osVersion** property for grouping and counts. Using the **OSVersion** property, we are able to translate that to the OS display name and build-friendly name.

<figure><img src="../../../.gitbook/assets/image (145).png" alt="Windows 11 OS Builds (Donut chart)" width="413"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 10 OS Builds (Donut chart)

Provides a count of Windows-managed device OS versions, grouping by the **osVersion** property. By using this property, we are able to translate that to the OS display name and build-friendly name.

<figure><img src="../../../.gitbook/assets/image (146).png" alt="Windows 10 OS Builds (Donut chart)" width="419"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### macOS Versions Count (Donut chart)

Provides a count of macOS-managed device OS versions, using the **osVersion** property for grouping and counting.

<figure><img src="../../../.gitbook/assets/image (147).png" alt="macOS Versions Count (Donut chart)" width="413"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

### Windows 11 Readiness Checks (Donut chart)

Provides a count of Windows devices and their Windows 11 readiness state, using the **UpgradeEligibility** property for the counts. The donut chart data is grouped by the following **UpgradeEligibility** values:

* **NotCapable**
* **Upgraded**’
* **Capable**
* **Unknown**

<figure><img src="../../../.gitbook/assets/image (148).png" alt="Windows 11 Readiness Checks (Donut chart)" width="443"><figcaption></figcaption></figure>

Clicking any item in the donut chart opens a table view of the full dataset for that item. Each device listed in the table can also be clicked to launch the specific device modal.

<figure><img src="../../../.gitbook/assets/image (149).png" alt="Example table" width="563"><figcaption></figcaption></figure>

### Supported Windows Versions

This data table is populated with Windows OS support lifecycle information, including release and end of support dates for Windows 10 and 11 operating systems. The data is obtained directly from Microsoft.

<figure><img src="../../../.gitbook/assets/image (150).png" alt="Supported Windows Versions" width="563"><figcaption></figcaption></figure>

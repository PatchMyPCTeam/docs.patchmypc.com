---
description: Definition and technical description of each of our custom WMI Classes
---

# Insights WMI Class Definitions

_Applies to: Patch My PC Advanced Insights_

<blockquote class="wp-block-quote">
<p><mark style="color:yellow;">**Properties marked with \***</mark></p>
<p><mark style="color:yellow;">These properties can vary by hardware manufacturer. Data generation methods may differ between manufacturers and not all manufacturers may be supported. Users should consult the manufacturer's documentation for accurate interpretation of these properties where applicable.</mark></p>
</blockquote>

***

### PMPC\_Disks

**DeviceID:** Identifier that uniquely names the physical disk.

**BusType:** The interface the disk is connected by.

**MediaType:** Media type of the physical disk

<mark style="color:yellow;">**\***</mark>**Manufacturer:** The name of the manufacturer

<mark style="color:yellow;">**\***</mark>**HealthStatus:** A high-level indication of device health.

<mark style="color:yellow;">**\***</mark>**OperationalStatus:** Status further explaining a given health status.

<mark style="color:yellow;">**\***</mark>**Model:** This field represents the model number of the hardware

<mark style="color:yellow;">**\***</mark>**PowerOnHours:** Length of time, in hours, the storage device has been powered on since manufacture.

<mark style="color:yellow;">**\***</mark>**ReadErrorsTotal:** Total read errors encountered by the device.

<mark style="color:yellow;">**\***</mark>**SerialNumber:** Serial Number of the storage device

<mark style="color:yellow;">**\***</mark>**Temperature:** The current temperature of the storage device in Celsius

<mark style="color:yellow;">**\***</mark>**TemperatureMax:** The maximum temperature in Celsius at which the storage device is capable of normal operation.

<mark style="color:yellow;">**\***</mark>**Wear:** Storage device wear indicator, in percentage. At 100 percent, the estimated wear limit will have been reached.

<mark style="color:yellow;">**\***</mark>**WriteErrorsTotal:** Total write errors encountered by the device.

<mark style="color:yellow;">These properties are collected via SMART. Not all devices may support SMART monitoring</mark>

***

### PMPC\_Batteries

**BatteryID:** String identifying the battery.

**DesignCapacity:** The design capacity of the battery in milliwatt-hours.&#x20;

**FullChargeCapacity:** The full charge capacity of the battery in milliwatt-hours.&#x20;

**Health:** Comparison of the FullChargeCapacity to the DesignCapacity property is used to determine the health of the battery. (100 = Healthy)

<mark style="color:yellow;">**\***</mark>**Chemistry:** Describes the batteries chemistry.

<mark style="color:yellow;">**\***</mark>**Manufacturer:** The name of the manufacturer

<mark style="color:yellow;">**\***</mark>**ManufacturerDate:** The date the battery was manufactured

<mark style="color:yellow;">**\***</mark>**SerialNumber:** Serial Number of the battery

***

### PMPC\_ODBC

**DataSourceName:** Name of the ODBC

**Database:** The Display Name of the Application

**Description:** The reported version of the application.

**Driver:** The driver used for the ODBC

**DriverVersion:** The specific file version of the driver

**Platform:** Specifies whether the ODBC is 64/32 bit

**User:** The name of the user that owns the ODBC (if applicable).

***

### PMPC\_UserApps

**InstallLocation:** The folder location in which the application is installed

**DisplayName:** The Display Name of the Application

**DisplayVersion:** The reported version of the application.

**InstallDate:** The date the application was installed.

**Publisher:** The name of the publisher of the application.

**QuietUninstallString:** command line string to uninstall the application.

**UninstallString:** command line string for silent uninstall of the application.

**User:** The name of the user that installed the application.

***

### PMPC\_LocalGroups

**GroupName:** Name of the local group.

**Members:** List of user members belonging to that local group.&#x20;

**GroupMembers:** List of sub groups that are members of the local group

<mark style="color:yellow;">If a member cannot be identified the SID will be displayed instead.</mark>

***

### PMPC\_Dock

<blockquote class="wp-block-quote">
<p>Please note that collection of this data requires additional software from the vendors to be installed on clients:</p>
<p>* HP - <a href="https://www.hp.com/us-en/solutions/client-management-solutions/download.html">HP Dock Accessory Provider</a></p>
<p>* Lenovo - <a href="https://pcsupport.lenovo.com/us/el/solutions/ht037099">Lenovo Dock Manager</a></p>
<p>* DELL - <a href="https://www.dell.com/support/kbdoc/en-us/000177080/dell-command-monitor">Dell Command Monitor</a> (or DSIA)</p>
</blockquote>

**DeviceName:** Identified name of the dock device.

<mark style="color:yellow;">**\***</mark>**Firmware:** The firmware version currently installed on the dock

<mark style="color:yellow;">**\***</mark>**Manufacturer:** Manufacturer of the dock

<mark style="color:yellow;">**\***</mark>**SerialNumber:** Serial Number of the dock if applicable (For dell this is the same as service tag)

**PnPID:** Device "PnP" Id, this is only used if we werent able to identify the dock model

***

### PMPC\_Monitors

**InstanceName:** Unique Identifier for the monitor

**DeviceName:** Name of the monitor

**InchSize:** Diagonal size of monitor

**ConnectionType:** The cable used to connect to monitor

**Primary:** Whether this monitor is configured as the primary display. True or False.&#x20;

**ResolutionHorizontal:** Maximum horizontal pixel count

**ResolutionVertical:** Maximum vertical pixel count

<mark style="color:yellow;">**\***</mark>**Model:** Model of the monitor

<mark style="color:yellow;">**\***</mark>**SerialNumber:** Serial number of monitor (service tag for DELL)

<mark style="color:yellow;">**\***</mark>**Manufacturer:** Name of manufacturer

<mark style="color:yellow;">**\***</mark>**ManufactureYear:** Year the monitor was made

***

### PMPC\_Updates

**UpdateId:** unique ID that represents the update

**Title:** Title of the update.

**Status:** Missing or Installed.

**Service:** The Update Service used to discover this update.

**Product:** Product associated with the update

**ProductID:** ProductID associated with the update

**InstalledOn:** Date the update was Installed On

**DatePosted:** Date the updated was release or revised

**ArticleId:** KB article ID identifying the update

***

### PMPC\_WifiInterface

**GUID:** unique ID that represents the Wifi Interface

**Description:** Name / description of the interface

**Authentication:** Type of authentication used (e.g., WPA2, WEP, Open)

**Band:** Frequency band used (e.g., 2.4GHz, 5GHz)

**Channel:** Current operating channel

**Cipher:** Encryption cipher used (e.g., AES, TKIP)

**ConnectionMode:** Mode of connection&#x20;

**Driver Version:** Version of the driver software controlling the interface

**PhysicalAddress:** MAC address of the interface

**RadioType:** Type of wireless radio (e.g., 802.11n, 802.11ac)

**Signal:** Percentage signal strength of the connection

**SSID:** Name of the wireless network

**State:** Current state of the interface (e.g., connected, disconnected)

***

### PMPC\_UserProfile

**SID:** Security Identifier associated with the user profile

**Path:** File path where the user profile is stored

**LastLoggedIn:** Date and time of the user's last login

**AccountName:** Name of the user account

**SizeGB:** Size of the user profile in gigabytes



***

### PMPC\_BrowserExtension

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Supported Browsers:</p>
<p>* Chrome</p>
<p>* Edge</p>
<p>* Brave</p>
<p>* Firefox</p>
<p>* Opera</p>
</blockquote>

**InstallPath:** Path of the extension content and manifest

**Name:** Name of the extension

**Author:** The reported author of the browser extension acording to the manifest

**Browser:** The browser that the extension is installed in.

**User:** The user that has the extension installed. (All browser extensions are per user)

**ID:** ID of the Browser Extension associated with Chrome / Edge store

**Version:** The version of the browser extension
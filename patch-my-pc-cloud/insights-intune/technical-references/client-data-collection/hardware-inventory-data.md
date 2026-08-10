# Hardware Inventory Data Collection in Patch My PC Advanced/Patch Insights for Intune

_Applies to: Advanced/Patch Insights for Intune_

This article documents the hardware inventory data collected by the Patch My PC (PMPC) Advanced/Patch Insights for Intune client.

| [BatteryHealth](hardware-inventory-data.md#batteryhealth)                                      | [DisplayMonitor](hardware-inventory-data.md#displaymonitor)                                         | [NetworkAdapter](hardware-inventory-data.md#user-content-f0-9f-93-81-networkadapter)                 |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| [Processor](hardware-inventory-data.md#user-content-f0-9f-93-81-processor)                     | [SystemInfo](hardware-inventory-data.md#systeminfo)                                                 | [Win32\_ComputerSystem](hardware-inventory-data.md#user-content-f0-9f-93-81-win32_computersystem)    |
| [Win32\_DiskDrive](hardware-inventory-data.md#user-content-f0-9f-93-81-win32_computersystem-1) | [Win32\_PhysicalMemory](hardware-inventory-data.md#user-content-f0-9f-93-81-win32_computersystem-2) | [Win32\_VideoController](hardware-inventory-data.md#user-content-f0-9f-93-81-win32_computersystem-3) |

## BatteryHealth

### Cinv 103

| Name               | Type   | Description                                      | Data Source          |
| ------------------ | ------ | ------------------------------------------------ | -------------------- |
| BatteryID          | string | Unique identifier for the battery                | PowerCfg/ FileSystem |
| Chemistry          | string | Battery chemistry type (e.g., Li-ion, NiMH)      | PowerCfg/ FileSystem |
| DesignCapacity     | int    | Original design capacity of the battery in mWh   | PowerCfg/ FileSystem |
| FullChargeCapacity | int    | Battery full charge capacity in mWh              | PowerCfg/ FileSystem |
| Health             | int    | Calculated health percentage (FullCharge/Design) | Calculated           |
| Manufacturer       | string | Battery manufacturer                             | PowerCfg/ FileSystem |
| SerialNumber       | string | Battery serial number                            | PowerCfg/ FileSystem |

## DisplayMonitor

### Cinv 103

| Name                 | Type   | Description                                     | Data Source |
| -------------------- | ------ | ----------------------------------------------- | ----------- |
| ConnectionType       | string | Connection interface (e.g., HDMI, DisplayPort)  | WMI         |
| DeviceName           | string | Identifier of the display device                | WMI         |
| HeightCm             | int    | Physical height of the screen in centimeters    | WMI         |
| HorizontalResolution | int    | Screen horizontal resolution in pixels          | WMI         |
| IsPrimary            | bool   | Indicates if the display is the primary monitor | WMI         |
| ManufactureYear      | int    | Year the display was manufactured               | WMI         |
| Model                | string | Display model name                              | WMI         |
| Manufacturer         | string | Display manufacturer                            | WMI         |
| ScreenSize           | float  | Diagonal screen size in inches                  | Calculated  |
| SerialNumber         | string | Manufacturer serial number                      | WMI         |
| VerticalResolution   | int    | Screen vertical resolution in pixels            | WMI         |
| WidthCm              | int    | Physical width of the screen in centimeters     | WMI         |
| XPosition            | int    | Horizontal position in multi-monitor setup      | WMI         |

## NetworkAdapter <a href="#user-content-f0-9f-93-81-networkadapter" id="user-content-f0-9f-93-81-networkadapter"></a>

### Cinv 103

| Name                                                     | Type   | Description                                                   | Data Source |
| -------------------------------------------------------- | ------ | ------------------------------------------------------------- | ----------- |
| AuthenticationType<mark style="color:red;">**\***</mark> | string | Network authentication type (e.g., WPA2, Open)                | Netsh       |
| Band<mark style="color:red;">**\***</mark>               | string | Wireless frequency band (e.g., 2.4GHz, 5GHz)                  | Netsh       |
| Channel<mark style="color:red;">**\***</mark>            | int    | Wireless channel number                                       | Netsh       |
| DefaultGateway                                           | string | Default gateway addresses                                     | WMI         |
| Description                                              | string | Description of the network adapter                            | WMI         |
| DnsServers                                               | string | List of DNS servers configured for the adapter                | WMI         |
| DriverVersion                                            | string | Version of the network adapter driver                         | WMI         |
| InterfaceId                                              | string | Unique identifier for the network interface                   | WMI         |
| InterfaceType                                            | uint   | Numeric identifier for interface type (e.g., Ethernet, Wi-Fi) | WMI         |
| IpAddresses                                              | string | List of IP addresses assigned to the adapter                  | WMI         |
| IsConnected                                              | bool   | Indicates if the adapter is currently connected               | WMI         |
| MacAddress                                               | string | Media Access Control address                                  | WMI         |
| RadioType<mark style="color:red;">**\***</mark>          | string | Wireless radio type (e.g., 802.11ac)                          | Netsh       |
| SignalStrength<mark style="color:red;">**\***</mark>     | int    | Strength of the wireless signal (e.g., dBm or %)              | Netsh       |
| SSID<mark style="color:red;">**\***</mark>               | string | Network SSID (name)                                           | Netsh       |
| SubnetMask                                               | string | Subnet mask(s) associated with the adapter                    | WMI         |

<mark style="color:red;">**\***</mark> Wi-fi only

## Processor <a href="#user-content-f0-9f-93-81-processor" id="user-content-f0-9f-93-81-processor"></a>

### Cinv 103

| Name          | Type   | Description                               | Data Source |
| ------------- | ------ | ----------------------------------------- | ----------- |
| Architecture  | uint   | CPU architecture code (e.g., x64, ARM)    | WMI         |
| BaseSpeed     | uint   | Base clock speed of the processor in MHz  | WMI         |
| Cores         | uint   | Total number of logical cores             | WMI         |
| IsVirtual     | bool   | Indicates if the processor is virtualized | WMI         |
| PhysicalCores | uint   | Number of physical cores                  | WMI         |
| ProcessorId   | int    | Unique processor identifier               | WMI         |
| ProcessorName | string | Name of the processor (e.g., model name)  | WMI         |
| Sockets       | int    | Number of CPU sockets available           | WMI         |

## SystemInfo

### Cinv 103

| Name         | Type      | Description                        | Data Source |
| ------------ | --------- | ---------------------------------- | ----------- |
| Model        | string    | The system or device model name    | WMI         |
| ChassisTypes | string\[] | Array of chassis type descriptions | WMI         |

## Win32\_ComputerSystem <a href="#user-content-f0-9f-93-81-win32_computersystem" id="user-content-f0-9f-93-81-win32_computersystem"></a>

### Hinv 101

| Name         | Type   | Description                    | Data Source |
| ------------ | ------ | ------------------------------ | ----------- |
| ComputerName | string | Name of the computer           | WMI         |
| ComputerType | string | Description of computer type   | WMI         |
| Domain       | string | Domain the computer belongs to | WMI         |
| Manufacturer | string | Manufacturer of the device     | WMI         |
| Model        | string | Device model                   | WMI         |

## Win32\_DiskDrive <a href="#user-content-f0-9f-93-81-win32_computersystem" id="user-content-f0-9f-93-81-win32_computersystem"></a>

### Hinv 101

| Name        | Type   | Description               | Data Source |
| ----------- | ------ | ------------------------- | ----------- |
| Description | string | Description of the device | WMI         |
| DeviceId    | string | Unique device identifier  | WMI         |
| Model       | string | Device model              | WMI         |
| Name        | string | Device name or caption    | WMI         |
| Size        | string | Size or capacity in bytes | WMI         |
| Status      | string | Predictive Failure status | WMI         |

## Win32\_PhysicalMemory <a href="#user-content-f0-9f-93-81-win32_computersystem" id="user-content-f0-9f-93-81-win32_computersystem"></a>

### Hinv 101

| Name                 | Type   | Description                   | Data Source |
| -------------------- | ------ | ----------------------------- | ----------- |
| BankLabel            | string | Label of the memory bank      | WMI         |
| Capacity             | string | Capacity of the device        | WMI         |
| ConfiguredClockSpeed | string | Configured clock speed in Mhz | WMI         |
| DeviceLocator        | string | Physical device location      | WMI         |
| Tag                  | string | Unique identifier tag         | WMI         |

## Win32\_VideoController <a href="#user-content-f0-9f-93-81-win32_computersystem" id="user-content-f0-9f-93-81-win32_computersystem"></a>

### Hinv 101

| Name          | Type   | Description                | Data Source |
| ------------- | ------ | -------------------------- | ----------- |
| DeviceId      | string | Unique device identifier   | WMI         |
| DriverDate    | string | Date of the driver         | WMI         |
| DriverVersion | string | Version of the driver      | WMI         |
| Name          | string | Name of the device         | WMI         |
| RAM           | string | Amount of RAM (AdapterRAM) | WMI         |

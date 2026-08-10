# Software Inventory Data Collection in Patch My PC Advanced/Patch Insights for Intune

_Applies to: Advanced/Patch Insights for Intune_

This article documents the software inventory data collected by the Patch My PC (PMPC) Advanced/Patch Insights for Intune client.

| [AntiSpywareProduct](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry)        | [AntiVirusProduct](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-1)   | [FirewallProduct](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-2)         |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| [MicrosoftUpdateCompliance](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry) | [OsServicingChannel](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-1) | [RebootStatus](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-2)            |
| [SoftwareRegistryEntry](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-3)   | [UpdateCompliance](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-4)   | [UpdateComplianceSummary](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-5) |
| [Win32\_BIOS](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-6)             | [Win32\_LogicalDisk](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-7) | [Win32\_OperatingSystem](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-7)  |
| [WuaMetadata](software-inventory-data.md#user-content-f0-9f-93-81-softwareregistryentry-5)             |                                                                                                   |                                                                                                        |

## AntiSpywareProduct <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Hinv 101

| Name        | Type   | Description             | Data Source |
| ----------- | ------ | ----------------------- | ----------- |
| displayName | string | Name of the AntiSpyware | WMI         |

## AntiVirusProduct <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Hinv 101

| Name        | Type   | Description           | Data Source |
| ----------- | ------ | --------------------- | ----------- |
| displayName | string | Name of the AntiVirus | WMI         |

## FirewallProduct <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Hinv 101

| Name        | Type   | Description          | Data Source |
| ----------- | ------ | -------------------- | ----------- |
| displayName | string | Name of the Firewall | WMI         |

## MicrosoftUpdateCompliance <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Uinv 104

| Name           | Type   | Description                                                  | Data Source        |
| -------------- | ------ | ------------------------------------------------------------ | ------------------ |
| UpdateID       | string | Unique identifier for the Microsoft update                   | Windows Update API |
| Name           | string | Name of the update                                           | Windows Update API |
| IsInstalled    | bool   | Indicates whether the update is installed                    | Windows Update API |
| Classification | int    | Classification code of the update (e.g., security, critical) | Windows Update API |

## OsServicingChannel <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Cinv 103

| Name           | Type   | Description              | Data Source  |
| -------------- | ------ | ------------------------ | ------------ |
| ServiceChannel | string | The OS servicing channel | WMI/Registry |

## RebootStatus <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Cinv 103

| Name      | Type   | Description                              | Data Source         |
| --------- | ------ | ---------------------------------------- | ------------------- |
| IsPending | bool   | Indicates if a system reboot is pending  | Registry/FileSystem |
| Reasons   | string | List of reasons why a reboot is required | Inferred            |

## SoftwareRegistryEntry <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Cinv 103 <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

| Name              | Type     | Description                                                    | Data Source |
| ----------------- | -------- | -------------------------------------------------------------- | ----------- |
| DisplayName       | string   | Name of the software as shown in Programs and Features         | Registry    |
| DisplayVersion    | string   | Version of the software                                        | Registry    |
| InstallDate       | DateTime | Date the software was installed                                | Registry    |
| Is64Bit           | bool     | Indicates whether the software is 64-bit                       | Registry    |
| IsSystemComponent | bool     | Indicates if the software is marked as a system component      | Registry    |
| ProductID         | string   | Unique identifier for the product (e.g., registry subkey path) | Registry    |
| Publisher         | string   | Name of the software publisher                                 | Registry    |

## UpdateCompliance <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Uinv 104 <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

| Name        | Type   | Description                               | Data Source                     |
| ----------- | ------ | ----------------------------------------- | ------------------------------- |
| PackageID   | string | Unique identifier for the update package  | Update Catalog                  |
| Name        | string | Name of the update                        | Update Catalog                  |
| IsInstalled | bool   | Indicates whether the update is installed | FileSystem/Registry/WMI/Win API |

## UpdateComplianceSummary <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Uinv 104 <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

| Name               | Type | Description                                            | Data Source        |
| ------------------ | ---- | ------------------------------------------------------ | ------------------ |
| MuInstalled        | int  | Number of Microsoft Updates installed                  | Windows Update API |
| MuRequired         | int  | Number of Microsoft Updates required                   | Windows Update API |
| PmpcCatalogVersion | int  | Version number of the PMPC update catalog last scanned | UpdateCompliance   |
| PmpcInstalled      | int  | Number of PMPC updates installed                       | UpdateCompliance   |
| PmpcNotApplicable  | int  | Number of PMPC updates not applicable                  | UpdateCompliance   |
| PmpcRequired       | int  | Number of PMPC updates required                        | UpdateCompliance   |

## Win32\_BIOS <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Hinv 101

| Name         | Type   | Description                      | Data Source |
| ------------ | ------ | -------------------------------- | ----------- |
| BIOSVersion  | string | BIOS version (SMBIOSBIOSVersion) | WMI         |
| SerialNumber | string | Device serial number             | WMI         |

## Win32\_LogicalDisk <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Hinv 101

| Name       | Type   | Description                            | Data Source |
| ---------- | ------ | -------------------------------------- | ----------- |
| DeviceId   | string | Unique device identifier               | WMI         |
| DriveType  | string | Type of drive (e.g., Fixed, Removable) | WMI         |
| FreeSpace  | string | Available free space in bytes          | WMI         |
| Size       | string | Total size of the volume in bytes      | WMI         |
| VolumeName | string | Name of the volume                     | WMI         |

## Win32\_OperatingSystem <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Hinv 101

| Name        | Type   | Description                     | Data Source |
| ----------- | ------ | ------------------------------- | ----------- |
| Build       | string | Build number of the OS          | WMI         |
| InstallDate | string | OS installation date            | WMI         |
| Name        | string | Operating system name (caption) | WMI         |
| SKU         | string | Operating system SKU            | WMI         |
| Version     | string | OS version                      | WMI         |

## WuaMetadata <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

### Uinv 104 <a href="#user-content-f0-9f-93-81-softwareregistryentry" id="user-content-f0-9f-93-81-softwareregistryentry"></a>

| Name                 | Type   | Description                                           | Data Source        |
| -------------------- | ------ | ----------------------------------------------------- | ------------------ |
| WuaLastStatusMessage | string | Last status message from the Windows Update Agent     | Windows Update API |
| WuaLastStatusCode    | int    | Last status code returned by the Windows Update Agent | Windows Update API |
| WuaAgentVersion      | string | Version of the Windows Update Agent                   | Windows Update API |
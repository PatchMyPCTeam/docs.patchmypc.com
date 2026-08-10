# User Inventory Data Collection in Patch My PC Advanced/Patch Insights for Intune

_Applies to: Advanced/Patch Insights for Intune_

This article documents the user inventory data collected by the Patch My PC (PMPC) Advanced/Patch Insights for Intune client.

| [BrowserExtension](user-inventory-data.md#browserextension)   | [LocalGroup](user-inventory-data.md#localgroup)   | [UserApplication](user-inventory-data.md#userapplication) |
| ------------------------------------------------------------- | ------------------------------------------------- | --------------------------------------------------------- |
| [UserLogonActivity](user-inventory-data.md#userlogonactivity) | [UserProfile](user-inventory-data.md#userprofile) |                                                           |

## BrowserExtension

### Cinv 103

| Name        | Type     | Description                                       | Data Source |
| ----------- | -------- | ------------------------------------------------- | ----------- |
| Author      | string   | Publisher or author of the extension              | File system |
| Browser     | string   | Browser name (e.g., Chrome, Firefox)              | File system |
| ID          | string   | Unique extension identifier                       | File system |
| InstalledOn | DateTime | Date the extension was installed                  | File system |
| InstallPath | string   | File system path where the extension is installed | File system |
| Name        | string   | Extension display name                            | File system |
| User        | string   | User profile associated with the extension        | WMI         |
| Version     | string   | Extension version                                 | File system |

## LocalGroup

### Cinv 103

| Name                                            | Type      | Description                     | Data Source |
| ----------------------------------------------- | --------- | ------------------------------- | ----------- |
| GroupMembers                                    | string\[] | List of members that are Groups | WinAPI      |
| GroupName<mark style="color:red;">**\***</mark> | string    | Name of the local group         | WinAPI      |
| Members                                         | string\[] | List of members that are users  | WinAPI      |

<mark style="color:red;">**\***</mark> Only the **Administrators** group is currently supported. All other groups are excluded and no information is collected from Domain Controllers.

## UserApplication

### Cinv 103

| Name                                               | Type   | Description                                                   | Data Source          |
| -------------------------------------------------- | ------ | ------------------------------------------------------------- | -------------------- |
| DisplayName                                        | string | User-friendly application name                                | Registry             |
| DisplayVersion                                     | string | Application version string                                    | Registry             |
| InstallDate                                        | string | Date application was installed (often in YYYYMMDD or similar) | Registry/File system |
| InstallLocation                                    | string | File system path where the app is installed                   | Registry/File system |
| Publisher                                          | string | Name of the software publisher                                | Registry             |
| QuietUninstallString                               | string | Command line string for silent uninstall                      | Registry             |
| RegistryPath<mark style="color:red;">**\***</mark> | string | Registry key path for the application entry                   | Registry             |
| UninstallString                                    | string | Command line string for uninstall                             | Registry             |
| User                                               | string | User associated with the installation                         | WMI                  |

<mark style="color:red;">**\***</mark> Read from user registry hives, which are loaded if required.

## UserLogonActivity

### Cinv 103

| Name          | Type   | Description                                      | Data Source         |
| ------------- | ------ | ------------------------------------------------ | ------------------- |
| LastLogonUser | string | The username (or SID) of the last logged-in user | Win32API / Registry |

## UserProfile

### Cinv 103

| Name                | Type   | Description                                      | Data Source |
| ------------------- | ------ | ------------------------------------------------ | ----------- |
| FriendlyName        | string | User-friendly display name of the profile        | LDAP        |
| IsLoaded            | string | Indicates if the profile is currently loaded     | WMI         |
| ProfilePath         | string | File system path to the user’s profile directory | WMI         |
| RegistryDatFilePath | string |                                                  | File system |
| Sid                 | string | Security Identifier for the user profile         | WMI         |

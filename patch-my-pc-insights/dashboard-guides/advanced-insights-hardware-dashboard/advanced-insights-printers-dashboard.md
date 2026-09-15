---
description: 'Applies to: Patch My PC Advanced Insights for Configuration Manager'
---

# Advanced Insights "Printers" Dashboard

{% hint style="info" %}
The Printers dashboard relies on printer inventory collected by the **Advanced Insights Inventory Extensions** (the custom PMPC\_PRINTER hardware inventory class). Devices only appear here once they have run a hardware inventory cycle that includes this class, so newly deployed clients may take a hardware inventory cycle to show up.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (1106).png" alt=""><figcaption></figcaption></figure>

The dashboard shows which printers are installed across your estate and which devices they are installed on. Both panels are scoped by the **collection selector** at the bottom of each panel (for example, _All Desktop and Server Clients_) and are further limited by your Role-Based Access Control (RBAC) scope.

To keep the data meaningful, both panels exclude:

* Terminal Services / Remote Desktop **redirected** printers (printers that follow a remote session rather than being installed on the device).
* Server-hosted **shared print queues**, so the focus stays on printers installed on client devices.

### Installed Printers

This panel lists each unique printer, identified by its **driver name**, together with the number of devices it is installed on:

| Column               | Description                                                                                        |
| -------------------- | -------------------------------------------------------------------------------------------------- |
| **InstalledPrinter** | The printer driver name (the trailing "Class Driver" text is trimmed for readability).             |
| **InstalledOn**      | The number of distinct client devices in the selected collection that have this printer installed. |

Use this panel to understand which printer models and drivers are in use, and how widely each is deployed, useful when planning driver updates or retiring a print device. Clicking a printer drills through to the **Printer Installations** list filtered to just that driver.

### Printer Installations

This panel is a device-level list of every printer installation in the selected collection:

| Column                  | Description                                                                                                                                                                                    |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ComputerName**        | The client device (with an online/offline indicator).                                                                                                                                          |
| **UserName**            | The primary or top console user of the device.                                                                                                                                                 |
| **Manufacturer0**       | The printer manufacturer.                                                                                                                                                                      |
| **PrinterByDriverName** | The printer driver name.                                                                                                                                                                       |
| **Port**                | The port the printer uses. Local ports such as `LPT1:` and `USB` are shown as-is; anything else is grouped as `Other`.                                                                         |
| **IsShared**            | Whether the printer is shared from this device.                                                                                                                                                |
| **ConnectionVia**       | How the device reaches the printer — the print server's short name for a network printer, `Local` for a directly attached (LPT/USB) printer, or `Network/Other` where it cannot be determined. |

You can quick-search, sort, filter, page and export both panels. Clicking a row opens the affected device.

### Per-device view

<figure><img src="../../../.gitbook/assets/image (1107).png" alt=""><figcaption></figcaption></figure>

Opening a device and selecting **Hardware → Printers** shows the printers connected to that individual device, including the manufacturer, driver name, port, whether the printer is shared, its share name and how the device connects to it.

### Related data sources

For administrators who want to trace the dashboard back to source, it is built from:

* Printer inventory – the custom v\_GS\_PMPC\_PRINTER hardware inventory view (populated by the Advanced Insights Inventory Extensions).
* Device, online status and user data – fn\_rbac\_R\_System, BGB\_ResStatus and v\_GS\_SYSTEM\_CONSOLE\_USAGE\_MAXGROUP.

All figures are limited by the selected collection and by your RBAC scope, so two administrators may see different results for the same collection if their permitted scopes differ.

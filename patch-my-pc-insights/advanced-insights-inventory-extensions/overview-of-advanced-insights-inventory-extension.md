---
description: Technical detail for the Inventory Extensions
---

# Overview of Advanced Insights Inventory Extension

_Applies to: Patch My PC Advanced Insights_

## Inventory Extensions Process Visualized

![](/_images/WMI-(1).png)

## What is the Inventory Extensions MSI?

The Inventory Extensions MSI is a .NET **WMI Provider**. This provider code is loaded by the **WMI Service** on Windows clients. The provider returns data that the client processes into a hardware inventory report where it is then submitted to the ConfigMgr site server and entered into the SQL database.

## What is WMI?

**WMI** stands for **Windows Management Instrumentation**. It is a set of specifications from Microsoft for consolidating the management of devices and applications in a network from Windows-based systems. WMI provides a standardized way for systems administrators to manage and query information about their systems.

The heart of **WMI** is the **WMI Service**, known as `Winmgmt` and part of the Windows OS, this service runs in the background on all Windows systems. This service acts as a broker between **WMI Clients** (ConfigMgr client) and the **WMI Providers** (Inventory Extensions MSI) that deliver the actual data.

## How does this integrate with ConfigMgr?

ConfigMgr's existing hardware inventory data is collected from **WMI**. We simply extend ConfigMgr's default hardware inventory policy with the new definitions of our Inventory Extensions data. This allows the ConfigMgr clients to query our **WMI Provider** through the **WMI Service** during its normal hardware inventory task - just like it would for any existing hardware inventory class.

For this reason **we do not consider the Inventory Extensions MSI as an "Agent"**. We do not install any services on clients, instead the existing WMI Service brokers the connection between our Inventory Extension MSI code and the ConfigMgr client for us. The only time this code runs on clients is during a Hardware Inventory task or when a custom client action is invoked, after which the **WMI Service** handles the unloading of our **WMI Provider**.
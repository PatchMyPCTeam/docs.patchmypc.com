# Show Applicability Rules

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: Product_\
_&#x41;vailable on tab: Updates_

## Overview

The **Show Applicability Rules** option displays the detection and applicability logic defined in the Patch My PC catalog for the selected WSUS update.

![Show Applicability Rules](/_images/image-(78 "Show Applicability Rules") (1).png>)

This view allows you to review the rules used to determine whether a software update is applicable, installed, or required on a client device. The rules shown are read directly from the catalog metadata and represent the same logic that is published to WSUS.

> \*\*Note\*\*
>
> This option is informational only. The applicability rules cannot be edited from this window. However, the XML content can be selected and copied to the clipboard for review or analysis.

When you select **Show Applicability Rules**, a window opens displaying the following sections for the selected update.

![Applpicability Rules](/_images/image-(79 "Applpicability Rules") (1).png>)

* **Update Title**\
  Displays the full update name as defined in the catalog.
* **Is Installed Rule**\
  Defines the logic used to determine whether the update is already installed on a device.
* **Is Installable Rule**\
  Defines the logic used to determine whether the update is applicable and can be installed on a device.

## SDP Rule Structure

The applicability rules displayed in this window are stored within the Software Distribution Package (SDP) metadata that is published to WSUS. The SDP contains the logical applicability rules that WSUS distributes to clients as part of the update metadata.

When an update is published, these rules are embedded in the update definition and synchronized to WSUS. During a scan cycle, the Windows Update Agent evaluates the SDP rule logic locally on each client device. WSUS itself does not execute the detection logic. Instead, it stores and distributes the metadata, while the client performs the actual rule evaluation.

The XML elements shown in the Show Applicability Rules window represent the exact logic that is packaged in the SDP and interpreted by the Windows Update Agent to determine whether the update is Installed, Required, or Not Applicable.

### Understanding the Rule Structure

The XML structure defines how conditions are evaluated on the client. The `lar` prefix represents logical applicability rules:

* **lar:And**\
  All enclosed conditions must evaluate to true.
* **lar:Or**\
  At least one enclosed condition must evaluate to true.
* **lar:Not**\
  The enclosed condition must evaluate to false.

The `bar` prefix represents basic applicability rules, such as registry, file, or version checks:

* **bar:RegKeyLoop**\
  Iterates through registry keys, such as Uninstall.
* **bar:RegSz**\
  Checks a string registry value such as DisplayName.
* **bar:RegDword**\
  Checks a numeric registry value.
* **bar:RegSzToVersion**\
  Compares a registry string value as a version number.
* **bar:RegValueExists**\
  Validates that a specific registry value exists.

These elements are combined to build the full compliance logic.

### Example: Google Earth Pro Applicability Logic Explained

The example below shows the applicability logic (Is Installable Rule) for Google Earth Pro x64.

![Applicability Rules Explained](/_images/image-(80 "Applicability Rules Explained") (1).png>)

* The rule uses `bar:RegKeyLoop` to iterate through all subkeys under `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall.`
* The attribute `TrueIf="Any"` means the rule evaluates to true if any single uninstall entry matches the conditions inside the loop.
* Inside the loop, a logical `lar:And` container is used. This means both conditions must be true for a match.
* First condition `RegSzToVersion Comparison="LessThan" Data="7.3.6.10441"` means the DisplayVersion value of the uninstall entry must be less than 7.3.6.10441.
* Second condition `RegSz Comparison="EqualTo" Data="Google Earth Pro"` means the DisplayName value must exactly equal Google Earth Pro.

In practical terms, the rule checks whether:

* Google Earth Pro is installed, and
* The installed version is lower/older than 7.3.6.10441.

If both conditions are met for any uninstall registry entry, the rule evaluates to true and the update is considered required and in WSUS terms **Not Compliant**.

If Google Earth Pro is not found, or the installed version is equal to or greater than 7.3.6.10441, the rule evaluates to false and the update is not required and in WSUS terms **Not Applicable**.
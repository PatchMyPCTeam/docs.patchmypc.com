# Release notes for the Patch My PC Return on Investment Tool

_Applies to: Patch My PC Return on Investment Tool_

## 1.9.0 - 2025-04-28

* Pressing Ctrl+D will now enable debug mode and output a log at your %TEMP% directory.
* Fixed an issue where a single null entry in SMS\_G\_System\_INSTALLED\_SOFTWARE class prevented fallback to the add/remove program classes during ConfigMgr Scan.
* Updated dependencies.

## 1.8.0 - 2025-02-19

* Improved device count query
* Updated dependencies

## 1.7.0 - 2025-01-02

* Change to quote calculation
* Updated dependencies

## 1.6.0 - 2024-11-12

* Now displays environment device count
* Small clarification on scan results
* Updated dependencies

## 1.5.0 - 2024-10-18

* Export now supports csv
* Duplicates removed from scan results
* Updated dependencies

## 1.4.0 - 2024-06-11

* Now targeting .NET 4.6.2 for better compatibility
* Updated dependencies

## 1.3.0 - 2024-05-13

* UI stays responsive while scanning
* Minor bug fix where manual stats wont update after a failed ConfigMgr Scan
* Window is now resizable
* More data in the PDF report

## 1.2.1 - 2024-04-08

* Fixed breaking change to device count Graph API query

## 1.2.0 - 2024-02-26

* PDF export option added

## 1.1.0 - 2024-01-29

* Fixed Intune device count bug
* Added tool-tips

## 1.0.4 - 2023-12-06

* Improved Intune scan reliability

## 1.0.3 - 2023-11-28

* Bug fix for null ARP DisplayName Entries.

## 1.0.2 - 2023-11-24

* Bug fix for handling null data returned in Intune scan.

## 1.0.1 - 2023-11-13

* Initial release
# Pause Product option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_\
_&#x4C;imited to SKU: Enterprise Plus, Enterprise Premium, MSP, MSP+_

The **Pause Product** right-click option in Patch My PC (PMPC) Publisher allows you to temporarily stop publishing new application versions or updates for a specific product until a selected date.

This is commonly used to enforce short-term change control or freeze periods.

When a product is paused, Publisher skips any new versions released before the selected resume date during synchronization. The currently published version remains unchanged.

## Behavior

In the example scenario, **Google Chrome (EXE x64)** is paused until **24th June 2026**. If one or more new versions are released during the pause period, they are not published by Publisher.

!['Pause Product Updates' dialog](../../../.gitbook/assets/image-\(4413\).png)

Once the pause period expires, Publisher resumes normal behavior. The next version available after the pause ends will be published. If no new version is available when the pause expires, and the current version is already published, no action is taken.

If a product is paused and a new version is detected, the configured **Alerts** will notify you that the product is currently paused.

## Alerts

When a paused product has a newer version available, Publisher does not publish the update. Instead, the configured Alerts can notify you that the product is paused.

The notification includes the product name, resume date, update classification, and severity.

Email reports show the paused product under **Paused ConfigMgr Applications** or the equivalent paused product section for the publishing target. Webhook notifications show the same pause information in a card format.

![Email alert for paused products](../../../.gitbook/assets/image-\(4362\).png)

![Webhook alert for paused products](../../../.gitbook/assets/image-\(4363\).png)

## Limitations and guidance

A product can be paused for up to 6 months.

If your long-term goal is to stop publishing new versions of a product entirely, you should deselect the product rather than using the **Pause Product** option.

The **Pause Product** feature is intended for short, temporary freeze windows (such as year-end change control periods), where updates must be prevented for a limited time.

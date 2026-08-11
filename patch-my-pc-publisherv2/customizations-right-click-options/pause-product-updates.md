# Pause Product Updates

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: Product_\
_Available on tab: Updates, ConfigMgr Apps, Intune Apps, Intune Updates_\
_Limited to SKU: Enterprise Plus, Enterprise Premium, MSP, MSP+_

## Overview

The **Pause Product Updates** option allows you to temporarily stop publishing new application versions or updates for a specific product until a selected date. This is commonly used to enforce short term change control or freeze periods.

<figure><img src="../../.gitbook/assets/image (155).png" alt="Pause Product Updates" width="521"><figcaption></figcaption></figure>

When a product is paused, any new versions released before the selected resume date are skipped when the Publisher performs a synchronization. The currently published version remains unchanged.

## Behavior

In the example scenario, **Google Chrome (EXE x64)** is paused until **4th March 2026**. If one or more new versions are released during the pause period, they are not published by the Publisher.

<figure><img src="../../.gitbook/assets/image (156).png" alt="" width="300"><figcaption></figcaption></figure>

Once the pause period expires, the Publisher resumes normal behavior. The next new version that becomes available after the pause ends will be published. If no new version is available when the pause expires and the current version is already published, no action is taken.

If a product is paused and a new version is detected, the configured **Alerts** will notify you that the product is currently paused.

## Alerts

When a paused product has a newer version available, the Publisher does not publish the update. Instead, the configured Alerts can notify you that the product is paused.

The notification includes the product name, the resume date, the update classification and the severity.

Email reports show the paused product under **Paused ConfigMgr Applications** or the equivalent paused product section for the publishing target. Webhook notifications show the same pause information in a card format.

<figure><img src="../../.gitbook/assets/image (4362).png" alt="Email alert for paused products" width="563"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4363).png" alt="Webhook alert for paused products" width="525"><figcaption></figcaption></figure>

## Limitations and guidance

A product can only be paused for a maximum of **6 months**.

If your long term goal is to stop publishing newer versions of a product entirely, you should unselect the product instead of using the pause option. The pause feature is intended for short, temporary, freeze windows such as year end change control periods where updates must be prevented for a limited time.

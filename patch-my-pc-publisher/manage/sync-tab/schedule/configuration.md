# Configuration in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Configuration** tab of the **Sync** tab of Patch My PC (PMPC) Publisher allows you to configure options that apply to every Sync Schedule.

{% hint style="info" %}
**Note**

&#x20;This tab replaces the **ConfigMgr SUP Sync Options** tab available in previous releases of Publisher.
{% endhint %}

## To open the Configuration tab

Navigate to **Sync** | **Configuration.**

<figure><img src="../../../../.gitbook/assets/image (1603).png" alt="Configuration tab" width="563"><figcaption></figcaption></figure>

This tab consists of the following sections:

* [Sync Priority](configuration.md#sync-priority)
* [ConfigMgr SUP Sync Options](configuration.md#configmgr-sup-sync-options)
* [Report settings](configuration.md#report-settings)
* [Sync Status](configuration.md#sync-status)

## Sync Priority

The **Sync Priority** section contains the **Prioritize updates when publishing** option. When this option is enabled (which is disabled by default), you can configure minimum thresholds for both the severity and CVE count for updates. Any updates meeting either threshold are published first on every target device, ordered by severity, then CVE count.

<figure><img src="../../../../.gitbook/assets/image (1296).png" alt=""><figcaption></figcaption></figure>

### To enable Sync Priority

1. Navigate to **Sync | Configuration**.
2. Enable the **Prioritize updates when publishing** option.
3. From the **Minimum severity** dropdown, select the required severity.
4. From the **Minimum CVE count** dropdown, select the required count.
5. Save your settings.

**Sync Priority** changes the publishing order. It does not add products to a sync. To create a Sync Schedule that publishes only these updates, enable the **Only priority updates** target for the relevant Sync Schedule.

## ConfigMgr SUP Sync Options

The **ConfigMgr SUP Sync Options** section contains the **Trigger ConfigMgr SUP Sync after publishing** option.

<figure><img src="../../../../.gitbook/assets/image (1290).png" alt="&#x27;ConfigMgr SUP Sync Options&#x27; section" width="563"><figcaption></figcaption></figure>

When this option is enabled, Publisher triggers a ConfigMgr Software Update Point (SUP) sync after new third-party updates are published. This ensures that newly published updates become available in ConfigMgr as soon as possible, without waiting for the next scheduled SUP sync.

{% hint style="danger" %}
**Important**

Before you can use this option, you need to [configure the SMS Provider connection](../../configmgr-apps-tab/base-install-options/connection-source.md#configure-sms-provider-connection).
{% endhint %}

## Report settings

The **Report settings** section lets you configure the **Sync report cadence** to control when Publisher sends sync report emails.

<figure><img src="../../../../.gitbook/assets/image (1604).png" alt="Report settings" width="563"><figcaption></figcaption></figure>

The available options are:

* **Per sync (default)**\
  Sends a report after each sync.
* **Daily digest**\
  Collects the results of each day's syncs and sends one report after the last sync of the day. If the email fails, Publisher tries again later.

{% hint style="info" %}
**Note**

Sync reports use the email settings on the [Alerts](../../alerts-tab/) tab. Configure email settings there before you change the cadence.
{% endhint %}

## Sync Status

{% hint style="info" %}
**Note**

See [Sync Status section of Patch My PC Publisher](sync-status.md) for more information.
{% endhint %}

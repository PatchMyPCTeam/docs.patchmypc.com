# ConfigMgr SUP Sync Options section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **ConfigMgr SUP Sync Options** section on the **Sync Schedule** tab in Patch My PC (PMPC) Publisher contains the **Trigger ConfigMgr SUP Sync after publishing** option.

<figure><img src="../../../.gitbook/assets/image (4863).png" alt="&#x27;ConfigMgr SUP Sync Options&#x27; section" width="563"><figcaption></figcaption></figure>

When enabled, Publisher triggers a ConfigMgr Software Update Point (SUP) sync after new third-party updates are published. This ensures that newly published updates become available in ConfigMgr as soon as possible, without waiting for the next scheduled SUP sync.

{% hint style="danger" %}
**Important**

Before you can use enable this option, you need to [configure the SMS Provider connection](../configmgr-apps-tab/base-install-options/connection-source-options.md#configure-sms-provider-connection).
{% endhint %}

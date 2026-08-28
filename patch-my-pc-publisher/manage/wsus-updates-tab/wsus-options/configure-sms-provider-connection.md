# Configure SMS Provider Connection section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The SMS Provider is the interface that enables all interactions with Microsoft ConfigMgr, including actions performed in the ConfigMgr console and through supported APIs.

Patch My PC (PMPC) Publisher also relies on the SMS Provider to perform operations such as triggering SUP synchronizations, creating and modifying applications, and distributing content.

<figure><img src="../../../../.gitbook/assets/image (782).png" alt="Configure SMS Provider Connection" width="563"><figcaption></figcaption></figure>

The SMS Provider configuration is shared across the Publisher. When you configure the SMS Provider from **WSUS Updates | WSUS Options**, the same settings are automatically used in other areas of the product, including **ConfigMgr Apps | Base Install Options** and the **Sync Schedule** tab.

{% hint style="info" %}
**Note**

See [Configure the SMS Provider Connection](../../../technical-references/configure-sms-provider.md) for information on how to configure the SMS Provider connection.
{% endhint %}

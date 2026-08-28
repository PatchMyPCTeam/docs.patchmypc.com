# Configure SMS Provider Connection section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The _SMS Provider_ is the interface that enables all interactions with Microsoft ConfigMgr, including actions performed in the ConfigMgr console and through supported APIs.

Patch My PC (PMPC) Publisher also relies on the SMS Provider to perform operations such as triggering Software Update Point (SUP) synchronizations, creating and modifying applications, and distributing content.

The **Configure SMS Provider Connection** section on the **WSUS Options** tab lets you configure the SMS Provider Connection.

<figure><img src="../../../../.gitbook/assets/image (782).png" alt="Configure SMS Provider Connection" width="563"><figcaption></figcaption></figure>

As the SMS Provider configuration is shared across Publisher, when you configure the SMS Provider from any of the following locations, the same settings are automatically used in other areas of Publisher:

* **WSUS Updates | WSUS Options**
* **ConfigMgr Apps | Base Install Options**
* The **Sync Schedule** tab.

{% hint style="info" %}
**Note**

See [Configure the SMS Provider Connection](../../../technical-references/configure-sms-provider.md) for information on how to configure the SMS Provider connection.
{% endhint %}

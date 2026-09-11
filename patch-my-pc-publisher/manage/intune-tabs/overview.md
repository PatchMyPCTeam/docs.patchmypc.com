# Overview of the Intune Apps and Intune Updates tabs in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Intune Apps** and **Intune Updates** tabs in Patch My PC (PMPC) Publisher let you select which third-party applications and updates to publish to Intune. Products enabled here determine which third-party applications and updates Publisher publishes and maintains in your environment.

Third-party applications _and_ updates appear in the **All Apps** node in the Intune Admin Center.

<figure><img src="../../../.gitbook/assets/image (729).png" alt="Applications and Updates appear in the All Apps view in the Intune Admin Center" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

You can configure additional behavior related to application and update publishing from the [Intune Options](intune-options/) tab on either the **Intune Apps** or **Intune Updates** tabs.
{% endhint %}

## Differences between Intune Apps and Intune Updates

Products on both the **Intune Apps** and **Intune Updates** tabs are published as Win32 apps and use the same core detection method to determine installation state. The key difference is how they handle applicability.

_Intune Apps_ are designed for initial installation and lifecycle management. They generally apply to any targeted device unless assignment filters or requirements restrict them.

_Intune Updates_ (while still Win32 apps) include an additional requirement script. This script evaluates whether an older version of the app is already installed on the device. The update Win32 app is considered applicable only if it detects a previous version. This ensures that updates target existing installations rather than installing new apps.

Because Intune does not have a native compliance evaluation model like WSUS, this requirement uses script-based logic to simulate update applicability while remaining fully integrated with the native Intune Win32 application model.

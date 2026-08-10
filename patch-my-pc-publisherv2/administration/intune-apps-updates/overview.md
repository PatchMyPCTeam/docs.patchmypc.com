# Overview

_Applies to: Patch My PC Publisher V2.x_

The **Intune Apps** and **Intune Updates** tabs are where you select which third-party applications and updates should be published to Intune. Products enabled here determine which third-party applications and updates the Publisher will publish and maintain within your environment.

![Intune Apps and Intune Updates Tab Overview](/_images/image-(366).png "Intune Apps and Intune Updates Tab Overview")

Third-party applications _and_ updates appear in the **All Apps** node in the Intune Admin Center.

![Applications and Updates appear in the All Apps view in the Intune Admin Center](/_images/image-(365).png "Applications and Updates appear in the All Apps view in the Intune Admin Center")

Additional behavior related to application and update publishing can be configured using the [**Options**](options/) button on the either the Intune Apps or Intune Updates tabs.

### Difference Between Intune Apps and Intune Updates

Products on both the Intune Apps and Intune Updates tabs are published as Win32 apps and use the same core detection method to determine installation state. The key difference is how applicability is handled.

Intune Apps are designed for initial installation and lifecycle management. They are generally applicable to any targeted device unless restricted by assignment filters or requirements.

Intune Updates, while still Win32 apps, include an additional requirement script. This script evaluates whether an older version of the application is already installed on the device. The update Win32 app is only considered applicable if a previous version is detected. This approach ensures that updates target existing installations rather than installing new applications.

Because Intune does not have a native compliance evaluation model like WSUS, this requirement script based logic is used to simulate update applicability while remaining fully integrated with the native Intune Win32 application model.
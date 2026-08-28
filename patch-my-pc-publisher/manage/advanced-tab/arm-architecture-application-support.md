# ARM Architecture Application Support section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **ARM Architecture Application Support** section on the **Advanced** tab of Patch My PC (PMPC) Publisher controls whether Publisher evaluates and publishes ARM64 applications.

<figure><img src="../../../.gitbook/assets/image (744).png" alt="&#x27;ARM Architecture Application Support&#x27; section" width="563"><figcaption></figcaption></figure>

## Enable support for ARM Architecture applications

When this option is enabled, Publisher prompts you to confirm.

<figure><img src="../../../.gitbook/assets/image (745).png" alt="Confirmation you want to enable ARM support" width="461"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

Once enabled, this setting cannot be disabled.
{% endhint %}

Once enabled, Publisher begins supporting ARM64 applications. ARM64 products are evaluated during Publisher syncs using existing auto-publishing rules.

Enabling this option causes ARM64 applications to be included in evaluation and publishing logic. Existing auto publishing rules are applied without modification, which may result in new ARM64 applications being published automatically.

Because the setting is permanent, it should be enabled only after confirming that ARM64 application support is required in the environment.

## ARM64 Application Naming

When ARM Architecture Application Support is enabled, ARM based applications are shown alongside existing products in the Publisher product tree(s) on the following tabs:

* Updates
* ConfigMgr Apps
* Intune Apps
* Intune Updates

ARM applications are identified by **ARM64** appended to the application name. This naming clearly distinguishes ARM64 installers from x64 and x86 variants.

<figure><img src="../../../.gitbook/assets/image (746).png" alt="ARM64 Products in the Product Tree" width="259"><figcaption></figcaption></figure>

## Automatic Requirement Handling

For third party updates published to WSUS, ARM64 applicability is controlled by a well known detectoid defined in the Patch My PC catalog SDP. This detectoid limits the update so it is only applicable to supported architectures.

```xml
<sdp:Prerequisites>
  <sdp:AtLeastOne>
    <sdp:PackageID>4103af66-247a-4782-b970-8899394c27c3</sdp:PackageID>
  </sdp:AtLeastOne>
</sdp:Prerequisites>
```

For ConfigMgr applications, ARM64 applications automatically include an operating system requirement that limits installation to Windows ARM64. This ensures the application is only offered to supported devices.

<figure><img src="../../../.gitbook/assets/image (172).png" alt="ConfigMgr OS Requirements" width="563"><figcaption></figcaption></figure>

For Intune Win32 applications, the operating system architecture requirements are automatically configured during publishing. ARM64 applications are limited to ARM64 devices, while most x64 applications are allowed to install on both x64 and ARM64 devices.

<figure><img src="../../../.gitbook/assets/image (173).png" alt="Intune OS Requirements" width="563"><figcaption></figcaption></figure>

## Assignments

Architecture-specific apps may report as Installed on devices with a different architecture due to a known detection script limitation. This is a reporting issue only and does not result in any software being installed. See [ARM64 update may show as Installed on x64 devices](https://patchmypc.com/kb/arm64-update-may-show-as-installed-on-x64-devices/) for details and a recommended workaround.

# Set Architecture Requirements

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: Product_\
_Available on tab: ConfigMgr Apps, Intune Apps_

## Overview

The **Set Architecture Requirements** option allows you to control which devices are eligible to install an application created by the Publisher.

When this option is used, the Publisher automatically configures operating system and architecture requirements on the application. These requirements are applied to the deployment type in ConfigMgr or to the requirement rules on the Win32 app in Intune. Only devices that meet the configured requirements are considered applicable when the application is deployed.

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3990).png" alt="Set Application Requirements" width="563"><figcaption></figcaption></figure>

This setting is commonly used to prevent applications from installing on unsupported operating systems, device types, or architectures.

## Platform Behavior

The **Set Architecture Requirements** option controls which devices are eligible to install an application based on operating system architecture and, where supported, device type. These requirements are evaluated before installation and ensure applications are only offered to supported devices.

The available requirement options and default behavior depend on the architecture of the application being published.

In ConfigMgr, requirements are applied directly to the deployment type. ConfigMgr evaluates these requirements before downloading content or starting installation. In addition to architecture based requirements, ConfigMgr also supports restricting applications to workstation or server operating systems.

<figure><img src="../../.gitbook/assets/image (3992).png" alt="Requirement set on the Deployment Type" width="563"><figcaption></figcaption></figure>

In Intune, requirements are applied as Win32 app requirement rules. Intune evaluates these rules at install time to determine device eligibility. Architecture requirements are supported, but device type restrictions such as workstation or server are not available.

<figure><img src="../../.gitbook/assets/image (3998).png" alt="Requirement set on the Win32 app" width="563"><figcaption></figcaption></figure>

## ARM64 Applications

Applications built specifically for ARM64 are created with an ARM64 suffix in the application name.

By default, ARM64 applications are configured to:

• Install on ARM64 OS.

{% hint style="info" %}
**Note**

In ConfigMgr, ARM64 applications are also restricted to workstation operating systems by default.
{% endhint %}

These requirements cannot be modified and are applied automatically to the deployment type when the application is created&#x20;

<figure><img src="../../.gitbook/assets/image (3993).png" alt="Example ConfigMgr ARM64 Application Requirements" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

For more information on how the Publisher handles ARM64 support for apps, see [ARM Architecture Application Support](../administration/advanced/arm-architecture-application-support.md).
{% endhint %}

## 64-bit Applications

For 64-bit applications, the deployment type is created with a requirement:

* &#x20;Install on 64-bit OS.

{% hint style="info" %}
**Note**

In ConfigMgr, applications can also be restricted to workstation or server operating systems.
{% endhint %}

The example below highlights how ARM64 applicability can differ between 64-bit applications based on catalog testing and support validation.

In the Google Chrome example, the application is configured to install on 64-bit operating systems only.

In contrast, the Notepad++ example shows both Install on 64-bit OS and Install on ARM64 OS selected. This indicates that the 64-bit Notepad++ application has been validated to run correctly on ARM64 devices and is therefore permitted to install on both x64 and ARM64 operating systems.

<figure><img src="../../.gitbook/assets/image (3996).png" alt="64-bit and ARM64 Requirement" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

These variances across 64-bit applications are intentional and are determined by the Patch My PC catalog team during application testing. ARM64 support is enabled only when it is considered appropriate for the specific application to avoid installation failures on unsupported devices.
{% endhint %}

For applications where **Install on ARM64 OS** is not enabled by default, you can optionally enable it if the application is known to support ARM64 execution. When you attempt to enable this option, you are prompted for confirmation to ensure the change is intentional.

<figure><img src="../../.gitbook/assets/image (3995).png" alt="Confirm ARM64 OS Requirement" width="449"><figcaption></figcaption></figure>

You can also restrict installation to workstation or server operating systems as needed.

## 32-bit Applications

For standard 32-bit (x86) applications, the deployment type is created with requirements to:

• Install on 32-bit OS\
• Install on 64-bit OS\
• Install on ARM64 OS

{% hint style="info" %}
**Note**

In ConfigMgr, applications can also be restricted to workstation or server operating systems.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (3997).png" alt="32-bit Application Requirements" width="375"><figcaption></figcaption></figure>

This reflects the Windows compatibility model, where 32-bit applications can generally run on all supported Windows architectures.

Optional restrictions can be applied to limit installation to workstations or servers only.&#x20;




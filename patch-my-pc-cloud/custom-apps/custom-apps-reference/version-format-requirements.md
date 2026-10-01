# Version Format Requirements for Patch My PC Cloud Custom Apps

_Applies to: Patch My PC Cloud Custom Apps_

When creating a Patch My PC (PMPC) Custom App, the **Version** field must use a version format compatible with the .NET **System.Version** format.

Failing to follow this format will result in the following error:

`Please enter a series of numbers separated by periods (e.g., X.X, X.X.X, or X.X.X.X)`

<figure><img src="../../../.gitbook/assets/image (1226).png" alt="" width="563"><figcaption></figcaption></figure>

The version must contain numeric segments separated by periods (**.**) and can contain a maximum of four segments:

* _x.x_
* _x.x.x_
* _x.x.x.x_

For example:

* 8.0
* 8.0.0
* 8.0.0.14

{% hint style="danger" %}
**Important**

Versions that do not follow this format cannot be used when creating a Custom App.

For example, the following formats are incompatible:

* 8.0.0.14.1
* 8.0.0-beta
* 8.0.0-build14
* 2026.09.01.123.456
{% endhint %}

## Why does the Version field require this?

The **Version** field of a Custom App is used by the Cloud Portal and its automatically generated PowerShell Script detection logic as a version value. The value must therefore be compatible with the version format supported by .NET's **System.Version**.

This requirement also aligns with the version format Microsoft Intune supports for native version-based detection and applicability rules.

### Previously configured Custom Apps with non-standard version values

Previously, the Cloud Portal did not sufficiently enforce this requirement when configuring the **Version** field. As a result, it was possible to configure apps using version values that were not compatible with **System.Version**.

When these apps were subsequently evaluated using version-based detection with PMPC detection scripts, this could lead to unpredictable or incorrect detection results.

### Recommended Configuration

We recommend the following configurations:

* [If the application's actual version is compatible with System.Version, use that version directly](version-format-requirements.md#if-the-applications-actual-version-is-compatible-with-system.version-use-that-version-directly)
* [If the application's native version contains additional information that is incompatible with System.Version, use a unique, compatible four-segment version for the Custom App](version-format-requirements.md#if-the-applications-native-version-contains-additional-information-that-is-incompatible-with-system)

#### If the application's actual version is compatible with System.Version, use that version directly

For example:

Application version: 8.0.0.14\
Custom App Version: 8.0.0.14

#### If the application's native version contains additional information that is incompatible with System.Version, use a unique, compatible four-segment version for the Custom App

For example:

Application version: 8.0.0.14.123-beta\
Custom App Version: 8.0.0.14

Using a compatible version lets you create the Custom App whilst  still providing a version that can distinguish the application.

{% hint style="danger" %}
**Important**

Ensure you configure Detection Rules correctly, as relying on version-based detection to evaluate the full app version when the app's actual version does not conform to the **System.Version** format is not recommended.
{% endhint %}

After creating the Custom App:

1. Configure the Custom App using a System.Version-compatible value, such as **8.0.0.14**
2. Switch the application's detection method to [Custom Detection Rules.](../create-a-custom-app/custom-apps-detection-rules-tab.md)
3. Configure the Custom Detection Rules to accurately detect the app's actual installed state.
4. If the full app version must be evaluated, use an appropriate string-based comparison rather than a version comparison.

## Summary

The **Version** field in a Custom App must contain a System.Version-compatible value:

&#x20;        **x.x → x.x.x → x.x.x.x**

If the app's actual version contains more than four segments or does not conform to this format:

* Use a compatible version when creating the Custom App.
* Do not depend on version-based detection to evaluate the incompatible version.
* Use Custom Detection Rules for accurate detection.
* Use string-based detection when you need to evaluate the complete application version.

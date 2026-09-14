# Intune Global Options section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Intune Global Options** section on the **Advanced** tab of Patch My PC (PMPC) Publisher controls how Publisher interacts with Microsoft Intune at a global level. These settings are primarily used to support advanced scenarios such as content extraction from Intune packages and tuning Microsoft Graph query behavior for large tenants.

<figure><img src="../../../.gitbook/assets/image (742).png" alt="&#x27;Intune Global Options&#x27; section" width="563"><figcaption></figcaption></figure>

## Store encryption information locally to allow extraction of Win32 .intunewin files

Publisher can store the encryption information used when creating Intune Win32 package files with the **.intunewin** extension. When the **Store encryption information locally to allow extraction of Win32 .intunewin files** checkbox is checked, the encryption keys are retained locally and can later be used to download and extract the contents of Intune applications and updates.

This capability is required if you want to use the [Intune Manager](../intune-tabs/intune-manager.md) to extract content from apps or updates published by Publisher.

### To enable encryption key storage

1. Open Publisher.
2. Navigate to the **Advanced** tab.
3. Under the **Intune Global Options** section, check the **Store encryption information locally to allow extraction of Win32 .intunewin files** checkbox.
4. Click **Apply** or **Save and Close**.

{% hint style="danger" %}
**Important**

Encryption information is only available for apps created after you enable this option. You cannot extract content from Intune apps or updates created before you turned on the option.
{% endhint %}

Once **Store encryption information locally to allow extraction of Win32 .intunewin files** setting is enabled, you can extract content for apps and updates created _after_ the setting was turned on by using the [**Extract Package**](../intune-tabs/intune-manager.md#extract-package) feature of Intune Application Manager.

## Number of items to be returned when the Graph API returns paged results

The **Number of items to be returned when the Graph API returns paged results** setting controls how many Intune objects Publisher returns per page when it queries Microsoft Graph.

This is useful in environments with a large number of apps, updates, or assignments:

* Lower values reduce the size of each response, which can help in slow or constrained network conditions.
* Higher values reduce the number of requests required to retrieve all data, which can improve performance in well-connected environments.

The default is **100,** with values of **1** to **999** being supported

In most scenarios, the default value of **100** is recommended. Adjust this setting only if you are troubleshooting performance or scalability issues related to Graph queries.

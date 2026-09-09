# Update Republishing Options section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Update Republishing Options** section on the **WSUS Options** tab in Patch My PC (PMPC) Publisher controls how republished third party updates are named. Republishing is required when an existing update needs to be replaced due to changes in content or metadata.

<figure><img src="../../../../.gitbook/assets/image (1009).png" alt="&#x27;Update Republishing Options&#x27; section" width="563"><figcaption></figcaption></figure>

Common scenarios requiring republishing include updates where you added or modified customizations, corrected detection logic, or need to sign the update with a new code signing certificate. In general, any change that affects the update CAB file or its digital signature requires republishing the update.

{% hint style="success" %}
**Tip**

For more information on Republishing, see [Customizations](../../../customizations/).
{% endhint %}

By default, when an update is republished, Publisher appends a timestamp to the update name indicating when the republish occurred. This makes it clear in the Microsoft Configuration Manager (ConfigMgr) console that the update is a republished revision and shows the exact republish date and time. The example shown in the image above demonstrates how a republished Google Chrome update would appear with this appended information.

## Do not append republished updates with a republished datetime

If the **Do not append republished updates with a republished datetime** checkbox is checked, the republished update keeps the original update name, and no timestamp is added.&#x20;

The update is still republished and supersedes the previous revision (if that option was selected during republishing), but the name shows no visible indication that a republish occurred.

{% hint style="info" %}
**Note**

Republishing only applies to an existing update version. When an update is republished, Publisher republishes the same version and creates a new revision of that update with a new Update ID.

If an administrator attempts to republish an update and the specified version is not found, Publisher does not republish. Instead, it performs a standard publish for the newer version and treats it as a new update rather than a republished revision.
{% endhint %}

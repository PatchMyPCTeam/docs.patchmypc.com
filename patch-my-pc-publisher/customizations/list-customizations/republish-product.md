# Republish Product option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Republish Product** right-click option in Patch My PC (PMPC) Publisher instructs Publisher to rebuild and republish an update or application during the next publishing service sync.

Use this action when an item has already been published, but its content or core metadata must be rebuilt to restore functionality or add files.

Republishing recreates the underlying content rather than issuing a simple metadata change. The exact behavior depends on the target platform.

* **WSUS updates -** Republishing creates entirely new updates. They appear as separate items in WSUS and ConfigMgr, with new content paths and content hashes. By default, the update title is appended with _'Republished on date'_ to help identify republished updates.
* **ConfigMgr applications -** Republishing creates a new content version.
* **Intune apps and updates -** Republishing replaces the existing app content and metadata for the Win32 app, whilst the Win32 application ID remains the same.

{% hint style="info" %}
**Note**

See the [Update Republishing Options](../../manage/wsus-updates-tab/wsus-options/update-republishing-options.md) for more information on how to configure republished update behavior for WSUS updates.
{% endhint %}

## When to Use Republish

Use republishing only when an update or application's content must change, and you cannot resolve the issue through a normal revision or metadata-only update.

Common scenarios include:

* **WSUS content files were removed**\
  If the content for a previously published WSUS update is missing, ConfigMgr will fail to download it and return a 404 error. Republishing restores the missing content in WSUS.
* **ScriptRunner binaries must be added**\
  When you enable a feature for the first time that depends on the ScriptRunner executable for an update or application already published, you must republish the item so the required binaries are included in the content.
* **A right-click customization option modified the content**\
  Options such as adding pre- or post-scripts, attaching an MST, or enabling conflicting process management introduce additional files. As these changes alter the content itself, republishing is required so the update package or application content can be rebuilt.
* **The WSUS code signing certificate changed**\
  Previously published updates must be republished so they can be signed again using the new certificate.

## Important Intune Considerations

In many environments, deleting an existing Intune Win32 app and allowing Publisher to recreate it during the next sync can be faster than using the **Republish Product** option.

When an app is recreated, it receives a new application ID, and the Intune Management Extension evaluates it almost immediately during the next policy sync.

Republished apps keep the same application ID and are subject to the Global Re-evaluation Schedule. This schedule typically rechecks previously evaluated apps about once every 24 hours.

As a result, clients may take significantly longer to detect republished apps Vs newly created apps.

## Important WSUS Considerations

When a WSUS update is marked for republishing, Publisher displays the following confirmation dialog, reminding you that a Software Update Point sync is required before the republished update becomes available in ConfigMgr.

<figure><img src="../../../.gitbook/assets/image (975).png" alt="Republish Updates" width="482"><figcaption></figcaption></figure>

After confirmation, you are prompted to choose whether the new update should supersede the existing update in WSUS. If you choose to supersede, the older update will be marked as superseded once the new update is created.

<figure><img src="../../../.gitbook/assets/image (1000).png" alt="Supersede Previously Published Updates" width="478"><figcaption></figcaption></figure>

If you prefer older updates to be expired instead of superseded, you can use the [Modify Published Updates](../../manage/wsus-updates-tab/wsus-options/modify-published-updates.md) wizard in Publisher to manually do this.

{% hint style="danger" %}
**Important**

Avoid deleting previously published updates directly from WSUS or ConfigMgr. Doing so can cause republished updates to reappear unexpectedly and may result in hash validation errors if clients attempt to download content that no longer exists.
{% endhint %}

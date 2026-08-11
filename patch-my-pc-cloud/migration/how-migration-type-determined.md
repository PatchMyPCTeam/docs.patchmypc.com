# How Migration Type is Determined in ConfigMgr to Intune App Migration for Patch My PC Cloud

_Applies to: Patch My PC Cloud_

The _Migration_ feature of Patch My PC (PMPC) Cloud evaluates Microsoft Configuration Manager (ConfigMgr) applications using an initial full scan when the environment is first connected, followed by delta scans that run every 60 minutes by default, but can also be triggered manually.

These scans detect changes to application metadata and determine whether an application can be reliably migrated as a PMPC Catalog App, a PMPC Custom App, or is unsupported for migration.

Where possible, PMPC Cloud prefers migrating applications as catalog apps, as this ensures they can be automatically kept up to date. PMPC Cloud cannot automatically update PMPC Custom Apps when a vendor releases a new version, as Custom Apps are not tracked in the catalog.

### Option 1: Publish the App in Intune as a PMPC Catalog App

Wherever possible, we attempt to match ConfigMgr applications to an existing app in our catalog using the installer hash. When a match is found, you can deploy the catalog app to Intune instead of the version in ConfigMgr, which may be out of support or exposed to known vulnerabilities.

When we migrate ConfigMgr applications using this method, we also migrate any installation arguments, customizations, and command lines you have defined for the ConfigMgr application.

The end result is that you now have a version of the app deployed that can be managed and kept up to date for the app's lifetime.

{% hint style="info" %}
**Note**

See [Publish the App in Intune as a PMPC Catalog App](migrate-application/publish-migrated-app-catalog-app.md) for more information.
{% endhint %}

### Option 2: Publish the App in Intune as a **Suggested** PMPC Catalog App

In some cases, we cannot confidently match a ConfigMgr application to a catalog app using the installer hash alone. When this happens, we evaluate additional application metadata to determine whether a reliable catalog match can still be suggested.

This evaluation may include:

* Application display name
* Application vendor
* Installer type (for example MSI or EXE)
* Installer context (system or user).

If these indicators collectively align with a known catalog app, we may suggest migrating the application as a PMPC Catalog App even when a direct installer hash match isn’t available. This allows you to leverage our catalog-based updates while making it clear that the match is based on metadata rather than binary identification.

{% hint style="info" %}
**Note**

See [Publish the App in Intune as a Suggested PMPC Catalog App](migrate-application/publish-migrated-app-suggested-app.md) for more information.
{% endhint %}

### Option 3: Publish the App in Intune as a PMPC Custom App

For those ConfigMgr applications that we cannot find a direct match to an app in our catalog, we can still migrate them, but as a [PMPC Custom App](../custom-apps/custom-apps-overview.md).

When we migrate ConfigMgr applications using this method, we migrate the exact version and include the migration of all installation arguments, customizations, and command lines you have defined for the ConfigMgr application.

You will be able to modify and manage the app from within the PMPC Cloud Portal and take advantage of the various customizations and features of PMPC Cloud Custom Apps.

{% hint style="info" %}
**Note**

See [Publish the App in Intune as a PMPC Custom App](migrate-application/publish-migrated-app-catalog-app-1.md) for more information.
{% endhint %}

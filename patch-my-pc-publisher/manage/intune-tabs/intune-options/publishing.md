# Publishing section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **PUBLISHING** section on the **Intune Options** tab of Patch My PC (PMPC) Publisher controls how Publisher creates, updates, names, organizes, and maintains apps and updates in Intune. These settings apply globally to all apps created from the **Intune Options** tab and directly influence application lifecycle behavior.

<figure><img src="../../../../.gitbook/assets/image (1276).png" alt="&#x27;PUBLISHING&#x27; section" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

Some options in the **Intune Win32 Application Options** section are global defaults. These settings can be overridden at the Vendor or Product level within the [Product Tree](../../../fundamentals/product-tree/working.md). When a more specific customization exists at a lower level, it takes precedence over the global setting, following standard product tree inheritance behavior.
{% endhint %}

## Digitally sign the detection method script and enforce signature checking on the application in Intune

When the **Digitally sign the detection method script and enforce signature checking on the application in Intune** option is enabled, Publisher digitally signs PowerShell-based detection and requirement scripts used by Win32 apps and configures the Win32 app to require signed scripts.

Specifically, Publisher sets the **Enforce script signature check and run script silently** property on the Win32 app’s detection and/or requirement rule in Intune. This is an application-level setting and does not modify PowerShell execution policy or device security configuration.

<figure><img src="../../../../.gitbook/assets/image (3857).png" alt="Enforce script signature check" width="524"><figcaption></figcaption></figure>

This option is intended for environments that already enforce signed PowerShell scripts, such as those using an AllSigned execution policy or app control solutions like AppLocker or Windows Defender Application Control (WDAC). By signing the detection and requirement scripts and enabling signature enforcement on the app, Publisher allows them to run silently and unblocked where unsigned scripts would otherwise be blocked or require user confirmation.

### To select a code-signing certificate for signing detection and requirement scripts

1. Enable Digitally sign the detection method script and enforce signature checking on the app in Intune.
2. Click **Browse** next to **Select code-signing certificate**.
3. In the certificate selection window, choose a valid code-signing certificate from the **Local Computer – Personal** certificate store.

<figure><img src="../../../../.gitbook/assets/image (86).png" alt="Browse the Local Computer Store for a Code-Signing Certificate" width="563"><figcaption></figcaption></figure>

4. Click **OK** to confirm the certificate selection.
5. Select **OK** again to save the Intune Options.

{% hint style="info" %}
**Note**

If Publisher is also being used for WSUS or ConfigMgr publishing, it is acceptable to select the existing WSUS code-signing certificate, if present. This lets you reuse the same trusted certificate for both third-party update publishing and Intune Win32 detection and requirement script signing.
{% endhint %}

The rest of this section is split into the following two sections:

* [Application-Specific Options](publishing.md#application-specific-options)
* [Update-Specific Options](publishing.md#update-specific-options)

## Application-Specific Options

### Copy assignments from the previous release when a new application is published

When creating apps, Publisher applies any assignments that are configured within the Publisher itself. Administrators may sometimes also add or adjust assignments directly in Intune after an app has been created.

When the **Copy assignments from the previous release when a new application or update is published** option is enabled, Publisher carries forward all existing assignments from the previous app version when creating a newer version. This includes assignments configured in Publisher and assignments that were manually added in Intune.

By enabling the option, the assumption is that any assignments present on the previous app represent the administrator’s intended targeting and should continue to apply to the updated version. This ensures assignment targeting remains consistent across app updates without requiring manual reassignment.

{% hint style="info" %}
**Note**

Assignments are copied only at app creation time. Enabling this option after a newer version already exists in Intune does not apply assignments from an older version of the app, retroactively.
{% endhint %}

### Delete assignments from the previous release when a new application is published

When the **Delete assignments from the previous release when a new application is published** checkbox is checked, Publisher removes assignments from older app versions when a new version is created.

If app retention is enabled, older Win32 apps may still exist in the Intune admin center and would otherwise remain assigned. Removing assignments from the previous version ensures that only the latest version of the app is targeted to Microsoft Entra ID groups, avoiding multiple versions being deployed unnecessarily to the same devices or users.

{% hint style="info" %}
**Note**

Assignments are removed only when you create a new app. If this option is enabled after a newer version already exists in Intune, assignments are not removed retroactively.
{% endhint %}

### Copy dependencies from the previous release when a new application is published

When the **Copy dependencies from the previous release when a new application is published** option is enabled, Publisher keeps app dependencies in Intune aligned as new versions of Patch My PC apps are published.

If a Win32 app has dependencies that reference other Win32 apps created by Publisher, Publisher updates those dependency references to point to the latest published versions when a new app version is created. This ensures dependency chains remain valid and up to date without requiring administrators to manually maintain dependencies after each update.

{% hint style="danger" %}
**Important**

Apps that are part of an active dependency chain remain protected from deletion. However, once dependencies are replaced with newer versions, older apps created by Publisher that are no longer referenced may become eligible for deletion based on the app retention policy configured in Publisher.
{% endhint %}

### Copy requirements from the previous release when a new application is published

When the **Copy requirements from the previous release when a new application is published** option is enabled, any customer-defined Win32 requirement rules added to the previous app after it was initially published are copied forward and applied to future Win32 apps created by Publisher.

{% hint style="info" %}
**Note**

Requirement rules are copied forward only when you create a new app. If this option is enabled after a newer version already exists in Intune, requirements are not copied retroactively.
{% endhint %}

### Update Enrollment Status Page associations when an updated application is published

When the **Update Enrollment Status Page associations when an updated application is published** checkbox is checked, Publisher automatically updates Enrollment Status Page (ESP) app associations to reference the latest version of a Win32 app created by Publisher.

If a new version of an app is published and that app is already referenced by an ESP profile, Publisher replaces the older application version in the ESP association.

This ensures that when new devices go through Autopilot, the ESP waits for and installs the most recent version of the app, without requiring manual updates to ESP configurations after each app update.

Apps must be explicitly associated with an ESP profile using the [Product Tree](../../../fundamentals/product-tree/overview.md). This is done by right-clicking a product and selecting [Manage Enrollment Status Page](../../../customizations/list-customizations/manage-enrollment-status-page.md), where you choose which ESP configuration the application should be included in.

{% hint style="info" %}
**Note**

Updating the ESP association ensures the correct app is referenced during Autopilot, but it does not create or modify app assignments. The newly published app must still be targeted with a **Required** assignment to the devices or groups used during Autopilot.
{% endhint %}

### Enable 'Allow available uninstall'

When the **Enable 'Allow available uninstall'** option is enabled, Publisher configures Win32 apps in Intune to allow users to uninstall the app from the Company Portal when the app is assigned as **Available**.

<figure><img src="../../../../.gitbook/assets/image (3859).png" alt="Allow available uninstall" width="533"><figcaption></figcaption></figure>

### Delete any previously created applications when an updated application is published

When the **Delete any previously created applications when an updated application is published** checkbox is checked, Publisher controls how many older Win32 app versions are retained in Intune when a new version is published.

If this option is _not_ enabled, previously created app versions are never automatically removed and will continue to exist in the Intune tenant indefinitely.

Rather than being a simple on/off delete, this option works with **Retain up to&#x20;**_**x**_**&#x20;previously created applications**, where _**x**_ can be set between **0** and **10**. Publisher can track and manage up to the **10** most recent versions of an app.

* Setting the value to **0** ensures that only the latest version of the app exists in Intune.
* Setting the value to **1** or more retains that number of previous versions alongside the latest release.

Retention settings can be overridden at the vendor and product level in the [Product Tree](../../../fundamentals/product-tree/working.md), allowing more granular control. For example:

* A global default may be set to retain **1** or **2** previous versions.
* Apps with a faster release cadence, such as web browsers, may retain **3** to **5** versions.
* The maximum supported retention value is **10**.

{% hint style="danger" %}
**Important**

Publisher tracks app retention based on catalog metadata, which includes the product IDs for the most recent 10 versions of an app. This means retention and cleanup decisions can be made only for those versions that still fall within the latest 10 versions tracked by the catalog.

If older Win32 apps exist in Intune outside of the last 10 tracked versions, Publisher can no longer associate them with the product lifecycle. Even if retention is enabled, those older apps are not automatically managed or removed.

In these cases, any apps falling outside of the tracked window must be reviewed and cleaned up manually using the [Intune Manager](../intune-manager.md).
{% endhint %}

#### Retention Best Practice

As a general best practice, it is recommended to retain at least one previous version of an app.

Keeping a single previous version allows administrators to rollback if an issue is discovered after publication that was not detected during testing. In these scenarios, Win32 app supersedence can be used to roll devices back to the last known good version. Without a retained previous version in Intune, rolling back becomes significantly more difficult.

The appropriate retention value ultimately depends on your organization’s update and rollback policy.

### Delay in-place updates of previously created applications by x days

When the **Delay in-place updates of previously created applications by x days** checkbox is checked, application updates are delayed for the specified number of days after the new version is synchronized from the catalog.

* The delay is calculated from the date Publisher first detects the new version.
* This allows time for validation or testing before updating production apps.

**Example:**&#x49;f a new version is synchronized on February 3 and the delay is set to 3 days, the application will not be updated until a Publisher sync on or after February 6.

This allows time for validation or testing before updating production applications.

The delay is calculated from the date Publisher first detects the new version.

## Update-Specific Options

The following options in this section behave the same regardless of whether they apply to applications or updates. Clicking a link takes you to the relevant section:

* [Copy assignments from the previous release when a new update is published](publishing.md#copy-assignments-from-the-previous-release-when-a-new-application-is-published)
* [Delete assignments from the previous release when a new update is published](publishing.md#delete-assignments-from-the-previous-release-when-a-new-application-is-published)
* [Copy dependencies from the previous release when a new update is published](publishing.md#copy-dependencies-from-the-previous-release-when-a-new-application-is-published)
* [Copy requirements from the previous release when a new update is published](publishing.md#copy-requirements-from-the-previous-release-when-a-new-application-is-published)
* [Delete any previously created applications when an updated update is published](publishing.md#delete-any-previously-created-applications-when-an-updated-application-is-published)
* [Delay in-place updates of previously created updates by x days](publishing.md#delay-in-place-updates-of-previously-created-applications-by-x-days).


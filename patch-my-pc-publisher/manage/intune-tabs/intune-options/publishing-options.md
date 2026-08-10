# Publishing Options section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

{% hint style="danger" %}
**Important**

This article has not been updated for Version 3.x. Once it has, this banner will be removed.
{% endhint %}

The **Publishing Options** section in Patch My PC (PMPC) Publisher controls how applications are created, updated, named, organized, and maintained in Intune when using the Publisher. These settings apply globally to all applications created from the Intune Apps and Intune Options tabs and directly influence application lifecycle behavior.

<figure><img src="../../../../.gitbook/assets/image (251).png" alt="Application Options" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

Some options in the **Intune Win32 Application Options** section are global defaults. These settings can be overridden at the **vendor** or **product** level within the [product tree](../../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md). When a more specific customization exists at a lower level, it takes precedence over the global setting, following standard product tree inheritance behavior.
{% endhint %}

## Digitally sign the detection method script and enforce signature checking on the application in Intune

When the **Digitally sign the detection method script and enforce signature checking on the application in Intune** option is enabled, the Publisher digitally signs PowerShell-based detection and requirement scripts used by Win32 applications and configures the Win32 application to require signed scripts.

Specifically, the Publisher sets the **Enforce script signature check and run script silently** property on the Win32 application’s detection and/or requirement rule in Intune. This is an application-level setting and does not modify PowerShell execution policy or device security configuration.

<figure><img src="../../../../.gitbook/assets/image (3857).png" alt="Enforce script signature check" width="524"><figcaption></figcaption></figure>

This option is intended for environments that already enforce signed PowerShell scripts, such as those using an AllSigned execution policy or application control solutions like AppLocker or Windows Defender Application Control (WDAC). By signing the detection and requirement scripts and enabling signature enforcement on the application, the Publisher allows them to run silently and unblocked where unsigned scripts would otherwise be blocked or require user confirmation.

To select a code-signing certificate for signing detection and requirement scripts:

1. Enable Digitally sign the detection method script and enforce signature checking on the application in Intune.
2. Select Browse next to Select code-signing certificate.
3. In the certificate selection window, choose a valid code-signing certificate from the Local Computer – Personal certificate store.

<figure><img src="../../../../.gitbook/assets/image (86).png" alt="Browse the Local Computer Store for a Code-Signing Certificate" width="563"><figcaption></figcaption></figure>

4. Select OK to confirm the certificate selection.
5. Select OK again to save the Intune Options.

{% hint style="info" %}
**Note**

If the Publisher is also being used for WSUS or ConfigMgr publishing, it is acceptable to select the existing WSUS code-signing certificate, if present. This allows the same trusted certificate to be reused for both third-party update publishing and Intune Win32 detection and requirement script signing.

The certificate
{% endhint %}

### Copy assignments from the previous release when a new application or update is published

When creating applications, the Publisher applies any assignments that are configured within the Publisher itself. Administrators may sometimes also add or adjust assignments directly in Intune after an application has been created.

When **Copy the assignments from previously created applications when an updated application is created** is enabled, the Publisher carries forward **all existing assignments** from the previous application version when creating a newer version. This includes assignments configured in the Publisher as well as assignments that were manually added in Intune.

By enabling the option, the assumption is that any assignments present on the previous application represent the administrator’s intended targeting and should continue to apply to the updated version. This ensures assignment targeting remains consistent across application updates without requiring manual reassignment.

{% hint style="info" %}
**Note**

Assignments are copied only at application creation time. Enabling this option after a newer version already exists in Intune does not apply assignments, from an older version of the application, retroactively.
{% endhint %}

### Delete assignments from previously created applications when an updated application is created

When **Delete assignments from previously created applications when an updated application is created** is enabled, the Publisher removes assignments from older application versions when a new version is created.

If application retention is enabled, older Win32 applications may still exist in the Intune admin center and would otherwise remain assigned. Removing assignments from the previous version ensures that only the latest version of the application is targeted to Microsoft Entra ID groups, avoiding multiple versions being deployed unnecessarily to the same devices or users.

{% hint style="info" %}
**Note**

Assignments are removed only at the time a new application is created. If this option is enabled after a newer version already exists in Intune, assignments are not removed retroactively.
{% endhint %}

## Application-Specific Options

### Update Enrollment Status Page associations with new application when an updated application is created

When the **Update Enrollment Status Page associations with new application when an updated application is created** option is enabled, the Publisher automatically updates Enrollment Status Page (ESP) app associations to reference the latest version of a Win32 application created by the Publisher.

If a new version of an application is published and that application is already referenced by an ESP profile, the Publisher replaces the older application version in the ESP association.

This ensures that when new devices go through Autopilot, the Enrollment Status Page waits for and installs the most recent version of the application, without requiring manual updates to ESP configurations after each application update.

Applications must be explicitly associated with an Enrollment Status Page profile using the [product tree](../../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md). This is done by right-clicking a product and selecting [Manage ESP profiles](../../../../patch-my-pc-publisherv2/customizations-right-click-options/manage-esp-profiles.md), where you choose which ESP configuration the application should be included in. For more information on all of the available right-click customization options, see [Customizations (Right-Click Options)](../../../../patch-my-pc-publisherv2/customizations-right-click-options/).

<figure><img src="../../../../.gitbook/assets/image (258).png" alt="Manage ESP Profiles in the Product Tree" width="549"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Updating the Enrollment Status Page association ensures the correct application is referenced during Autopilot, but it does not create or modify application assignments. The newly published application must still be targeted with a Required assignment to the devices or groups used during Autopilot.
{% endhint %}

### Update application dependencies from previously created applications when an updated application is created

When **Update application dependencies from previously created applications when an updated application is created** is enabled, the Publisher keeps application dependencies in Intune aligned as new versions of Patch My PC applications are published.

If a Win32 application has dependencies that reference other Win32 applications created by the Publisher, the Publisher updates those dependency references to point to the latest published versions when a new application version is created. This ensures dependency chains remain valid and up to date without requiring administrators to manually maintain dependencies after each update.

{% hint style="danger" %}
**Important**

Applications that are part of an active dependency chain remain protected from deletion. However, once dependencies are replaced with newer versions, older applications created by the publisher, that are no longer referenced, may become eligible for deletion based on the application retention policy configured in the Publisher.
{% endhint %}

### Copy requirements from previous release when a new application or update is published

When the **Copy requirements from previous release when a new application or update is published** option is enabled, any customer-defined Win32 requirement rules added to the previous application after it was initially published are copied forward and applied to future Win32 applications created by Publisher.

{% hint style="info" %}
**Note**

Requirement rules are copied forward only when a new application is created. If this option is enabled after a newer version already exists in Intune, requirements are not copied retroactively.
{% endhint %}

### Delete any previously created applications when an updated application is published

When **Delete any previously created applications when an updated application is published** is enabled, the Publisher controls how many older Win32 application versions are retained in Intune when a new version is published.

If this option is _not_ enabled, previously created application versions are never automatically removed and will continue to exist in the Intune tenant indefinitely.

Rather than being a simple on/off delete, this option works in conjunction with **Retain up to X previously created applications**, where X can be set between 0 and 10. The Publisher can track and manage up to the **10** most recent versions of an application.<br>

* Setting the value to 0 ensures that only the latest version of the application exists in Intune.
* Setting the value to 1 or higher retains that number of previous versions alongside the latest release.

Retention settings can be overideden at the vendor and product level in the [product tree](../../../../patch-my-pc-publisherv2/administration/intune-apps-updates/product-tree.md), allowing more granular control. For example:

* A global default may be set to retain **1** or **2** previous versions.
* Applications with a faster release cadence, such as web browsers, may retain **3** to **5** versions.
* The maximum supported retention value is **10**.

{% hint style="danger" %}
**Important**

The Publisher tracks application retention based on catalog metadata, which includes the product IDs for the most recent 10 versions of an application. This means retention and cleanup decisions can be made only for those versions that still fall within the latest 10 versions tracked by the catalog.

If older Win32 applications exist in Intune that fall outside of the last 10 tracked versions, the Publisher can no longer associate them with the product lifecycle. Even if retention is enabled, those older applications are not automatically managed or removed.

In these cases, any applications that fall outside the tracked window must be reviewed and cleaned up manually using the [Intune Application Manager](../../../../patch-my-pc-publisherv2/administration/intune-apps-updates/form-controls/intune-application-manager.md).
{% endhint %}

### Retention Best Practice

As a general best practice, it is recommended to retain at least one previous version of an application.

Keeping a single previous version allows administrators to perform a rollback if an issue is discovered after publication that was not detected during testing. In these scenarios, Win32 app supersedence can be used to roll devices back to the last known good version. Without a retained previous version in Intune, rolling back becomes significantly more difficult.

The appropriate retention value ultimately depends on your organization’s update and rollback policy.

## Delete previously created updates when a new update is published

When **Delete previously created updates when a new update is published** is enabled, the Publisher applies the same retention behavior [described above for applications](publishing-options.md#delete-any-previously-created-applications-when-an-updated-application-is-published) to Intune Updates.

## Configure maximum runtime of Win32 applications to

This option sets the maximum amount of time, in minutes, that a Win32 application is allowed to run during installation in Intune.

The default value is **120 minutes**. You can change this value by using the up and down control or by entering a custom value directly in the field. The maximum supported value is **1440 minutes**.

If an installation exceeds the configured runtime, Intune marks the install as failed. The configured value is automatically applied to all Win32 applications created or updated by the Publisher.

This setting is visible on the Program tab of the Win32 application properties in the Intune admin center.

<figure><img src="../../../../.gitbook/assets/image (241).png" alt="Installation time required" width="518"><figcaption></figcaption></figure>

## Enable 'Allow available uninstall'

When **Enable "Allow available uninstall"** is enabled, the Publisher configures Win32 applications in Intune to allow users to uninstall the application from the Company Portal when the app is assigned as Available.

<figure><img src="../../../../.gitbook/assets/image (3859).png" alt="Allow available uninstall" width="533"><figcaption></figcaption></figure>

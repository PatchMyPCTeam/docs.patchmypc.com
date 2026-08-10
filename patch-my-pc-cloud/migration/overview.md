# Overview of ConfigMgr to Intune App Migration using Patch My PC Cloud

_Applies to: Patch My PC Cloud_

The _Migration_ feature of Patch My PC (PMPC) Cloud allows you to migrate applications from a Microsoft Configuration Manager (ConfigMgr) hierarchy to a PMPC Cloud company.

Rather than simply copying existing applications _as-is_, our migration experience is designed to support modernization by allowing you to move away from outdated, unsupported, or vulnerable applications and toward applications that are easier to manage and keep secure in a modern Microsoft Intune environment.

As part of the migration process, PMPC Cloud analyzes your existing ConfigMgr applications to help identify:

* Applications that are outdated or no longer supported
* Applications exposed to known Common Vulnerabilities and Exposures (CVEs)
* Opportunities to upgrade to newer, supported versions that are available in the PMPC catalog.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Migrating ConfigMgr Packages to Intune is unsupported.</p>
</blockquote>

All migrated applications benefit from additional customization and management capabilities to ensure they remain secure, maintainable, and aligned with modern desktop management practices.

## Application Migration Options

PMPC Cloud supports two methods for migrating applications from ConfigMgr to Intune.

* [PMPC Catalog App](overview.md#pmpc-catalog-app)
* [PMPC Custom App](overview.md#pmpc-custom-app)

The migration path is determined through ongoing application evaluation, not when the migration is initiated.&#x20;

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [How Migration Type Is Determined](how-migration-type-determined.md) for more information on how PMPC Cloud determines the appropriate migration path.</p>
</blockquote>

### PMPC Catalog App

Where possible, PMPC Cloud attempts to match a ConfigMgr application to an existing app in the PMPC catalog. A confident match is typically made using the hash of the main installer binary.&#x20;

When the hash isn't recognized, PMPC Cloud evaluates application metadata, such as the application title and publisher, to suggest a potential catalog match.

When an application is migrated as a catalog app, it is automatically updated and maintained over time.

### PMPC Custom App

If PMPC Cloud cannot confidently match the application to an app in the PMPC catalog, the application is migrated as a PMPC Custom App.

Custom Apps migrate the exact version, including all installation arguments and customizations, allowing the app to be managed and modified in Intune through the PMPC Cloud Portal.

Unlike applications migrated as catalog apps, PMPC Custom Apps are not automatically kept up to date and require manual updates when new versions are needed.
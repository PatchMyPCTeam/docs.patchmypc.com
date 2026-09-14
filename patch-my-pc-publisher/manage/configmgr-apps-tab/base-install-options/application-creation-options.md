# Application Creation Options section in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Application Creation Options** section on the **Base Install Options** tab of Patch My PC (PMPC) Publisher controls how applications are created, updated, named, organized, and maintained in ConfigMgr when using Publisher.

<figure><img src="../../../../.gitbook/assets/image (727).png" alt="&#x27;Application Creation Options&#x27;" width="563"><figcaption></figcaption></figure>

These settings apply globally to all applications created from the **ConfigMgr Apps** tab and directly influence application lifecycle behavior.

{% hint style="success" %}
**Tip**

Some options in the **Application Creation Options** section are global defaults. You can override these settings at the **vendor** or **product** level within the Product Tree. When a more specific customization exists at a lower level, it takes precedence over the global setting, following standard Product Tree inheritance behavior.
{% endhint %}

## Allow applications to be installed from the Install Application task sequence action

When the **Allow applications to be installed from the Install Application task sequence action** checkbox is checked, Publisher explicitly sets this flag on the application object in ConfigMgr.

Specifically, Publisher enables **Allow this application to be installed from the Install Application task sequence action without being deployed** on each application it creates or updates.

{% hint style="success" %}
**Tip**

You do not need to enable this setting when applications are explicitly referenced in a task sequence using a fixed application selection in the **Install Application** step.
{% endhint %}

{% hint style="danger" %}
**Important**

When enabled, this setting is applied _only_ when the deployment type setting, installation behavior, is set to **Install for system**. User-based applications that install in the user context do not meet the requirements for this setting.

See [Product Naming in the Patch My PC Catalog](../../../technical-references/catalog-information.md#product-naming-in-the-patch-my-pc-catalog) for more details on how to identify a user-based app.
{% endhint %}

This option should be checked &#x6F;_&#x6E;ly_ in the following scenarios:

* Applications installed using dynamic application selection in a task sequence.
* Applications are evaluated and selected at runtime, rather than being hard-coded in the task sequence.

### Policy impact and when to disable this option

Enabling the **Allow applications to be installed from the Install Application task sequence action without being deployed** setting causes ConfigMgr to generate additional application policy. This policy is distributed to clients even if the application is never used in a task sequence.

If your environment does not use variable-driven or dynamically selected application lists in task sequences, you typically don't need this option and can disable it to reduce unnecessary policy processing.

If your environment uses task sequences that install applications dynamically, such as using an Application List variable or runtime logic, leave this option enabled (it is by default) to prevent task sequence failures.

As a general guideline, enable this option only when task sequences rely on dynamic application selection. If task sequences always explicitly reference applications or deploy them normally, disabling this option helps minimize policy overhead.

## Allow clients to use distribution points from the site’s default boundary group

Checking the **Allow clients to use distribution points from the site’s default boundary group** checkbox enables a fallback behavior during application installation. If the requested application content is not available on any Distribution Point (DP) in the client’s current or neighboring boundary groups, the client is allowed to download the content from DPs belonging to the site’s default boundary group.

When enabled by Publisher, this setting applies directly to the application deployment type in ConfigMgr. It helps prevent installation failures in scenarios where boundary group coverage is incomplete or where content has not yet been distributed to all required DPs.

<figure><img src="../../../../.gitbook/assets/image (510).png" alt="Allow clients to use distribution points from the site’s default boundary group" width="476"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

While this option improves resiliency, it can result in clients downloading content from less optimal DPs, such as over slower network links, if the default boundary group contains DPs that are remote from the client's location.
{% endhint %}

## **Detection Script Code-Signing**

This section controls whether Publisher digitally signs PowerShell-based detection method scripts using the [WSUS code signing certificate](../../wsus-updates-tab/wsus-options/certificate-management/) and has three possible settings:

* **Do not code-sign detection scripts**
* **Code-sign using the WSUS Signing Certificate**
* **Code-sign using a custom certificate**

If the  **Code sign using the WSUS Signing Certificate** setting is selected (which it is by default), Publisher digitally signs PowerShell-based detection method scripts using the WSUS code signing certificate.

This ensures the detection scripts are trusted and can run successfully on clients that enforce PowerShell execution policy or script signature requirements.

This setting is applied directly to the detection method of each application deployment type created or updated by Publisher.

If you want to select a different certificate for signing detection scripts, select the **Code-sign using a custom certificate** option and configure the relevant certificate in the **Certificate** field.

## Do not include the version in the application name, so the application name doesn’t change after updates

If the **Do not include the version in the application name, so the application name doesn’t change after updates** checkbox is checked (which it is not by default), newly created applications will no longer include the version number in the application name.

This is useful when external tooling or processes reference applications by name, such as MDT UDI, UI++, or other solutions that rely on a static application name.

When this setting is disabled (the default setting), each new application version includes the version number in the name. As a result, the application name changes every time a new version is published.

When this option is enabled, the application name remains the same across versions, while the underlying content, detection logic, and deployment type are updated to reflect the latest release.

In the example below, **Notepad++ (x86)** was published with this option enabled, while **Notepad++ 8.8.9 (x64)** was published with the option disabled.

In both cases, the ConfigMgr console still shows the exact application version in the **Software Version** column.

<figure><img src="../../../../.gitbook/assets/image (513).png" alt="ConfigMgr console shows the exact application version in the Software Version column" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If you want to control application naming on a per-product basis, additional naming options are available through the [right-click customizations](../../../customizations/) menu in the Product Tree. Product-level naming options override this global setting.
{% endhint %}

{% hint style="danger" %}
**Important**

If this setting is enabled and application retention is also enabled, any retained applications will have the version number appended to their names to distinguish them from the current version.
{% endhint %}

## **Move applications to the following folder in the applications node of the console**

The **Move applications to the following folder in the applications node of the console** setting \
controls _where_ applications created or updated by Publisher are placed within the **Application Management | Applications** node of the ConfigMgr console.

When the **Move applications to the following folder in the applications node of the console** checkbox is checked and configured, Publisher automatically moves each application it creates or updates into the selected console folder. This helps keep third-party applications organized and separate from manually created or first-party applications.

### To choose where applications are placed in the ConfigMgr console

1. Load Publisher.
2. Navigate to the **ConfigMgr Apps | Base Install Options** tab.
3. Scroll down to the **Application Creation Options** section.
4. Check the **Move applications to the following folder in the applications node of the console** checkbox.
5. Click **Browse Folders**.

<figure><img src="../../../../.gitbook/assets/image (1094).png" alt="Clicking &#x27;Browse Folders&#x27;." width="563"><figcaption></figcaption></figure>

6. In the **Select Console Folder** screen, window expand the **Applications** node.
7. Select an existing folder (for example, **Applications\3rd Party Apps**), or in the **Create New Folder** field, type the name of a new folder and click **Create Folder**.
8. Click **OK** to confirm the folder selection.
9. Click **OK** again to save the ConfigMgr Apps Options.

All applications created or updated by Publisher will now be moved to the selected console folder.

{% hint style="info" %}
**Note**

The selected console folder can be overridden at the vendor or product level using the Product Tree on the **ConfigMgr Apps** tab. If a folder is defined at a lower level in the tree, that more specific setting takes precedence over this global.
{% endhint %}

## When a New Application Update is Available

The settings under **When a New Application Update is Available** section control how Publisher handles new versions of applications that were previously created by Publisher. The behavior you choose determines whether existing applications are updated in place, new applications are created, and how older versions are retained or removed.

<figure><img src="../../../../.gitbook/assets/image (1095).png" alt="&#x27;When a New Application Update is Available&#x27; section" width="563"><figcaption></figcaption></figure>

### Update existing application’s metadata, deployment type, detection method, and content files (Default)

When the **Update existing application’s metadata, deployment type, detection method, and content files** option is selected, Publisher updates an existing ConfigMgr application _in place_ rather than [creating a brand new application](application-creation-options.md#create-a-new-application-without-modifying-any-previous-applications).

This is the default option and is commonly used because the application ID does not change in ConfigMgr when we update it to the new version. By keeping the same application ID:

* Task sequences that reference the application continue to work without modification.
* Existing required and available deployments remain intact, ensuring that the latest version of the application is automatically deployed or made available in Software Center to the same device collections that targeted the previous version.

This is especially valuable for operating system deployment scenarios, where administrators want task sequences to always install the most recent version without updating references every time a new release is published.

Before performing an in-place update, Publisher validates that the application is in a healthy state. This includes confirming that:

* Publisher originally created and manages the application.
* The corresponding application content exists on disk in the content source folder.

These checks are required to safely support additional behaviors such as application retention and cleanup.

When an in-place update occurs, Publisher:

* Preserves the existing application object and application ID.
* Updates application metadata such as:
  * Software version
  * Application Name
  * Description and related metadata.
* Removes the existing Deployment Type.
* Creates a new Deployment Type and corresponding content source folder.

{% hint style="success" %}
**Tip**

Removing and recreating the deployment type results in two new revisions on the application object for each update. Over time, this causes the total number of application revisions to increase.
{% endhint %}

{% hint style="danger" %}
**Important**

In some environments using a Cloud Management Gateway (CMG), a small number of customers have historically observed issues when updating applications in place. In these cases, clients may encounter content or policy hash mismatches, where updated application policy does not consistently replicate through the CMG.

A common symptom of this behavior is an error similar to the following in **CIDownloader.log** on affected clients:

`Evaluation Failed, 0x87D00289 (-2016410999), Unknown Error`

These issues most commonly occur with applications that have multiple revisions, which can happen over time when an application is repeatedly updated in place.

If you encounter these symptoms in a CMG-enabled environment, the recommended workaround is to use **Create a new application without modifying any previous applications** instead of updating applications in place.
{% endhint %}

#### Delay the in-place application upgrade by _X_ days

When the **Delay the in-place application upgrade by&#x20;**_**X**_**&#x20;days** checkbox is checked, application updates are delayed for the specified number of days after the new version is synchronized from the catalog.

* The delay is calculated from the date Publisher first detects the new version.
* This allows time for validation or testing before updating production applications.

**Example:**\
If a new version is synchronized on February 3 and the delay is set to 3 days, the application will not be updated until a Publisher sync on or after February 6.

### Create a new application without modifying any previous applications

When the **Create a new application without modifying any previous applications** option is selected, Publisher creates a brand-new ConfigMgr application for each new version instead of updating an existing application in place. Unlike the [in-place update option](application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default), it creates a new application ID for every version.

This option is commonly used when administrators want to preserve each application version independently or avoid modifying existing application objects. It is also best suited for environments where strict version control is required, and task sequences are updated intentionally.

Because a new application is created each time:

* Task sequences that reference older application versions will continue to install those versions until they are manually updated to reference the new application.
* Existing required and available deployments remain associated only with the original application and do not automatically apply to the newly created application.

{% hint style="info" %}
**Note**

The option to **Create a new application without modifying any previous applications** can result in application sprawl over time if older versions are not cleaned up. For this reason, it is commonly used together with [application retention settings](application-creation-options.md#retain-up-to-x-previously-created-applications) to limit the number of older application versions kept in the environment.
{% endhint %}

### Retain up to x previously created applications

When checked, the **Retain up to x previously created applications** checkbox controls how many older application versions ConfigMgr retains when Publisher publishes new versions. It applies regardless of whether you choose to [**update applications in place**](application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default) or [**create a new application for each version**](application-creation-options.md#create-a-new-application-without-modifying-any-previous-applications).

Valid values range from **0** (the default) to **10**.

When this value is set to **0**, only the latest version of an application is kept in ConfigMgr. Any older versions are removed.

When this value is set to a value greater than **0**, Publisher retains that number of older application versions alongside the latest version.

For example, setting this value to **1** ensures that the environment always contains the latest application version and one previous version. This allows for quick rollback to a last known good version if needed, while preventing excessive growth in the number of applications.

{% hint style="success" %}
**Tip**

You can adjust application retention at the vendor and product levels in the [Product Tree](../../../fundamentals/product-tree/working.md), giving you more granular control and allowing you to override the configured global setting.

This option is especially useful for third-party applications with a rapid release cadence, such as web browsers. Retaining additional versions makes it easier to roll back if needed using supersedence.&#x20;

See [Supersedence](https://learn.microsoft.com/en-us/intune/configmgr/apps/deploy-use/revise-and-supersede-applications#supersedence) for more information about using supersedence in ConfigMgr.&#x20;
{% endhint %}

{% hint style="info" %}
**Note**

Publisher only tracks the ten most recent application versions during synchronization. Publisher cannot automatically clean up older application versions outside of this window through application retention. You need to review and manually remove these older versions if cleanup is required. The recommended cleanup approach is to use the [App Manager](../app-manager.md).
{% endhint %}

{% hint style="danger" %}
**Important**

Publisher will not delete an application referenced by a task sequence, even if it exceeds the retention limit and the option to delete applications with deployments is enabled.

To delete applications referenced by task sequences, remove them from the task sequence first.
{% endhint %}

#### **Behavior with update in place**

When you select the [Update existing application’s metadata, deployment type, detection method, and content files](application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default) option, application retention works by first preserving the current version before applying the update.

Before updating the application to the new version, Publisher duplicates the existing application and moves its content into a **Retained Apps** folder. Publisher then updates the application in place by removing the existing deployment type and creating a new deployment type for the latest version. This ensures the previous version is retained according to the configured retention count while the application ID remains unchanged.

If the number of applications exceeds the configured retention value, Publisher removes the oldest application versions, starting with those that fall outside the retention window.

#### **Behavior with create new application**

When the [Create a new application without modifying any previous applications](application-creation-options.md#create-a-new-application-without-modifying-any-previous-applications) option is selected, application retention is applied across the chain of independently created application objects.

Each new version is created as a separate application. If the number of applications exceeds the configured retention value, Publisher removes the oldest application versions, starting with those that fall outside the retention window.

### **Remove administrative categories from retained applications**

By default, all administrative categories assigned to a ConfigMgr application are preserved when you retain older application versions. This is useful in scenarios such as operating system deployment frontends, where administrative categories are used to populate application selection lists. The option to **Remove administrative categories from retained applications** ensures that only the current version appears in those lists, preventing outdated versions from being presented.

{% hint style="danger" %}
**Important**

The **Remove administrative categories from retained applications** checkbox is only available when the [Retain up to X previously created applications](application-creation-options.md#retain-up-to-x-previously-created-applications) setting is configured.
{% endhint %}

When checked, this option removes administrative categories from retained (older) application versions. Only the latest published application keeps the assigned administrative categories.

{% hint style="info" %}
**Note**

See [Manage Categories](../../../customizations/list-customizations/manage-categories.md) for more information about assigning categories to ConfigMgr apps.
{% endhint %}

### **Delete applications even if they have a deployment**

When the **Delete applications even if they have a deployment** checkbox is checked, Publisher can delete retained application versions even if they have existing deployments. When disabled, applications with active deployments are preserved and are not removed during retention cleanup.

{% hint style="danger" %}
**Important**

The **Delete applications even if they have a deployment** checkbox is only available when the [Retain up to X previously created applications](application-creation-options.md#retain-up-to-x-previously-created-applications) setting is configured.
{% endhint %}

This option provides flexibility for environments where older application deployments are no longer required but may still exist, allowing retention cleanup to proceed without the need for manual intervention to remove a deployment(s).

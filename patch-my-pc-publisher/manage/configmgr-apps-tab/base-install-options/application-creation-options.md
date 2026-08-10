# Application Creation Options section in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Application Creation Options** section in Patch My PC (PMPC) Publisher controls how applications are created, updated, named, organized, and maintained in ConfigMgr when using the Publisher.

These settings apply globally to all applications created from the ConfigMgr Apps tab and directly influence application lifecycle behavior.

> \*\*Note\*\*
>
> See \[Application Creation Options]\(application-creation-options.md) for more information.

> \*\*Tip\*\*
>
> Some options in the \*\*Application Creation Options\*\* section are global defaults. These settings can be overridden at the \*\*vendor\*\* or \*\*product\*\* level within the Product Tree. When a more specific customization exists at a lower level, it takes precedence over the global setting, following standard product tree inheritance behavior.

## Allow applications to be installed from the Install Application task sequence action

When the **Allow applications to be installed from the Install Application task sequence action** setting is enabled, Publisher explicitly sets this flag on the application object in ConfigMgr.

Specifically, Publisher enables **Allow this application to be installed from the Install Application task sequence action without being deployed** on each application it creates or updates.

![Allow applications to be installed from the Install Application task sequence action](/_images/image-(509).png)

> \*\*Tip\*\*
>
> This setting does not have to be enabled when applications are explicitly referenced in a task sequence using a fixed application selection in the \*\*Install Application\*\* step.

> \*\*Important\*\*
>
> When enabled, this setting is applied \_only\_ when the deployment type setting, \*\*installation behavior,\*\* is set to \*\*Install for system\*\*. User-based applications that install in the user context do not meet the requirements for this setting.
>
> See \[Product Naming in the Patch My PC Catalog]\(../../../technical-references/catalog-information.md#product-naming-in-the-patch-my-pc-catalog) for more details on how to identify a user-based app.

This option should be left set to **Enabled** _only_ in the following scenarios:

* Applications installed using dynamic application selection in a task sequence.
* Applications are evaluated and selected at runtime, rather than being hard-coded in the task sequence.

### Policy impact and when to disable this option

Enabling the **Allow applications to be installed from the Install Application task sequence action without being deployed** setting causes ConfigMgr to generate additional application policy. This policy is distributed to clients even if the application is never used in a task sequence.

If your environment does not use variable-driven or dynamically selected application lists in task sequences, this option is typically not required and can be disabled to reduce unnecessary policy processing.

If your environment uses task sequences that install applications dynamically, such as using an Application List variable or runtime logic, this option should be left enabled (which it is by default) to prevent task sequence failures.

As a general guideline, enable this option only when task sequences rely on dynamic application selection. If applications are always explicitly referenced in task sequences or deployed normally, disabling this option helps minimize policy overhead.

## Allow clients to use distribution points from the site’s default boundary group

Enabling the **Allow clients to use distribution points from the site’s default boundary group** setting enables a fallback behavior during application installation. If the requested application content is not available on any Distribution Point (DP) in the client’s current or neighboring boundary groups, the client is allowed to download the content from DPs belonging to the site’s **default boundary group**.

When enabled by Publisher, this setting is applied directly to the application deployment type in ConfigMgr. It helps prevent installation failures in scenarios where boundary group coverage is incomplete or where content has not yet been distributed to all required DPs.

![Allow clients to use distribution points from the site's default boundary group](/_images/image-(510).png)

> \*\*Note\*\*
>
> Whilst this option improves resiliency, it can result in clients downloading content from less optimal DPs, such as across slower network links, if the default boundary group contains DPs that are remote to the client's location.

## **Code sign the PowerShell detection method script using the WSUS signing certificate**

When enabling **Code sign the PowerShell detection method script using the WSUS signing certificate** setting, Publisher digitally signs PowerShell-based detection method scripts using the [WSUS code signing certificate](../../wsus-updates-tab/wsus-options/certificate-management/).

This ensures the detection scripts are trusted and can run successfully on clients that enforce PowerShell execution policy or script signature requirements.

This setting is applied directly to the detection method of each application deployment type created or updated by Publisher.

![Code sign the PowerShell detection method script using the WSUS signing certificate](/_images/image-(512).png)

> \*\*Important\*\*
>
> You cannot select a different certificate for signing detection scripts. Publisher always uses the WSUS code signing certificate configured on the \[WSUS Options]\(../../wsus-updates-tab/wsus-options/) tab.
>
> Even in ConfigMgr-only environments where the WSUS Updates tab might be hidden, the \[WSUS Role ]\(../../../requirements/wsus-requirements/software.md#wsus-role)must still be installed on the Publisher server. Publisher retrieves the code signing certificate from the local WSUS certificate store, and this same certificate is used for both third party updates and ConfigMgr application detection script signing.

## Do not include the version in the application name...

When the **Do not include the version in the application name, so the application name doesn’t change after updates** setting is enabled, newly created applications will no longer include the version number in the application name.

This behavior is useful in scenarios where external tooling or processes reference applications by name, such as MDT UDI, UI++, or other solutions that rely on a static application name.

When this option is disabled (the default setting), each new application version includes the version number in the name. As a result, the application name changes every time a new version is published.

When this option is enabled, the application name remains the same across versions, while the underlying content, detection logic, and deployment type are updated to reflect the latest release.

As shown in the example below, **Notepad++ (x86)** was published with this option enabled, while **Notepad++ 8.8.9 (x64)** was published with the option disabled.

In both cases, the exact application version is still visible in the **Software Version** column in the ConfigMgr console.

![](/_images/image-(513).png)

> \*\*Note\*\*
>
> If you want to control application naming on a per-product basis, additional naming options are available through the \[right-click customizations]\(../../../customizations/) menu in the Product Tree. Product-level naming options override this global setting.

> \*\*Important\*\*
>
> If this feature is enabled and application retention is also enabled, any retained applications will have the version number appended to their names to distinguish them from the current version.

## Move applications to a specific console folder

This option controls _where_ applications created or updated by Publisher are placed within the **Application Management | Applications** node of the ConfigMgr console.

When the **Move applications to the following folder in the applications node of the console** setting is enabled and configured, Publisher automatically moves each application it creates or updates into the selected console folder. This helps keep third-party applications organized and separate from manually created or first-party applications.

To choose where applications are placed in the ConfigMgr console:

1. Enable **Move applications to the following folder in the applications node of the console**.
2. Select **Browse Folders**.
3. In the **Select Console Folder** window:
   * Expand the **Applications** node.
   * Select an existing folder (for example, **Applications\3rd Party Apps**), **or**
   * Enter a name in **Create New Folder** and select **Create Folder**.
4. Select **OK** to confirm the folder selection.
5. Select **OK** again to save the ConfigMgr Apps Options.

All applications created or updated by Publisher will now be moved to the selected console folder.

![Move applications to the following folder in the applications node of the console](/_images/image-(220).png)

> \*\*Note\*\*
>
> The selected console folder can be overridden at the vendor or product level using the \[product tree]\(../../../../patch-my-pc-publisherv2/administration/configmgr-apps/product-tree.md) on the ConfigMgr Apps tab. If a folder is defined at a lower level in the tree, that more specific setting takes precedence over this global. For more information, see \[Customizations (Right-Click Options)]\(../../../../patch-my-pc-publisherv2/customizations-right-click-options/).

## When a new application update is available

The following settings control how the Publisher handles new versions of applications that were previously created by the Publisher. The behavior you choose determines whether existing applications are updated in place, new applications are created, and how older versions are retained or removed.

![Application Lifecycle Settings](/_images/image-(221).png)

### Update existing application’s metadata, deployment type, detection method, and content files (Default)

When **Update existing application’s metadata, deployment type, detection method, and content files** is selected, the Publisher updates an existing ConfigMgr application _in place_ rather than [creating a brand new application](application-creation-options.md#create-a-new-application-without-modifying-any-previous-applications).

This option is the default and is commonly used because the application ID does not change in ConfigMgr when we update it to the new version. By keeping the same application ID:

* Task sequences that reference the application continue to work without modification.
* Existing required and available deployments remain intact, ensuring that the latest version of the application is automatically deployed or made available in Software Center to the same device collections that targeted the previous version.

This is especially valuable for operating system deployment scenarios, where administrators want task sequences to always install the most recent version without updating references every time a new release is published.

Before performing an in-place update, the Publisher validates that the application is in a healthy state. This includes confirming that:

* The application was originally created and is managed by the Publisher.
* The corresponding application content exists on disk in the content source folder.

These checks are required to safely support additional behaviors such as application retention and cleanup.

When an in-place update occurs, the Publisher:

* Preserves the existing application object and application ID.
* Updates application metadata such as:
  * Software version.
  * Application Name.
  * Description and related metadata.
* Removes the existing Deployment Type.
* Creates a new Deployment Type and corresponding content source folder.

> \*\*Tip\*\*
>
> Removing and recreating the deployment type results in \*\*2 new revisions\*\* on the application object for each update. Over time, this causes the total number of application revisions to increase.

> \*\*Important\*\*
>
> In some environments using a Cloud Management Gateway (CMG), a small number of customers have historically observed issues when updating applications in place. In these cases, clients may encounter content or policy hash mismatches, where updated application policy does not consistently replicate through the CMG.
>
> A common symptom of this behavior is an error similar to the following in \*\*CIDownloader.log\*\* on affected clients:
>
> \`Evaluation Failed, 0x87D00289 (-2016410999), Unknown Error\`
>
> These issues have most commonly been observed with applications that have multiple revisions, which can occur over time when an application is repeatedly updated in place.
>
> If you encounter these symptoms in a CMG-enabled environment, the recommended workaround is to use \*\*Create a new application without modifying any previous applications\*\* instead of updating applications in place.

#### Delay the in-place application upgrade by _X_ days

When enabled, application updates are delayed for the specified number of days after the new version is synchronized from the catalog.

* The delay is calculated from the date the new version is first detected by the Publisher.
* This allows time for validation or testing before updating production applications.

**Example:**\
If a new version is synchronized on February 3 and the delay is set to 3 days, the application will not be updated until a Publisher sync on or after February 6.

### Create a new application without modifying any previous applications

When **Create a new application without modifying any previous applications** is selected, the Publisher creates a brand-new ConfigMgr application for each new version instead of updating an existing application in place. Unlike the [in-place update option](application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default), a new application ID is created for every version.

This option is commonly used in environments where administrators want to preserve each application version independently or avoid modifying existing application objects. It is also best suited for environments where strict version control is required and task sequences are updated intentionally.

Because a new application is created each time:

* Task sequences that reference older application versions will continue to install those versions until they are manually updated to reference the new application.
* Existing required and available deployments remain associated only with the original application and do not automatically apply to the newly created application.

> \*\*Note\*\*
>
> The option to \*\*Create a new application without modifying any previous applications\*\* can result in application sprawl over time if older versions are not cleaned up. For this reason, it is commonly used together with \[application retention settings]\(application-creation-options.md#retain-up-to-x-previously-created-applications) to limit the number of older application versions kept in the environment.

### Retain up to x previously created applications

The **Retain up to x previously created applications** option controls how many older application versions are retained in ConfigMgr when new versions are published by the Publisher. It applies regardless of whether you choose to [**update applications in place**](application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default) or [**create a new application for each version**](application-creation-options.md#create-a-new-application-without-modifying-any-previous-applications).

Valid values range from **0 to 10**.

When this value is set to **0**, only the latest version of an application is kept in ConfigMgr. Any older versions are removed.

When this value is set greater than **0**, the Publisher retains that number of older application versions alongside the latest version.

For example, setting this value to **1** ensures that the environment always contains the latest application version and one previous version. This allows for quick rollback to a last known good version if needed, while preventing excessive growth in the number of applications.

> \*\*Tip\*\*
>
> Application retention can be adjusted at the vendor and product levels in the \[product tree]\(../../../../patch-my-pc-publisherv2/administration/configmgr-apps/product-tree.md), allowing more granular control and will override the global setting configured.
>
> This option is especially useful for third-party applications with a rapid release cadence, such as web browsers. Retaining additional versions makes it easier to roll back if needed using supersedence. For more information about using supersedence in ConfigMgr, see: [https://learn.microsoft.com/en-us/intune/configmgr/apps/deploy-use/revise-and-supersede-applications#supersedence](https://learn.microsoft.com/en-us/intune/configmgr/apps/deploy-use/revise-and-supersede-applications#supersedence)

> \*\*Note\*\*
>
> The Publisher tracks only the \*\*10 most recent application versions\*\* during synchronization. If older application versions fall outside this tracked window, the Publisher cannot automatically clean them up through application retention. These older versions must be reviewed and removed manually if cleanup is required. The recommended approach for cleanup is to use the \[ConfigMgr Application Manager]\(../../../../patch-my-pc-publisherv2/administration/configmgr-apps/form-controls/configmgr-application-manager.md).

> \*\*Important\*\*
>
> The Publisher will not delete an application that is referenced by a task sequence, even if it exceeds the retention limit and the option to delete applications with deployments is enabled.
>
> Applications referenced by task sequences must be manually removed from the task sequence before they become eligible for deletion by the Publisher.

#### **Behavior with update in place**

When [Update existing application’s metadata, deployment type, detection method, and content files](application-creation-options.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default) is selected, application retention is handled by first preserving the current version before applying the update.

Before the application is updated to the new version, the Publisher duplicates the existing application and moves it's content into a **Retained Apps** folder. The application is then updated in place by removing the existing deployment type and creating a new deployment type for the latest version. This ensures the previous version is retained according to the configured retention count while the application ID remains unchanged.

If the number of applications exceeds the configured retention value, the Publisher removes the oldest application versions, starting with those that fall outside the retention window.

**Behavior with create new application**

When [Create a new application without modifying any previous applications](application-creation-options.md#create-a-new-application-without-modifying-any-previous-applications) is selected, application retention is applied across the chain of independently created application objects.

Each new version is created as a separate application. If the number of applications exceeds the configured retention value, the Publisher removes the oldest application versions, starting with those that fall outside the retention window.

### **Remove administrative categories from retained applications**

This option is available only when [Retain up to X previously created applications](application-creation-options.md#retain-up-to-x-previously-created-applications) is configured.

By default, all administrative categories assigned to a ConfigMgr application are preserved when older application versions are retained. This is useful in scenarios such as operating system deployment frontends, where administrative categories are used to populate application selection lists. The option to **Remove administrative categories from retained applications is** ensures that only the current version appears in those lists, preventing outdated versions from being presented.

When this option is enabled, administrative categories are removed from retained (older) application versions. Only the latest published application keeps the assigned administrative categories.

For more information about assigning categories to ConfigMgr apps, see [Customizations (Right-Click Options)](../../../../patch-my-pc-publisherv2/customizations-right-click-options/).

### **Delete applications even if they have a deployment**

This option is available only when [Retain up to X previously created applications](application-creation-options.md#retain-up-to-x-previously-created-applications) is configured.

When the **Delete applications even if they have a deployment** is enabled, the Publisher can delete retained application versions even if they have existing deployments. When disabled, applications with active deployments are preserved and are not removed during retention cleanup.

This option provides flexibility for environments where older application deployments are no longer required but may still exist, allowing retention cleanup to proceed without the need for manual intervention top remove a deployment(s).
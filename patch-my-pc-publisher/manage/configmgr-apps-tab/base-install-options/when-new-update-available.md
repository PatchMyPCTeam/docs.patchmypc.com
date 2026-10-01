---
hidden: true
---

# When a New Update is Available section in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **WHEN A NEW UPDATE IS AVAILABLE** section on the **Base Install Options** tab of Patch My PC (PMPC) Publisher controls how Publisher handles new versions of applications that were previously created by Publisher. The behavior you choose determines whether existing applications are updated in place, new applications are created, and how older versions are retained or removed.

<figure><img src="../../../../.gitbook/assets/image (1253).png" alt="&#x27;WHEN A NEW UPDATE IS AVAILABLE&#x27; section" width="563"><figcaption></figcaption></figure>

In this section, you can choose either:

* [Update existing application (Default)](when-new-update-available.md#update-existing-application-default)
* [Create a new application](when-new-update-available.md#create-a-new-application)

{% hint style="info" %}
**Note**

Some settings apply to both options as detailed in [Common Settings](when-new-update-available.md#common-settings).
{% endhint %}

## Update existing application (Default)

When the **Update existing application (Default)** option is selected, Publisher updates an existing ConfigMgr application _in place_ rather than [creating a brand new application](when-new-update-available.md#create-a-new-application-without-modifying-any-previous-applications).

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

### Delay the in-place application upgrade by _x_ days

When the **Delay the in-place application upgrade by&#x20;**_**x**_**&#x20;days** option is enabled, application updates are delayed for the specified number of days after the new version is synchronized from the catalog.

* The delay is calculated from the date Publisher first detects the new version.
* This allows time for validation or testing before updating production applications.

**Example:**\
If a new version is synchronized on February 3 and the delay is set to 3 days, the application will not be updated until a Publisher sync on or after February 6.

{% hint style="info" %}
**Note**

See [Common Settings](when-new-update-available.md#common-settings) for more information about the other available settings when this option is selected.
{% endhint %}



## Create a new application

When the **Create a new application** option is selected, Publisher creates a new ConfigMgr application for each new version instead of updating an existing application in place. Unlike the [in-place update option](when-new-update-available.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default), it creates a new application ID for every version.

<figure><img src="../../../../.gitbook/assets/image (1254).png" alt="Create a new application" width="563"><figcaption></figcaption></figure>

This option is commonly used when administrators want to preserve each application version independently or avoid modifying existing application objects. It is also best suited for environments where strict version control is required, and task sequences are updated intentionally.

Because a new application is created each time:

* Task sequences that reference older application versions will continue to install those versions until they are manually updated to reference the new application.
* Existing required and available deployments remain associated only with the original application and do not automatically apply to the newly created application.

{% hint style="info" %}
**Note**

The option to **Create a new application** can result in application sprawl over time if older versions are not cleaned up. For this reason, it is commonly used together with [application retention settings](when-new-update-available.md#retain-up-to-x-previously-created-applications) to limit the number of older application versions kept in the environment.

Also, see [Common Settings](when-new-update-available.md#common-settings) for more information about the other available settings when this option is selected.
{% endhint %}

## Common Settings

The following settings can be enabled and configured regardless of whether **Update existing application** or **Create a new application** are selected:

* [Retain up to _x_ previously created applications](when-new-update-available.md#retain-up-to-x-previously-created-applications)
* [Remove administrative categories from retained applications](when-new-update-available.md#remove-administrative-categories-from-retained-applications)
* [Delete applications even if they have a deployment](when-new-update-available.md#delete-applications-even-if-they-have-a-deployment)

### Retain up to _x_ previously created applications

When checked, the **Retain up to x previously created applications** checkbox controls how many older application versions ConfigMgr retains when Publisher publishes new versions. It applies regardless of whether you choose to [**update applications in place**](when-new-update-available.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default) or [**create a new application for each version**](when-new-update-available.md#create-a-new-application-without-modifying-any-previous-applications).

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

When you select the [Update existing application’s metadata, deployment type, detection method, and content files](when-new-update-available.md#update-existing-applications-metadata-deployment-type-detection-method-and-content-files-default) option, application retention works by first preserving the current version before applying the update.

Before updating the application to the new version, Publisher duplicates the existing application and moves its content into a **Retained Apps** folder. Publisher then updates the application in place by removing the existing deployment type and creating a new deployment type for the latest version. This ensures the previous version is retained according to the configured retention count while the application ID remains unchanged.

If the number of applications exceeds the configured retention value, Publisher removes the oldest application versions, starting with those that fall outside the retention window.

#### **Behavior with create new application**

When the [Create a new application without modifying any previous applications](when-new-update-available.md#create-a-new-application-without-modifying-any-previous-applications) option is selected, application retention is applied across the chain of independently created application objects.

Each new version is created as a separate application. If the number of applications exceeds the configured retention value, Publisher removes the oldest application versions, starting with those that fall outside the retention window.

### **Remove administrative categories from retained applications**

By default, all administrative categories assigned to a ConfigMgr application are preserved when you retain older application versions. This is useful in scenarios such as operating system deployment frontends, where administrative categories are used to populate application selection lists. The option to **Remove administrative categories from retained applications** ensures that only the current version appears in those lists, preventing outdated versions from being presented.

{% hint style="danger" %}
**Important**

The **Remove administrative categories from retained applications** checkbox is only available when the [Retain up to X previously created applications](when-new-update-available.md#retain-up-to-x-previously-created-applications) setting is configured.
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

The **Delete applications even if they have a deployment** checkbox is only available when the [Retain up to X previously created applications](when-new-update-available.md#retain-up-to-x-previously-created-applications) setting is configured.
{% endhint %}

This option provides flexibility for environments where older application deployments are no longer required but may still exist, allowing retention cleanup to proceed without the need for manual intervention to remove a deployment(s).

# Tenant Management

_Applies to: Patch My PC Publisher V2.x_

Each tenant added to the Publisher has its own authentication settings, application options, product selections and customizations.

## Add a Tenant

The Add Tenant button allows you to create a new tenant configuration within the Publisher.

<figure><img src="../../../../.gitbook/assets/image (4108).png" alt="Add a Tenant" width="545"><figcaption></figcaption></figure>

To add a new Tenant:

1. Click the **Add Tenant** button. The Intune Options form open automatically for tenant configuration.

<figure><img src="../../../../.gitbook/assets/image (4110).png" alt="Intune Options form opened when adding a new tenant" width="563"><figcaption></figcaption></figure>

2. Complete the configuration by following [Scenario 4: Intune Applications and Updates](../../../scenario-based-guidance/installation-and-configuration/scenario-4-intune-applications-and-updates.md)   . Specifically **Steps 7 through 14**.

{% hint style="info" %}
**Note**

Steps 7 through 14 cover configuring authentication and core application settings for the new tenant, validating the connection, and enabling required publishing options.

This includes entering the Tenant Friendly Name, configuring the Entra ID application details and credential, reviewing and adjusting Application Options, and testing the connection.


{% endhint %}

3. Once the Intune Options have been configured, click **OK** to close the form and return to the main Publisher window.

<figure><img src="../../../../.gitbook/assets/image (4112).png" alt="Saving Intune Options for the newly added tenant" width="301"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Caution**

During the save process, the main product tree refreshes and the first tenant in the tenant drop down list is automatically reselected.

After the refresh completes, ensure you manually select the newly created tenant from the drop down list before continuing with product selections and customizations.
{% endhint %}

4. Select the required products in the [product tree](../product-tree.md) for the newly added tenant.

{% hint style="info" %}
**Note**

Product selections apply only to the currently selected tenant.
{% endhint %}

5. Configure any required right-click customizations. For detailed guidance, see [Customizations (Right-Click Options)](../../../customizations-right-click-options/).

## Delete a Tenant

The Delete Tenant button allows you to remove an existing tenant configuration from the Publisher.

<figure><img src="../../../../.gitbook/assets/image (4109).png" alt="Delete a Tenant" width="545"><figcaption></figcaption></figure>

To delet a Tenant:

1. Select the tenant you want to remove from the Tenant drop down list.
2. Click the **Delete Tenant button**.
3. When the confirmation dialog appears, Click **Yes** to permanently remove the tenant, or click **No** to cancel.

<figure><img src="../../../../.gitbook/assets/image (4111).png" alt="Delete a tenant confirmation" width="300"><figcaption></figcaption></figure>

After confirmation, the tenant configuration is removed from the current Publisher instance and no longer appears in the tenant drop down list.

{% hint style="info" %}
**Note**

After confirmation, the tenant configuration is removed from the current Publisher instance and no longer appears in the tenant drop down list.

Deleting a tenant removes its authentication settings, application options, product selections, and customizations from the Publisher.

This action **does not** remove applications or updates that were previously published to Microsoft Intune.
{% endhint %}

{% hint style="warning" %}
**Important**

If the tenant needs to be re-added later, it must be configured again manually or imported from a previously exported configuration.

You can import a tenant only if the export was created from a Publisher instance that was configured for single tenancy using an Enterprise Plus or Enterprise Premium license. Exports created from a Publisher instance that was already configured for multi-tenant management cannot be imported into another multi-tenant instance.
{% endhint %}

## Import a Tenant

Tenant import allows you to add an existing tenant configuration into a multi-tenant Publisher instance.

<figure><img src="../../../../.gitbook/assets/image (4113).png" alt="Import a Tenant" width="545"><figcaption></figcaption></figure>

{% hint style="warning" %}
**Important**

Before importing, ensure the tenant configuration was exported from a Publisher instance that was configured in single-tenant mode. In most cases, this means the source Publisher instance was licensed with Enterprise Plus or Enterprise Premium at the time the export was created.

The absence of a tenant selector in the Intune Apps or Intune Updates tabs indicates the Publisher was operating in single-tenant mode. The term single-tenant mode is used here only to distinguish it from multi-tenant functionality.
{% endhint %}

{% hint style="danger" %}
**Caution**

Exports from a multi-tenant Publisher instance cannot be imported into another multi-tenant instance. Attempting to do so would require manual modification of the settings.xml file, which is not supported and is not recommended.
{% endhint %}

To import a tenant configuration from another Publisher instance:

1. Export the Publisher configuration from the source Publisher instance. See Export Settings in [Backup and Restore Settings](../../advanced/backup-and-restore-settings.md) for more details.
2. Click the **Import Intune Tenants** button.
3. Browse to the exported file from the source Publisher instance. If the file was exported from another Publisher instance as a .cab file, change the file type filter to .cab.&#x20;

<figure><img src="../../../../.gitbook/assets/image (4114).png" alt="Select the correct file type filter" width="563"><figcaption></figcaption></figure>

4. Select the appropriate .cab or .xml file and click **Open**.
5. Wait for the import process to complete. A confirmation message will indicate that the Intune tenant has been successfully imported. Click **OK**.

<figure><img src="../../../../.gitbook/assets/image (4115).png" alt="Tenant import successful" width="432"><figcaption></figcaption></figure>

6. Select the newly imported tenant from the Tenant drop down list and click **Options**.

<figure><img src="../../../../.gitbook/assets/image (4116).png" alt="Configure the imported tenant" width="563"><figcaption></figcaption></figure>

7. Review the imported configuration is correct.

{% hint style="warning" %}
**Important**

Client Secrets are securely salted on the source Publisher instance and cannot be restored to a different Publisher instance. Certificates are also not transferred during export and import.

After importing a tenant, review the selected client authentication method and reconfigure the App Secret or App Certificate as required before testing the connection or enabling publishing.


{% endhint %}

8. Once the Intune Options have been configured, click **OK** to close the form and return to the main Publisher window.

<figure><img src="../../../../.gitbook/assets/image (4112).png" alt="Saving Intune Options for the newly added tenant" width="301"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Caution**

During the save process, the main product tree refreshes and the first tenant in the tenant drop down list is automatically reselected.

After the refresh completes, ensure you manually select the newly created tenant from the drop down list before continuing with product selections and customizations.
{% endhint %}

9. Review the selected products in the [product tree](../product-tree.md) for the imported tenant.
10. Review and configure any required right-click customizations. For detailed guidance, see [Customizations (Right-Click Options)](../../../customizations-right-click-options/).

{% hint style="info" %}
**Note**

For full consideration of items that are not included in an export or backup, see [Backup and Restore](../../advanced/backup-and-restore-settings.md).

Certain items are not contained within the exported configuration file. This includes external or supplemental content such as additional files and custom images, for example branding images used for the Managed Client Processes feature.

It is recommended that you review all right-click options and any configurations that reference external files. Confirm that any additional files, scripts, certificates, or image assets referenced in customizations are manually backed up and restored as required.

These items must be handled separately, as they are not included in the tenant configuration export.
{% endhint %}

### Import Multiple Tenants

The Publisher supports importing multiple tenant configuration files in a single operation..

To Import Multiple Tenants:

1. Ensure each tenant configuration was exported from a supported single tenant Publisher instance (typically licensed with the Enterprise Plus or Enterprise Premium SKU).
2. On the target multi-tenant Publisher instance, click the **Import Intune Tenant** button.
3.   Browse to the exported files from the source Publisher instance. If the files were exported from another Publisher instance as a .cab file, change the file type filter to .cab.

<figure><img src="../../../../.gitbook/assets/image (4117).png" alt="Import multiple tenants" width="563"><figcaption></figcaption></figure>

4. Select the appropriate .cab or .xml files and click **Open**.
5. Wait for the import process to complete. A confirmation message will indicate that the Intune tenants were successfully imported. Click **OK**.

<figure><img src="../../../../.gitbook/assets/image (4118).png" alt="Tenant import successful" width="442"><figcaption></figcaption></figure>

6. Select the first tenant from Tenant drop down box that you want to review and continue from **Step 8** in [Import a Tenant](tenant-management.md#import-a-tenant). In the example below, 2 tenants were imported.

<figure><img src="../../../../.gitbook/assets/image (4119).png" alt="Imported Tenants" width="545"><figcaption></figcaption></figure>

## Select and Manage a Tenant

In a multi-tenant Publisher configuration, the Intune Apps and Intune Updates tabs are configured independently for each tenant.

Use the tenant drop down box at the top of the Intune Apps or Intune Updates tab to select the tenant you want to manage. All product selections, customizations, and publishing options apply only to the currently selected tenant.

The Options button also corresponds to the selected tenant. When you open [Intune Options](../options/), you are viewing and modifying authentication settings and application options for that specific tenant only.

There are no global Intune configuration settings that can be applied across all tenants simultaneously. Product selections, right click customizations, and publishing behavior must be configured individually for each tenant.

{% hint style="success" %}
**Tip**

If you are an MSP interested in centralized application sets or shared configuration capabilities across customers, consider the Patch My PC Cloud solutions where you can leverage [Templates](../../../../patch-my-pc-cloud/deployments/use-template.md) and [MSP App Sets](../../../../patch-my-pc-cloud/managed-service-provider-feature/msp-app-sets/).
{% endhint %}

{% hint style="info" %}
**Note**

For tenant specific email and webhook configuration, see [Notifications](notifications.md).
{% endhint %}

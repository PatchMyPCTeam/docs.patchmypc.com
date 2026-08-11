# Modify Published Updates

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Modify Published Updates** wizard is used to manage third party updates that have already been published to WSUS. It provides a centralized view of published updates and allows administrators to safely maintain, clean up, and correct updates without needing to manually interacting with the WSUS console.

This wizard is commonly used during troubleshooting, republishing workflows, and ongoing maintenance to ensure WSUS and ConfigMgr only evaluate and display the correct updates.

![Modify Published Updates](/_images/image-(91 "Modify Published Updates") (1).png>)

Clicking **Run Wizard** opens the **Modify Updates Wizard**.

![Modify Updates Wizard](/_images/image-(195).png)

The **Modify Updates Wizard** is divided into two main areas that make it easy to locate and manage published, third-party, updates. The upper portion of the window contains filtering controls, while the main pane displays the list of matching updates and their current state.

The filtering area allows you to quickly narrow down updates based on common attributes such as vendor, declined status, expired status, supersedence status, metadata state, and enabled status. Multiple filters can be combined to precisely target updates, which is especially useful in environments with a large number of published third party updates. A title filter is also available to search by update name, making it easy to locate specific products or versions.

The main results grid displays each update along with key information, including classification, vendor, publish date, and current state in WSUS. From this view, you can select one or more updates and perform actions using the buttons at the bottom of the wizard. This layout allows administrators to review update status and take action without switching between the Publisher, WSUS, and ConfigMgr consoles.

## Conditional Formatting

The UpdateID column is highlighted in yellow when the update is in a WSUS state that is not considered complete or healthy.

This typically indicates that publishing did not complete successfully or that update content is missing or not yet available. Common causes include incomplete content upload or metadata processing issues.

The yellow highlight is an attention indicator. Click [**More Details**](modify-published-updates.md#more-details) so see the update status.

![Conditional Formatting](/_images/image-(196).png)

If you select an update that is highlighted in yellow and choose [**Show in WSUS**](modify-published-updates.md#show-in-wsus), the WSUS console provides more detailed state information. This additional detail can help identify why the update is flagged, such as missing content.

![Update Missing Content](/_images/image-(472 "Update Missing Content") (1).png>)

## Filtering

The filtering options at the top of are used to quickly narrow down the list of published updates. This is especially important in environments with a large number of third party updates, where manually scrolling through the list would be inefficient.

| Filter name       | Description                                                                                                                                                       | Values                                                                               |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Vendor            | Filters updates by the publishing vendor. This is commonly used to isolate Patch My PC updates or updates from a specific third-party vendor.                     | <p>Default = All Vendors<br>&#x3C;Patch My PC><br>&#x3C;vendor 2></p>                |
| Declined Status   | Filters updates based on whether they are currently declined in WSUS. This is useful when identifying updates that are still active versus those already retired. | <p>Default - All Declined Status</p><p>Yes = Declined<br>No = Not Declined</p>       |
| Expired Status    | Filters updates based on whether they are marked as expired. Expired updates are no longer evaluated by ConfigMgr clients.                                        | <p>Default - All Expired Status</p><p>Yes = Expired</p><p>No = Not Expired</p>       |
| Superseded Status | Filters updates based on whether they are superseded by another update.                                                                                           | <p>Default = All Superseded Status<br>Yes = Superseded</p><p>No = Not Superseded</p> |
| Metadata Status   | Filters updates based on whether the update is published with Full Content or Metadata only.                                                                      | <p>Default = All Metadata Status<br>Yes = Metadata Only</p><p>No = Full Content</p>  |
| Enabled Status    | Filters updates based on if they are selected (Enabled) in the Publisher                                                                                          | <p>Default = All Enabled Status<br>Yes = Enabled<br>No = Not Enabled</p>             |
| Title Filter      | Allows searching by update name. This is useful for locating specific products or versions, including republished updates that include a timestamp in the name.   | \<string>                                                                            |

## Decline (Updates)

**Declining** an update marks it as declined in WSUS. Declined updates are no longer evaluated for installation by the Windows Update Agent for WSUS standalone environments or by ConfigMgr clients.

Declining updates is most commonly used to reduce legacy technical debt in environments where multiple third party catalogs have been used over time. In these scenarios, WSUS often contains thousands of third party updates that are no longer deployed or used for compliance. If updates remain undeclined, ConfigMgr continues to evaluate them for applicability, even if they are never deployed. This unnecessary evaluation increases client scan times and adds additional IIS and database load on WSUS servers.

Declining unused updates helps streamline the update catalog and improves overall performance. By ensuring that only actively managed updates remain available, clients spend less time scanning for applicability and WSUS processes fewer update records during synchronization and evaluation cycles. As a best practice, any update that is no longer required should be declined to minimize operational overhead.

To decline one or more published updates:

1. Locate and select the update or updates you want to decline using the available filters.
2. Select **Decline** at the bottom of the wizard. The Publisher sends the request to WSUS and displays a progress and confirmation window showing the result for each selected update.

![Decline Update(s)](/_images/image-(197).png)

> \*\*Note\*\*
>
> Declining updates is also important for managing WSUS product category limits. Some patch management solutions create a separate WSUS product category for each product or vendor. Over time, this can cause the total number of enabled categories to exceed the Microsoft supported limit of 100, which can lead to publishing and synchronization failures.
>
> Declining updates from unused catalogs helps reduce the effective category footprint in WSUS and prevents hitting this limit.
>
> For more information on category limits and related publishing errors, see: [https://patchmypc.com/kb/publish-error-too-many-locally-published-categories/](https://patchmypc.com/kb/publish-error-too-many-locally-published-categories/)

> \*\*Tip\*\*
>
> Only after a Software Update Point synchronization are declined updates marked as expired in ConfigMgr.

## Un-decline (Updates)

The **Un-decline** option is used to reverse a previously declined update and make it active again. The exact behavior depends on whether the environment is using ConfigMgr or WSUS in standalone mode.

In a ConfigMgr environment, undeclining is only possible while the update still exists in the ConfigMgr database. After an update is declined and a Software Update Point synchronization runs, the update is marked as expired in ConfigMgr. Expired updates remain available only until ConfigMgr maintenance removes them. ConfigMgr runs a cleanup stored procedure on a regular schedule, typically every seven days, to remove expired updates. Once this cleanup has occurred, the update can no longer be undeclined.

In a WSUS standalone environment without ConfigMgr, the undecline behavior is simpler. Declined updates remain in WSUS until they are manually deleted or cleaned up using WSUS maintenance. As long as the update still exists in WSUS, it can be undeclined at any time.

To un-decline one or more published updates:

1. Locate and select the update or updates you want to decline using the available filters.
2. Select **Un-decline** at the bottom of the wizard. The Publisher sends the request to WSUS and displays a progress and confirmation window showing the result for each selected update.

![Un-decline Update(s)](/_images/image-(198).png)

## Delete Updates

The **Delete** option permanently removes selected published updates from WSUS. This action deletes the update metadata and content and cannot be reversed. Because of the risk associated with permanent deletion, the Delete button is disabled by default.

Deleting updates is intended only for exceptional scenarios, such as updates that were published in error, cleaning up unused third party vendors, or reducing WSUS product categories that should no longer exist. It is not recommended for routine maintenance or general cleanup. In most cases, declining updates is the preferred and safer option, as it avoids potential update identity and hash related issues.

> \*\*Important\*\*
>
> Deleting updates permanently removes them from WSUS. If the associated product remains enabled in the Publisher, the Publisher will publish the same update on the next sync, using the same Update ID. When this happens, ConfigMgr can resynchronize the update and clients may already have cached content that no longer matches the republished update.
>
> This mismatch can cause hash validation failures during deployment and prevent updates from installing successfully on clients.

![Delete option disabled by default](/_images/image-(199).png)

To delete one or more published updates:

1. [Enable the Delete option](modify-published-updates.md#enabling-the-delete-option) via a registry value in the **Patch My PC Publishing Service** key.
2. Locate and select the update or updates you want to delete using the available filters.
3. Select **Delete** at the bottom of the wizard. The Publisher sends the request to WSUS and displays a progress and confirmation window showing the result for each selected update.
4. Click **Yes** to delete the update(s) or click **No** to abort the deletion.

![Confirm deletion](/_images/image-(201).png)

5. Review the results to confirm the action completed successfully, then select **Close** to exit the confirmation window.

### Enabling the Delete option

The Delete button is hidden by default and must be explicitly enabled using a registry key. This safeguard helps prevent accidental deletion of updates.

To enable the Delete option:

1. On the system where the Publisher service is installed, open an elevated command prompt.
2. Run the following command:

```
REG ADD "HKLM\SOFTWARE\Patch My PC Publishing Service" /v EnableDeleteUpdates /t REG_DWORD /d 1
```

3. Close and re-open the Modify Updates Wizard form.

## Show in WSUS

The **Show in WSU**S option control whether locally published third party updates are visible in the WSUS console. This option does not affect update applicability, deployment, or compliance in ConfigMgr. They only control WSUS console visibility.

This is typically used for troubleshooting scenarios where additional WSUS level detail is required, such as reviewing update state, content status, or category associations directly in WSUS.

When this option is selected, the Publisher marks the update so it appears in the WSUS console. This allows administrators to use native WSUS views to investigate publishing or processing issues without changing how the update behaves in WSUS or ConfigMgr.

To show one or more published updates in the WSUS console:

1. Locate and select the update or updates you want to show in WSUS using the available filters.
2. Select **Show in WSUS** at the bottom of the wizard. The Publisher sends the request to WSUS and displays a progress and confirmation window showing the result for each selected update.
3. Review the results to confirm the action completed successfully, then select **Close** to exit the confirmation window.

![Show Update(s) in WSUS](/_images/image-(202).png)

## Hide in WSUS

The **Hide in WSU**S option control whether locally published third party updates are visible in the WSUS console. This option does not affect update applicability, deployment, or compliance in ConfigMgr. They only control WSUS console visibility.

When this option is selected, the Publisher marks the update so it is removed from view in the WSUS console.

> \*\*Note\*\*
>
> Hiding updates in WSUS is one effective way to help control the WSUS product category limit. Some third party vendors create a large number of locally published categories, and over time this can result in tens of categories being visible in the WSUS console. When the total number of locally published categories approaches or exceeds the Microsoft supported limit of 100, publishing and synchronization errors can occur.
>
> Using Hide in WSUS can reduce the number of locally published categories exposed in the WSUS console while still allowing ConfigMgr to manage the updates normally. This is a recommended mitigation when cleaning up unused vendors or when addressing errors related to too many locally published categories. For more information on the consequence and remediation of too many WSUS categories, see [https://patchmypc.com/kb/publish-error-too-many-locally-published-categories/](https://patchmypc.com/kb/publish-error-too-many-locally-published-categories/)

To hide one or more published updates in the WSUS console:

1. Locate and select the update or updates you want to hide in WSUS using the available filters.
2. Select **Hide in WSUS** at the bottom of the wizard. The Publisher sends the request to WSUS and displays a progress and confirmation window showing the result for each selected update.

![Hide Update(s) in WSUS](/_images/image-(203).png)

## Show Applicability Rules

The **Show Applicability Rules** option allows you to view the detection and applicability logic that determines whether an update is required on an endpoint or whether the update is already installed.

These rules are defined in the Patch My PC catalog and are published to WSUS as part of the update metadata. In a ConfigMgr environment, ConfigMgr evaluates these rules during software update scan cycles to determine applicability and compliance. In a WSUS standalone environment, WSUS clients evaluate the same rules locally to determine whether the update is applicable or already installed.

To view applicability rules for an update:

* Locate the update you want to view the applicability rules for by using the available filters. Select the checkbox next to the update you want to process.
* Select **Show Applicability Rules** at the bottom of the wizard. The Publisher sends the request to WSUS and displays a progress and confirmation window showing the result for each selected update.
* Review the results to confirm the action completed successfully, then select **Close** to exit the confirmation window.

![Show Applicability Rules](/_images/image-(204).png)

![Applicability Rules Example](/_images/image-(205).png)

> \*\*Note\*\*
>
> Not all third party updates display detailed applicability rules in this view. For MSP based updates, applicability is evaluated using MSI patch metadata rather than standard WSUS file, registry, or WMI detection rules.
>
> The MSI patch metadata defined in the catalog can be extensive and evaluates conditions such as target product codes, supported version ranges, and upgrade codes to determine whether the patch is applicable or already installed. Instead of displaying this extensive evaluation logic, the Publisher displays a placeholder labeled \*\*WSUS Generated MSP Rule.\*\*

## **More Details**

The **More Details** option opens an **Update Details** window for a selected update. This view exposes the underlying WSUS metadata for the update and is intended for validation and troubleshooting. The information shown here is read only and reflects exactly what was published to WSUS.

![More Details](/_images/image-(207).png)

This view is useful when confirming update identity, revision state, and metadata values that affect installation behavior.

The table below describes each field displayed in the Update Details window.

| Field           | Description                                                                                                                                |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Title           | The full update title as published to WSUS.                                                                                                |
| State           | The current WSUS processing state of the update. Ready indicates the update is fully processed and usable.                                 |
| Description     | The update description.                                                                                                                    |
| Information URL | A URL with additional information about the update.                                                                                        |
| Support URL     | A vendor provided support or documentation link.                                                                                           |
| Creation Date   | The date and time when this revision of the update's metadata was authored. The date is in Coordinated Universal Time.                     |
| Arrival Date    | The date and time when the metadata for this revision of the update finished downloading to the WSUS server                                |
| Classification  | The WSUS classification assigned to the update such as Updates or Security Updates.                                                        |
| Severity        | The severity level associated with the update when applicable.                                                                             |
| UpdateID        | The unique WSUS update identifier. Note: This value changes for republished updates.                                                       |
| Filename        | The primary file name associated with the update content.                                                                                  |
| Command Line    | The installation command line that WSUS and clients use to install the update.                                                             |
| CVE IDs         | Any CVE identifiers associated with the update.                                                                                            |
| Revision        | The WSUS revision number for the update. The revision increments when WSUS detects a change in the update metadata during synchronization. |
| Hash            | The content hash for the update. This value is shown in Base64 format and is used for content integrity validation.                        |
| Approved        | Indicates whether the update is approved in WSUS.                                                                                          |
| Declined        | Indicates whether the update is declined in WSUS.                                                                                          |
| Expired         | Indicates whether the update is expired in WSUS.                                                                                           |
| Superseded      | Indicates whether the update is superseded by another update.                                                                              |

> \*\*Note\*\*
>
> If the update includes customizations, the \*\*Filename\*\* is always \*\*PatchMyPC-ScriptRunner.exe\*\*. This indicates that the Script Runner is used to execute the customized installation logic.
>
> If no customizations are applied to the update in the Publisher, the original vendor provided installer filename is shown instead.

To view more details about an update:

1. Locate and select the update you want to view more details for for by using the available filters.
2. Select **More Details** at the bottom of the wizard. The Publisher sends the request to WSUS and displays a progress and confirmation window showing the result for each selected update.

![Update Details](/_images/image-(206).png)

## Extract Content

The **Extract Content** option allows you to export the WSUS content for a selected update to a local folder. This is typically used for troubleshooting, validation, or inspection of the update files that were published to WSUS.

To extract content for an update:

1. Locate and select the update you want extract content for for by using the available filters.
2. Select **Extract Content** at the bottom of the wizard.
3. In the Browse For Folder window, select an existing folder or create a new folder.
4. Select **OK** to begin extraction.

![Extract Content](/_images/image-(208).png)

> \*\*Tip\*\*
>
> The CAB file from the WSUS Content folder is copied to the folder specified in step 3. Typically, double clicking a CAB file in Windows Explorer displays the vendor installer binary along with any supporting Patch My PC files required to install a customized update.

## Re-Sign Update

The **Re-Sign Update** option allows you to re-sign an already published update using a new WSUS code signing certificate. This is typically required when the original code signing certificate has expired and timestamping was not enabled at the time the update was published.

> \*\*Important\*\*
>
> Timestamping keeps an update cryptographically valid after a code signing certificate expires. In WSUS standalone environments, re-signing may not be required, even if the certificate has expired, as long as the certificate is still present in the client Trusted Publishers certificate store.
>
> If ConfigMgr is configured to [manage certificates for third-party updates](https://learn.microsoft.com/en-us/intune/configmgr/sum/deploy-use/third-party-software-updates#configure-the-wsus-signing-certificate) it will block expired code signing certificates. During a Software Update Scan Cycle, ConfigMgr removes expired certificates from the Trusted Publishers store on clients. If the certificate is no longer present on the client device, updates signed with that certificate are not trusted, even if timestamping was enabled, and the updates must be re-signed.

> \*\*Important\*\*
>
> Re-signing changes the update content hash. Because of this, existing content already downloaded into ConfigMgr deployment packages is no longer valid.
>
> After updates are re signed, you must remove the old content and allow ConfigMgr to download the newly signed content.

![Re-sign Update](/_images/image-(209).png)

To re-sign an update

1. Locate and select the update you want to re-sign by using the available filtering options.
2. Select **Re-Sign Update** at the bottom of the wizard.
3. Review the warning message indicating that deployment package content must be deleted and redistributed. Select **OK** to continue, or **Cancel** to abort.
4. After re-signing completes, delete the affected updates from the ConfigMgr deployment package.
5. After a Software Update Point synchronization refreshes the update metadata, re-download the content to the deployment package. This can be done manually from the ConfigMgr console or automatically through an Automatic Deployment Rule, depending on how updates are managed in your environment.
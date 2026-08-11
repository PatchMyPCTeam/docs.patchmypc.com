# App Manager in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **ConfigMgr Application Manager** form control in Patch My PC (PMPC) Publisher is used to view and manage applications in ConfigMgr that were created using the Publisher. It provides a centralized interface to review application properties, deployments, task sequence usage and dependency relationships before performing application cleanup.

![ConfigMgr Application Manager](/_images/image-(94 "ConfigMgr Application Manager") (1).png>)

The form queries the ConfigMgr SMS Provider and displays only applications that were published by the Publisher.

The primary use case for this form is application cleanup. It allows administrators to identify unused applications, remove deployments, extract content, or delete applications in a controlled and supported manner.

> \*\*Note\*\*
>
> The Publisher relies on both the application XML representation stored in the ConfigMgr database and the associated content source folders to validate previous update versions and retained application chains. These components are evaluated together by the Publisher to ensure application retention and lifecycles are managed correctly.
>
> Removing an application directly from the ConfigMgr console deletes the console object but does not remove the corresponding content source folder from disk. This results in orphaned content remaining on disk. While the Publisher is designed to tolerate this condition, it is not the recommended cleanup approach.
>
> The ConfigMgr Application Manager is the preferred tool when performing application cleanup for Publisher created applications. It ensures that the ConfigMgr application object and the related content source paths are removed together, maintaining consistency between the console and the file system.

The table below outlines the available columns in this form:

<table><thead><tr><th width="145.111083984375" valign="top">Column name</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">Publisher</td><td valign="top">Displays the software vendor associated with the application as identified by the Publisher metadata.</td></tr><tr><td valign="top">Title</td><td valign="top">Shows the application name as it appears in the ConfigMgr console.</td></tr><tr><td valign="top">Version</td><td valign="top">Indicates the application version defined during publishing. This value is used by the Publisher to evaluate update ordering and supersedence.</td></tr><tr><td valign="top">Release Date</td><td valign="top">Displays the date the application was published (created) in ConfigMgr.</td></tr><tr><td valign="top">Deployments</td><td valign="top">Shows the number of active ConfigMgr deployments associated with the application.</td></tr><tr><td valign="top">Dependencies</td><td valign="top">Displays the number of dependency relationships where this application depends on another application.</td></tr><tr><td valign="top">Dependent DTs</td><td valign="top">Shows how many deployment types depend on this application. This indicates downstream usage that can block deletion.</td></tr><tr><td valign="top">Dependent TS</td><td valign="top">Displays the number of task sequences that reference this application.</td></tr><tr><td valign="top">Model Name</td><td valign="top">Displays the internal ConfigMgr CI Unique ID for the application. This value is primarily used for backend identification and troubleshooting.</td></tr></tbody></table>

> \*\*Note\*\*
>
> Applications referenced by task sequences cannot be deleted until those references are removed.

> \*\*Tip\*\*
>
> Highlighting a row in the application results table and pressing \*\*Ctrl + C\*\* will copy the entire row to the clipboard. This is useful for application management and troubleshooting scenarios.

## Search

The **Search** field is used to quickly filter results in the ConfigMgr Application Manager.

When application results are already displayed, the list is filtered automatically as you type. No additional action is required to apply the search.

The search evaluates all visible columns in the results grid. Matching results are shown dynamically based on the entered text.

Clearing the search field restores the full list of results.

## Refresh

The **Refresh** button refreshes the data from ConfigMgr to ensure the application information displayed is up-to-date.

## Select All / Select None

The **Select All** button selects every application currently visible in the list. This is commonly used when performing bulk actions such as deleting multiple applications.

The **Select None** button clears any current selection.

## Extract Content

The Extract Content button copies the source content of the selected applications to a folder. This action is commonly used to review, validate, or back up application files before making cleanup decisions in ConfigMgr.

Multiple applications can be selected at the same time using Ctrl plus click or Shift plus click. When multiple applications are selected, the Extract Content action processes each application in a single operation and stages the content together.

To extract the content for one or more published applications:

1. Locate the application or applications you want to extract the content for using the available filters. Select the checkbox next to each update you want to process.
2. Select **Extract Content** at the bottom of the wizard.

![Extact Content](/_images/image-(95 "Extact Content") (1).png>)

3. An output folder selection dialog is displayed. Review your selection choice and click **Browse** to choose a destination path for the extracted content.

> \*\*Note\*\*
>
> The destination must be a valid UNC path. If the specified folder does not exist, it will be automatically created.

![Content Extraction Summary](/_images/image-(96 "Content Extraction Summary") (1).png>)

4. Click **OK**.

After clicking OK, a summary dialog is displayed showing the results of the extraction operation. The dialog includes the total number of applications processed along with counts for successful, failed, and skipped items.

Clicking OK on the summary dialog automatically opens Windows Explorer to the specified output directory. This allows you to immediately review the extracted application content and confirm the files were copied as expected.

> \*\*Note\*\*
>
> Each application is written to its own subfolder within the selected destination, making it easier to inspect version specific files and determine whether the content should be retained or safely removed.
>
> Only applications with available source content can be extracted.
>
> If the destination folder does not already exist, it is created automatically during the extraction process.

## Delete Deployment(s)

The **Delete Deployment(s)** button removes all ConfigMgr deployments associated with the selected applications. This action does not delete the applications themselves.

The total number of deployments for each application is shown in the **Deployments** column. Reviewing this column before proceeding helps confirm the scope of the action.

Multiple applications can be selected at the same time using **Ctrl + Click** or **Shift + Click**. When multiple applications are selected, deployments for all selected applications are removed in a single operation.

To delete deployments for one or more applications:

1. Locate the application or applications whose deployments you want to remove by using the available filters. Select the checkbox next to each application.
2. Select **Delete Deployment(s)** at the bottom of the wizard.
3. When prompted, review the confirmation dialog and confirm that you want to remove all deployments for the selected applications.

After confirmation, the Publisher removes the deployments from ConfigMgr. The application objects and their content remain unchanged.

## Delete Application(s)

The **Delete Applications(s)** button deletes all the selected applications. Multiple applications can be selected at the same time using **Ctrl + Click** or **Shift + Click**.

To delete one or more applications:

1. Locate the application or applications you want to remove by using the available filters. Select the application(s) you want to delete.
2. Select **Delete Application(s)** at the bottom of the wizard.
3. When prompted, review the confirmation dialog and confirm that you want to remove all the selected applications.

After confirmation, the Publisher removes the selected applications from ConfigMgr and also the related content from disk.
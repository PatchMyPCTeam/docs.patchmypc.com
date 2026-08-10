# Intune Application Manager

_Applies to: Patch My PC Publisher V2.x_

## ![](/_images/image-(353).png>) Overview

The **Intune Application Manager** form control is used to view and manage Win32 apps (applications and updates) in Intune. It provides a centralized interface to review application properties, assignments and installation status before performing application modifications.

![Intune Application Manager](/_images/image-(4087).png "Intune Application Manager")

The form queries Intune, through Microsoft Graph, and displays all Win32 apps in the Intune tenant.

The primary use case for this form is application modification and cleanup. It allows administrators to identify unused applications, remove assignments, extract content, or delete applications in a controlled and supported manner.&#x20;

The table below outlines the available columns in this form:

| Column name            | Description                                                                                                       |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Name                   | Displays the application name as it appears in the Intune Admin Center.                                           |
| Description            | Shows the application description defined in Intune for the Win32 app.                                            |
| Publisher              | Displays the software vendor associated with the application as defined in Intune for the Win32 app.              |
| Device installs        | Shows the number of devices where the application is successfully installed.                                      |
| Device install pending | Shows the number of devices where installation is in progress or pending.                                         |
| Device not applicable  | Shows the number of devices where the application is not applicable based on requirements or applicability rules. |
| User installs          | Shows the number of user based installations associated with the application.                                     |
| Classification         | Displays whether the item is classified as an application or update in Intune.                                    |
| Modified               | Displays the date and time the application was last modified in Intune.                                           |
| Assigned               | Indicates whether the application has one or more assignments configured in Intune.                               |

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Highlighting a row in the application results table and pressing **Ctrl + C** will copy the entire row to the clipboard. This is useful for application management and troubleshooting scenarios.</p>
</blockquote>

## Search

The **Search** field is used to quickly filter results in the Intune Application Manager.

When application results are already displayed, the list is filtered automatically as you type. No additional action is required to apply the search.

The search evaluates all visible columns in the results grid. Matching results are shown dynamically based on the entered text.

Clearing the search field restores the full list of results.

## Show

The **Show** dropdown filters the applications displayed in the Intune Application Manager based on application type and origin. It allows you to quickly narrow the list to Win32 applications created or managed by the Publisher, or to view all applications regardless of source.

![Show](/_images/image-(4228).png "Show")

It primarily controls whether the grid shows Publisher managed Win32 apps, non Publisher apps, or both.

Options include:

* Show All
* Show All PMPC
* Show All PMPC Applications
* Show All PMPC Updates
* Show All Applications
* Show All Applications Except PMPC
* Show PMPC Custom Applications Only
* Show All Updates
* Show All Updates Except PMPC
* Show PMPC Custom Updates Only

This filter only changes what is visible in the grid. It does not modify applications in Intune.

## Refresh

The **Refresh** button refreshes the data to ensure the application information displayed is up-to-date.

## Select All / Select None

The **Select All** button selects every application currently visible in the list. This is commonly used when performing bulk actions such as deleting multiple applications.

The **Select None** button clears any current selection.

## Delete Application(s)

The **Delete Applications(s)** button deletes all the selected applications. Multiple applications can be selected at the same time using **Ctrl + Click** or **Shift + Click**.&#x20;

To delete one or more applications:

1. Locate the application or applications you want to remove by using the available filters. Select the application(s) you want to delete.
2. Select **Delete Application(s)** at the bottom of the wizard.
3. When prompted, review the confirmation dialog and confirm that you want to remove all the selected applications.

After confirmation, the Publisher removes the selected applications from Intune.

## Export

The **Export** button is used to export the currently displayed Intune Win32 application data to a CSV file.

1. Ensure application results are displayed in the Intune Application Manager.
2. Select **Export**.
3. Choose a destination location for the CSV file.
4. Select **Save** to complete the export.

The CSV file is created immediately and can be opened in tools such as Microsoft Excel or Power BI.

![PatchMyPC-IntuneAppManager.csv](/_images/image-(361).png "PatchMyPC-IntuneAppManager.csv")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The exported CSV can be used with the Patch My PC Power BI dashboard to monitor the compliance and deployment of applications and updates in Intune. For more information, see: <a href="https://patchmypc.com/kb/power-bi-reports-microsoft-intune/">https://patchmypc.com/kb/power-bi-reports-microsoft-intune/</a></p>
</blockquote>

## Right-Click Options

The Intune Application Manager provides several right click options that allow you to view information and perform actions against existing Win32 applications in your Intune tenant. These actions apply immediately and operate on live data in Intune.

### Manage DO Priority

This option allows you to configure Delivery Optimization (DO) priority for the selected application.

DO priority controls how quickly the content for an application is downloaded once the Intune Management Extension (IME) evaluates the policy. **Foreground** prioritises the download and processes the content immediately, while **Background** allows Windows to download the content with normal priority and defer based on network conditions and activity.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>For most Intune Updates, **Background** is an appropriate choice because the installation is typically not time-critical. When deploying Patch My PC applications during Autopilot, it is recommended to set DO to **Foreground**. This ensures faster content download and helps prevent delays to a user’s onboarding experience.</p>
</blockquote>

For more information about the various configuration options for assignments, see [Manage Assignments](../../../customizations-right-click-options/manage-assignments/).

### Manage ESP Associations

This option allows you to view and manage Enrollment Status Page associations for the selected application. It determines whether the application is required during device enrollment and ESP processing.

When you click this option, select the ESP profile you want the selected app(s) to be associated with.

![Manage ESP Associations](/_images/image-(4088).png "Manage ESP Associations")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Only classic ESP profiles are supported. This feature _does not_ apply to the newer Autopilot device preperation policies found in the Windows Autopilot configuration experience.</p>
</blockquote>

Once you have selected the profile(s), the **Select ESP Association** window displays a summary of the selected application and the ESP changes that will be applied.

![Select ESP Association](/_images/image-(4136).png "Select ESP Association")

The grid includes the following columns:

* **AppName**
  \
  The name of the selected application.
* **ESP to add**
  \
  The number of ESP profiles that the application will be added to.
* **ESP to remove (If enforced)**
  \
  The number of ESP profiles that will be removed if enforcement is enabled.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If the **Enforce selected ESP Association** checkbox is enabled, the Publisher will remove the application from any existing ESP profiles that are not part of the current selection.</p>
<p>If this option is not enabled, the application will only be added to the selected ESP profile and existing associations will remain unchanged.</p>
</blockquote>

For more information about the various configuration options for ESP associations, see [Manage ESP Profiles](../../../customizations-right-click-options/manage-esp-profiles.md).

### View Assignments

This option is available only when a single Win32 application is selected. Selecting this option opens the **Manage Application Assignments** window for the selected application.

This window provides a live view of all assignments currently configured for that application in Intune. The assignments shown reflect the current state in Intune, and any changes made are applied immediately when saved.

![Manage Application Assignments Form](/_images/image-(4089).png "Manage Application Assignments Form")

For more information about the various configuration options for assignments, see [Manage Assignments](../../../customizations-right-click-options/manage-assignments/).

#### View Installation Status

This option is available only when a single Win32 application is selected.

Selecting this option opens the Microsoft Intune admin center and navigates directly to the **Overview** page of the selected application. This provides access to device and user installation status, deployment health, and related monitoring information.

This action is read only and does not modify the application or its assignments. It is intended to provide quick access to installation status and troubleshooting information for the selected application.

### Show Categories

Selecting this option opens a read-only window and display any categories that are associated with the selected Win32 app(s).

![Show Categories](/_images/image-(4090).png "Show Categories")

For more information about the various configuration options for Categories, see [Manage Categories](../../../customizations-right-click-options/manage-categories.md).

### Extract Package

There is a configurable option in the Publisher, on the [Advanced ](../../advanced/)tab, to store the encryption keys used to create the Intune package files (.intunewin).

With the keys stored, you can use the Intune Application Manager to download and extract the content of the Patch My PC published Intune applications and updates.

Click **Extract Package** and specify an **Output Folder** where the package content will be extracted. You can enter a path directly or use **Browse** to select a location.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The destination must be a valid UNC path. If the specified folder does not exist, it will be automatically created.</p>
</blockquote>

![Extract Package](/_images/image-(4091).png "Extract Package")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If the **Extract Package** option is greyed out, it means that the encryption keys were not gathered when the Win32 app was published, likely due to the feature being enabled after the application or update had been published, or you have selected a Win32 app that was not created by the Publisher.</p>
</blockquote>

### Delete Assignment(s)

This option removes all assignments associated with the selected Win32 application(s). This action deletes Required, Available, and Uninstall assignments from Intune but does not delete the application itself.

This option supports multi select and is applied immediately after confirmation. It is useful when you need to quickly unassign applications from multiple groups without navigating through the Intune admin center.

### Delete Application(s)

This option deletes the selected Win32 application(s) from the Intune tenant. This action also removes any associated assignments and cannot be undone.

![Delete Application](/_images/image-(4229).png "Delete Application")

This option supports multi select and permanently removes the applications from Intune. It is intended for cleanup scenarios where applications are no longer required in the tenant.
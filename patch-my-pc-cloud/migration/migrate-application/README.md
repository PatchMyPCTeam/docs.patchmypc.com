# Migrate an Application from ConfigMgr to Intune using Patch My PC Cloud App Migration

_Applies to: Patch My PC Cloud_

There are three different types of application migrations we currently support in Patch My PC (PMPC) Cloud, depending on the results of the Migration scan:

* [Publish the App in Intune as a Suggested PMPC Catalog App](publish-migrated-app-suggested-app.md)
* [Publish the App in Intune as a PMPC Catalog App](publish-migrated-app-catalog-app.md)
* [Publish the App in Intune as a PMPC Custom App](publish-migrated-app-catalog-app-1.md)

> \*\*Important\*\*
>
> As detailed in \[Migration Requirements]\(../requirements.md), to use the \*\*Migrate\*\* button to perform the migration, your PMPC Cloud Company must be using an Enterprise Premium license.

The process for starting a migration is the same regardless of the type of target app that will be created in PMPC Cloud/Intune.

To perform a Migration:

1. Sign in to your PMPC Cloud Company.
2.  Navigate to **Migration**.<br>

    !\[Begin an application Migration from the Migration tab]\(/\_images/image-(3666).png "Begin an application Migration from the Migration tab")
3. Find the application you want to migrate.

![Select the application to migrate](../../../.gitbook/assets/image-\(3670\).png)

> \*\*Tip\*\*
>
> You can use the \*\*Search\*\* box and start typing the name of the application to help you find it.
>
> Alternatively, click the filter button and select the checkbox next to the \*\*Match Type\*\* of the application you wish to migrate (\*\*PMPC App\*\* or \*\*Custom App\*\*). Then, click \*\*Apply All Filters\*\* to view only the matching applications.

4. If a warning triangle is not present in the **Info** column for the application, go to step 11.
5.  If a warning triangle is shown in the **Info** column, click it to open the application's properties.<br>

    ![Understand if the migration will not include some properties](../../../.gitbook/assets/image-\(3672\).png)
6.  In the application's properties, locate the tab(s) with a warning triangle beside them.<br>

    ![Read and understand any warnings about the application to be migrated](../../../.gitbook/assets/image-\(3673\).png)
7. Click the relevant tab and look for the items with the warning triangle beside them.
8. Review the warning and determine your course of action.
9. If you are happy to proceed with the migration, go to step 11.
10. If you cannot proceed with the migration, close the application's properties and click **Cancel** to close the **Migration Wizard**. You now need to assess how to address the warnings to determine your next course of action for this application.

![Click the Migrate button](../../../.gitbook/assets/image-\(3675\).png)

11. The behavior of the **Migrate** button depends on both the application **Match Type** and the **Migrate button** state shown in the UI. The image below highlights two possible Migrate button states:

    * **Button State 1 – Single Migrate button**\
      Clicking **Migrate** immediately starts the migration wizard.
    * **Button State 2 – Migrate button with dropdown**\
      Clicking **Migrate** displays additional options, allowing you to choose how the application should be migrated.

    ![Migrate Button State](../../../.gitbook/assets/image-\(3788\).png)

    Use the following sections to determine which action to take based on the application’s **Match Type** and the **Migrate** button state shown:

* [Match Type: Catalog App, Button State = 1](./#match-type-catalog-app-button-state-1)
* [Match Type: Custom App, Button State = 1](./#match-type-custom-app-button-state-1)
* [Match Type: Custom App, Button State = 2](./#match-type-custom-app-button-state-2)

### **Match Type: Catalog App, Button State = 1**

If the application is identified as a **Catalog App**, click **Migrate** and follow the [Publish the App in Intune as a PMPC Catalog App](publish-migrated-app-catalog-app.md) process.

### **Match Type: Custom App, Button State = 1**

If the application is identified as a PMPC Custom App and no alternative catalog match is available, the migration will proceed directly as a custom app. Click **Migrate** and follow the [Publish the App in Intune as a PMPC Custom App](publish-migrated-app-catalog-app-1.md) process.

### **Match Type: Custom App, Button State = 2**

If the application is identified as a **Custom App**, but a potential catalog match was identified based on application metadata instead of the file hash, the drop-down menu will present two options:

![two options in the dropdown if a potential catalog match was identified based on application metadata instead of the file hash, the drop-down menu](../../../.gitbook/assets/image-\(3790\).png)

* **Match to Catalog App -** Select this to migrate the application using the suggested catalog match and follow the [Publish the App in Intune as a Suggested PMPC Catalog App](publish-migrated-app-suggested-app.md) process.
* **Create a Custom App -** Select this to migrate the application as a PMPC Custom App and follow the [Publish the App in Intune as a PMPC Custom App](publish-migrated-app-catalog-app-1.md) process.

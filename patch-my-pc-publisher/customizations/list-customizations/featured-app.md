# Featured App option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: Product_
\
_Available on tab: ConfigMgr Apps, Intune Apps_

The **Featured App** right-click option in Patch My PC (PMPC) Publisher allows you to mark an application as **featured**, making it more prominent and easier for users to discover in both the Microsoft ConfigMgr Software Center and Intune Company Portal.&#x20;

Featured applications are typically highlighted or surfaced more prominently, which is useful for recommended apps, commonly used tools, or newly introduced software.

When enabled, Publisher automatically configures the appropriate setting on the application in the target platform when it publishes or updates the app.

For ConfigMgr apps, this option automatically enables the following checkbox on the **Software Center** tab of the application:

**Display this as a featured app and highlight it in the Company Portal and Software Center**&#x20;

!['Display this as a featured app and highlight it in the Company Portal and Software Center' checkbox](/_images/image-(100).png "&#x27;Display this as a featured app and highlight it in the Company Portal and Software Center&#x27; checkbox")

For Intune apps, this option automatically sets the **Show this as a featured app setting** to **Yes** for the Win32 application.

!['Show this as a featured app' setting](/_images/image-(101).png "&#x27;Show this as a featured app&#x27; setting")

The setting is applied during the next Publisher sync for newly created or updated applications.
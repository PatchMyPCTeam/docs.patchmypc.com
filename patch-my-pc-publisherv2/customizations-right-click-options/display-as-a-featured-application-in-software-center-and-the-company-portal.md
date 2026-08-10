# Display as a featured application in Software Center and the Company Portal

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: Product_
\
_Available on tab: ConfigMgr Apps, Intune Apps_

This option allows you to mark an application as **featured**, making it more prominent and easier for users to discover in both **ConfigMgr Software Center** and the **Intune Company Portal**.&#x20;

![Display as a featured application in Software Center and the Company Portal](/_images/image-(99).png "Display as a featured application in Software Center and the Company Portal")

Featured applications are typically highlighted or surfaced more prominently, which is useful for recommended apps, commonly used tools, or newly introduced software.

When enabled, the Publisher automatically configures the appropriate setting on the application in the target platform during publish or update.

For ConfigMgr apps, this option automatically enables the Featured checkbox on the Software Center tab of the application.

![Display as a featured application in Software Center](/_images/image-(100).png "Display as a featured application in Software Center")

For Intune apps, this option automatically enablesShow this as a featured app to Yes for the Win32 application.

![Show this as a featured app](/_images/image-(101).png "Show this as a featured app")

The setting is applied during the next Publisher sync for newly created or updated applications.
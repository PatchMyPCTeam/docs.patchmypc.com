# Display as a featured application in Software Center and the Company Portal

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: Product_\
_&#x41;vailable on tab: ConfigMgr Apps, Intune Apps_

This option allows you to mark an application as **featured**, making it more prominent and easier for users to discover in both **ConfigMgr Software Center** and the **Intune Company Portal**.

![Display as a featured application in Software Center and the Company Portal](../../.gitbook/assets/image-\(99\).png)

Featured applications are typically highlighted or surfaced more prominently, which is useful for recommended apps, commonly used tools, or newly introduced software.

When enabled, the Publisher automatically configures the appropriate setting on the application in the target platform during publish or update.

For ConfigMgr apps, this option automatically enables the Featured checkbox on the Software Center tab of the application.

![Display as a featured application in Software Center](../../.gitbook/assets/image-\(100\).png)

For Intune apps, this option automatically enablesShow this as a featured app to Yes for the Win32 application.

![Show this as a featured app](../../.gitbook/assets/image-\(101\).png)

The setting is applied during the next Publisher sync for newly created or updated applications.

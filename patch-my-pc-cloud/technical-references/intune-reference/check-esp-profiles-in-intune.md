# Check ESP Profiles in Intune

_Applies to: Microsoft Intune_

If a Patch My PC (PMPC) Cloud deployment has been configured to use [ESP Profiles](../../deployments/deploy-app/configurations-tab/additional-tools/esp-profiles.md), this is how you can check the deployment(s) has been added to the correct ESP Profile in Intune:

1. Sign in to the **Intune admin center**
2.  Navigate to **Devices**<br>

    ![Navigating to "Devices"](../../../.gitbook/assets/image-\(828\).png)
3.  Navigate to **Enrollment**<br>

    ![Navigating to "Enrollment"](../../../.gitbook/assets/image-\(978\).png)
4.  Scroll down and select **Enrollment Status Page**<br>

    ![Scrolling down and selecting "Enrollment Status Page"](../../../.gitbook/assets/image-\(979\).png)
5.  On the **Enrollment Status Page** click the relevant profile the PMPC Cloud deployment has been added to.<br>

    ![Clicking the relevant profile the PMPC Cloud deployment has been added to](../../../.gitbook/assets/image-\(980\).png)
6.  On the _**\<profile\_name>**_ page, navigate to **Manage | Properties**<br>

    ![Navigating to "Manage | Properties"](../../../.gitbook/assets/image-\(981\).png)
7.  Scroll down to the **Block device use until required apps are installed if they are assigned to the user/device** field. This shows the apps that must be installed before the user can use the device and will include the PMPC Cloud deployment if it was configured correctly.<br>

    ![Scrolling down to the "Block device use until required apps are installed if they are assigned to the user/device field", which shows the apps that must be installed before a user can use the device](../../../.gitbook/assets/image-\(982\).png)

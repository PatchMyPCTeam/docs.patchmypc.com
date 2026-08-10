# Check ESP Profiles in Intune

_Applies to: Microsoft Intune_

If a Patch My PC (PMPC) Cloud deployment has been configured to use [ESP Profiles](../../deployments/deploy-app/configurations-tab/additional-tools/esp-profiles.md), this is how you can check the deployment(s) has been added to the correct ESP Profile in Intune:

1. Sign in to the **Intune admin center**
2.  Navigate to **Devices**<br>

    ![Navigating to "Devices"](/_images/image-(828).png "Navigating to “Devices”")
3.  Navigate to **Enrollment**<br>

    ![Navigating to "Enrollment"](/_images/image-(978).png "Navigating to “Enrollment”")


4.  Scroll down and select **Enrollment Status Page**<br>

    ![Scrolling down and selecting "Enrollment Status Page"](/_images/image-(979).png "Scrolling down and selecting “Enrollment Status Page”")


5.  On the **Enrollment Status Page** click the relevant profile the PMPC Cloud deployment has been added to.<br>

    ![Clicking the relevant profile the PMPC Cloud deployment has been added to](/_images/image-(980).png "Clicking the relevant profile the PMPC Cloud deployment has been added to")


6.  On the _**\<profile\_name>**_ page, navigate to **Manage | Properties**<br>

    ![Navigating to "Manage | Properties"](/_images/image-(981).png "Navigating to “Manage | Properties”")


7.  Scroll down to the **Block device use until required apps are installed if they are assigned to the user/device** field. This shows the apps that must be installed before the user can use the device and will include the PMPC Cloud deployment if it was configured correctly.<br>

    ![Scrolling down to the "Block device use until required apps are installed if they are assigned to the user/device field", which shows the apps that must be installed before a user can use the device](/_images/image-(982).png "Scrolling down to the “Block device use until required apps are installed if they are assigned to the user/device field”, which shows the apps that must be installed before a user can use the device")
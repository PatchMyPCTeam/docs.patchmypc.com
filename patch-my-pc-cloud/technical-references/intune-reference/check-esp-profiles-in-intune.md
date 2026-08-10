# Check ESP Profiles in Intune

_Applies to: Microsoft Intune_

If a Patch My PC (PMPC) Cloud deployment has been configured to use [ESP Profiles](../../deployments/deploy-app/configurations-tab/additional-tools/esp-profiles.md), this is how you can check the deployment(s) has been added to the correct ESP Profile in Intune:

1. Sign in to the **Intune admin center**
2.  Navigate to **Devices**<br>

    <figure><img src="../../../.gitbook/assets/image (828).png" alt="Navigating to “Devices”"><figcaption></figcaption></figure>
3.  Navigate to **Enrollment**<br>

    <figure><img src="../../../.gitbook/assets/image (978).png" alt="Navigating to “Enrollment”"><figcaption></figcaption></figure>


4.  Scroll down and select **Enrollment Status Page**<br>

    <figure><img src="../../../.gitbook/assets/image (979).png" alt="Scrolling down and selecting “Enrollment Status Page”"><figcaption></figcaption></figure>


5.  On the **Enrollment Status Page** click the relevant profile the PMPC Cloud deployment has been added to.<br>

    <figure><img src="../../../.gitbook/assets/image (980).png" alt="Clicking the relevant profile the PMPC Cloud deployment has been added to"><figcaption></figcaption></figure>


6.  On the _**\<profile\_name>**_ page, navigate to **Manage | Properties**<br>

    <figure><img src="../../../.gitbook/assets/image (981).png" alt="Navigating to “Manage | Properties”"><figcaption></figcaption></figure>


7.  Scroll down to the **Block device use until required apps are installed if they are assigned to the user/device** field. This shows the apps that must be installed before the user can use the device and will include the PMPC Cloud deployment if it was configured correctly.<br>

    <figure><img src="../../../.gitbook/assets/image (982).png" alt="Scrolling down to the “Block device use until required apps are installed if they are assigned to the user/device field”, which shows the apps that must be installed before a user can use the device"><figcaption></figcaption></figure>

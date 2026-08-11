# Why is the “Deploy” button greyed out in Cloud?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

Why when I try to deploy an app, is the **Deploy** button greyed out?

!["Deploy" button greyed out.](../../../.gitbook/assets/image-\(3044\).png)

### CAUSE

This can be caused if you add the **UpdateOnly** assignment type to a deployment that is configured to use an [ESP Profile](../../deployments/deploy-app/configurations-tab/additional-tools/esp-profiles.md) which is unsupported in Intune. If you look at the **Configurations** tab it will show a read "**X**" highlighting the configuration conflict.

### RESOLUTION

To resolve this issue:

1.  Click the **Configurations** page of the deployment.<br>

    ![Clicking the "Configurations" page](../../../.gitbook/assets/image-\(3077\).png)

    \
    If the problem is caused by an ESP Profile being configured, the **ESP Profiles** tab will be automatically opened.<br>

    !["ESP Profile" tab automatically opened](../../../.gitbook/assets/image-\(3046\).png)
2.  Scroll down to the **ESP Profiles** section, under which you will see the following message:<br>

    **ESP profiles should be empty when the assignments list contains only UpdateOnly assignments.**<br>

    !["ESP profiles should be empty when the assignments list contains only UpdateOnly assignments." message](../../../.gitbook/assets/image-\(3047\).png)
3.  You now need to decide whether you:

    a. Remove the **UpdateOnly** assignment

    b. Change this deployment to not use any ESP Profiles.\
    \
    Either of these options will enable the **Deploy** button.

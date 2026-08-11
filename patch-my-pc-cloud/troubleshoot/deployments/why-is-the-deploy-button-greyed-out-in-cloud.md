# Why is the “Deploy” button greyed out in Cloud?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

Why when I try to deploy an app, is the **Deploy** button greyed out?

<figure><img src="../../../.gitbook/assets/image (3044).png" alt="“Deploy” button greyed out."><figcaption></figcaption></figure>

### CAUSE

This can be caused if you add the **UpdateOnly** assignment type to a deployment that is configured to use an [ESP Profile](../../deployments/deploy-app/configurations-tab/additional-tools/esp-profiles.md) which is unsupported in Intune. If you look at the **Configurations** tab it will show a read "**X**" highlighting the configuration conflict.

### RESOLUTION

To resolve this issue:

1.  Click the **Configurations** page of the deployment.<br>

    <figure><img src="../../../.gitbook/assets/image (3077).png" alt="Clicking the “Configurations” page"><figcaption></figcaption></figure>

    \
    If the problem is caused by an ESP Profile being configured, the **ESP Profiles** tab will be automatically opened.<br>

    <figure><img src="../../../.gitbook/assets/image (3046).png" alt="“ESP Profile” tab automatically opened"><figcaption></figcaption></figure>


2.  Scroll down to the **ESP Profiles** section, under which you will see the following message:<br>

    **ESP profiles should be empty when the assignments list contains only UpdateOnly assignments.**<br>

    <figure><img src="../../../.gitbook/assets/image (3047).png" alt="“ESP profiles should be empty when the assignments list contains only UpdateOnly assignments.” message"><figcaption></figcaption></figure>


3.  You now need to decide whether you:

    a. Remove the **UpdateOnly** assignment

    b. Change this deployment to not use any ESP Profiles.\
    \
    Either of these options will enable the **Deploy** button.

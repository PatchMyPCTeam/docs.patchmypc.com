# Why is an app not shown in the “App Dependencies” dropdown in Cloud?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to use the _App Dependencies_ feature of Patch My PC (PMPC) Cloud, but when I click on the **App Dependencies** dropdown, I do not see the app I need to ensure is installed on the device before the app I am trying to deploy.

<figure><img src="../../../.gitbook/assets/image (2274).png" alt="Required app missing from the “App Dependencies” dropdown"><figcaption></figcaption></figure>

### CAUSE

This problem can be caused if the app you are trying to create the dependency with (i.e., the one that needs to be installed before the app you are trying to deploy) has:

* not already been deployed
* not been deployed successfully. Only apps with a Success status will be shown
* only Update Only or Uninstall assignments.

### RESOLUTION

To resolve this issue, ensure that the app you are trying to create the dependency with (i.e., the one that needs to be installed before the app you are trying to deploy) has:

* Been deployed successfully.
* Has at least Available or Required assignment.

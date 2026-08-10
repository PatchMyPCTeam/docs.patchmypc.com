# Check App Version Retention in Intune

_Applies to: Microsoft Intune_

If a Patch My PC (PMPC) Cloud deployment has been configured to use a [Retention Policy](../../deployments/deploy-app/configurations-tab/additional-tools/retention-policy.md), this is how you can check that the relevant number of versions have been created correctly in Intune:

1. Sign in to the **Intune admin center**
2. Navigate to **Apps**

![Navigating to "Apps"](/_images/image-(3281).png "Navigating to “Apps”")

3. Navigate to **All Apps**

![Navigating to "All Apps"](/_images/image-(3282).png "Navigating to “All Apps”")

You will see all versions of all apps deployed.

In the following example, 7-Zip has been deployed with a **Retention Policy** of **2**. So the latest version (23.01) is kept as it is the previous two versions (19.00 and 16.04). The next time a new version is deployed, the new version will be added and version 16.04 deleted.

![List of apps deps deployed](/_images/image-(3283).png "List of apps deps deployed")
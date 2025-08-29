# Check App Version Retention in Intune

_Applies to: Microsoft Intune_

If a Patch My PC (PMPC) Cloud deployment has been configured to use a [Retention Policy](../../cloud-deployments/deploying-an-app-using-cloud/cloud-configurations-deployment-tab/retention-policy-deployments.md), this is how you can check that the relevant number of versions have been created correctly in Intune:

1. Sign in to the **Intune admin center**
2. Navigate to **Apps**

<figure><img src="../../../_images/gitbook/image (2579).png" alt="Navigating to “Apps”" width="563"><figcaption></figcaption></figure>

3. Navigate to **All Apps**

<figure><img src="../../../_images/gitbook/image (2580).png" alt="Navigating to “All Apps”" width="563"><figcaption></figcaption></figure>

You will see all versions of all apps deployed.

In the following example, 7-Zip has been deployed with a **Retention Policy** of **2**. So the latest version (23.01) is kept as it is the previous two versions (19.00 and 16.04). The next time a new version is deployed, the new version will be added and version 16.04 deleted.

<figure><img src="../../../_images/gitbook/image (2581).png" alt="List of apps deps deployed" width="563"><figcaption></figcaption></figure>

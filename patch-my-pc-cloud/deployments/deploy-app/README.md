# Deploy an App using Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Patch My PC (PMPC) Cloud can be used to deploy apps using Microsoft Intune.

> \*\*Note\*\*
>
> You can also:
>
> \* \[Deploy the same App with multiple configurations]\(../technical-references/deploy-same-app.md)
>
> \* \[Create a Deployment with No Assignments]\(../technical-references/deployment-without-assignments.md).

To deploy an app using PMPC Cloud:

1. Sign in to the portal at [https://portal.patchmypc.com/](https://portal.patchmypc.com/)
2. Locate the required application on the **App Catalog** page.

> \*\*Tip\*\*
>
> Use the \*\*Search\*\* field to help you locate the app.

!["App Catalog" page](../../../.gitbook/assets/image-\(895\).png)

> \*\*Note\*\*
>
> If an app (for example, the Windows version of Slack) has multiple versions available for different variants/installer types, the App Catalog shows the total number of available versions. If you hover your mouse over this, you can see the list of variants grouped accordingly. Only that version will be displayed if a single version is available for all variants.
>
> !\[Total number of available variants]\(/\_images/image-(3173 "Total number of available variants").png>)

3.  Click the app to open its properties.<br>

    ![Application's "Properties" page](../../../.gitbook/assets/image-\(896\).png)
4. Click **Deploy** to start the Deployment Wizard.

> \*\*Note\*\*
>
> If the app you are deploying is also supported for macOS, you will see a separate \*\*Deploy\*\* option for \*\*macOS\*\* and you should follow the \[Deploy a macOS app]\(../../macos-support/deploy-macos-app.md) process.
>
> Also, if the app you are deploying is already published by our on-premises Publisher, you will see the \*\*This app is already deployed\*\* warning dialog stating that deploying the same app through both Publisher and PMPC Cloud can cause potential issues if there are differences between the deployment configurations. We therefore strongly recommend you only deploy an app through either Publisher PMPC Cloud to avoid such issues.

![Click "Deploy" to start the Deployment Wizard](../../../.gitbook/assets/image-\(897\).png)

The [General Information](general-information-tab.md) tab is displayed, which needs to be completed.

> \*\*Note\*\*
>
> Once the Deployment Wizard starts, the \*\*Apply Template\*\* button becomes available, which allows you to apply any \[Deployment Templates]\(../use-template.md) you have created that contain preconfigured settings to your deployments.

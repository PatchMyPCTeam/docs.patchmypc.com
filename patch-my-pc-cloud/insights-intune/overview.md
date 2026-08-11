# Overview of Patch My PC Advanced/Patch Insights for Intune

_Applies to: Advanced/Patch Insights for Intune_

The _Advanced/Patch Insights for Intune_ feature of Patch My PC (PMPC) Cloud allows you to see a wealth of information about your organization that you can use to monitor, maintain, and enhance your environment.

Your PMPC Cloud license type determines the name of the node in your portal:

* [Advanced Insights](overview.md#advanced-insights)
* [Patch Insights](overview.md#patch-insights)

## Advanced Insights

If you are either using an Enterprise Premium license or you are an Enterprise Plus customer who has [signed up for an Enterprise Premium Trial](../manage/settings/company-settings/sign-up-enterprise-premium-trial.md), the node will be named **Advanced Insights**, which allows you to perform both reporting on your Intune tenant, plus any devices running the PMPC Client.

The **Advanced Insights** node consists of the following sub-nodes, each of which contains the most common datasets organizations typically want to report on:

* **Home -** Contains a summary of all of the information from the other tabs.
* **Updates -** Contains a summary of the most common software update-related information.
* **Hardware -** Contains a summary of the most common hardware-related information.
* **Intune -** Contains a summary of the most common information from your Intune tenant.

!['Advanced Insights' node](<../../.gitbook/assets/image-(574) (1).png>)

## Patch Insights

If you are using the Enterprise Plus license, the node will be named **Patch Insights**, which allows you to perform just reporting on your Intune tenant.

You can only access the **Intune** sub-node, which contains a summary of the most common information from your Intune tenant.

!['Patch Insights' node](<../../.gitbook/assets/image-(577) (1).png>)

> \*\*Note\*\*
>
> You will see the other sub-nodes available for \*\*Advanced Insights\*\*, but you will be unable to access them unless you upgrade your license to an Enterprise Premium license or \[sign up for an Enterprise Premium Trial]\(../manage/settings/company-settings/sign-up-enterprise-premium-trial.md).

> \*\*Important\*\*
>
> The data in the \*\*Intune\*\* sub-node is populated using Microsoft Graph calls to your Intune tenant.
>
> For data to appear and update in the other sub-nodes, you need to install our client on any devices you wish to collect data from. See \[Patch My PC Client]\(../../patch-my-pc-client/) for more information.

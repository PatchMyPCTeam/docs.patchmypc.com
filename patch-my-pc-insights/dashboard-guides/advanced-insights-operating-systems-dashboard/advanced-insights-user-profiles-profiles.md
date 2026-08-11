---
description: User profiles inventoried on client devices
---

# Advanced Insights "User Profiles" Profiles

_Applies to: Patch My PC Advanced Insights_

> The User Profiles data on this page requires the deployment of the \[Advanced Insights Inventory Extensions]\(../../advanced-insights-inventory-extensions/)
>
> The Delete user profile button on this page requires the Approval of the run Script \[Advanced Insights Client Actions]\(../../advanced-insights-inventory-extensions/insights-custom-client-actions.md#script-approval)

![](../../../.gitbook/assets/image-\(2873\).png)

The User profiles dashboard is data collected from the Inventory Extensions. Here we are able to display information on:

* Aged Profiles - Users profiles with last logon greater than or equal to 90 days.
* Unknown Age Profiles - User profiles with no last logon date data.
* Orphaned User Profiles - User profiles with no associated user account.
* Conflicting Paths - User profiles on the same device that share the same user profile path.

![](../../../.gitbook/assets/image-\(2876\).png)

On each of these reports you will be able to see the Computer name, Account name, Last logged in date, Age and Size of the user profile.

The donut chart breaks down profiles based on size on disk.

![](../../../.gitbook/assets/image-\(2875\).png)

The User Profiles chart gives you a full list of inventoried user profiles on client devices but also you have the ability to delete a users profile from a device too.

> Each profile entry includes a \*\*Delete\*\* button, allowing administrators to remove a user profile from the device entirely.
>
> \*\*Warning\*\*: This action permanently deletes the local user profile, including all associated files and settings, from the device.

![](../../../.gitbook/assets/image-\(2878\).png)

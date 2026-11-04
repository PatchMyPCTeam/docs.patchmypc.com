# Patch Insights for Managed Service Provider users of Patch My PC Cloud

_Applies to: Patch My PC (PMPC) Cloud and Patch Insights for Intune_

{% hint style="danger" %}
**Public Preview**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

Patch My PC (PMPC) Cloud customers with a Managed Service Provider (MSP) Plus subscription now have access to [Patch Insights for Intune](../insights-intune/).

## Requirements

To gain access to Patch Insights as an MSP requires:

* An MSP Plus subscription.
* The parent MSP company to have an Intune connection to the Intune tenant you wish to report on.

## Using Patch Insights as an MSP

Once the _Advanced Internet Reporting_ feature is enabled, the **Patch Insights** node appears in the Cloud Portal.

You can then use the features of [Patch Insights](../insights-intune/).

To grant new users access to Patch Insights, create an [invitation](../manage/settings/users/add-user.md#invitation-from-an-administrator) for the user that grants them the **Read-Only Report Admin** user role.

For an existing user, grant them the **Read-Only Report Admin** user role.

An administrator at the parent MSP company can switch to a child company and view reports only for that child company, provided the child company has its own Intune connection and the reporting feature is enabled for the child company.

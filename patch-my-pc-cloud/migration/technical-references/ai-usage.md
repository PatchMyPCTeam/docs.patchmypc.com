# Artificial Intelligence Usage in ConfigMgr to Intune App Migration using Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Artificial Intelligence (AI) capabilities are available in the Patch My PC (PMPC) Cloud Portal to enhance the application migration experience.

When migrating PSADT-based applications, AI is used to assist with parsing the PowerShell script and identifying key components such as the primary installer, pre-script logic, and post-script logic. This helps improve migration accuracy, particularly for more complex scripts.

In some cases, automated parsing may fail, especially where PSADT scripts have been heavily customized or deviate from common structures. The use of AI is intended to improve script interpretation in these scenarios and significantly increase the number of applications that can be successfully migrated.

{% hint style="info" %}
**Note**

AI usage is optional and can be disabled at any time from the Cloud Portal settings. See [Manage Cloud AI Usage](../../manage/settings/company-settings/ai-usage.md) for more details.
{% endhint %}

{% hint style="danger" %}
**Important**

AI usage is automatically enabled for new customers when the Migration feature is first configured. For early access customers onboarded to the migration feature before December 17th, 2025, AI usage was not enabled automatically and must be enabled explicitly.
{% endhint %}

For more information on how AI is used in the Cloud Portal, including common FAQs, see the [Patch My PC Trust Center](https://trust.patchmypc.com/faq).

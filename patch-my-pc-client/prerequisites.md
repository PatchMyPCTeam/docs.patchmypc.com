# Patch My PC Client Prerequisites

_Applies to: Patch My PC Client_

The Patch My PC (PMPC) Client has the following Prerequisites:

* You must use the PMPC Portal, and it must be connected to your Intune tenant.
* Your PMPC company must be connected to the same Intune tenant used to manage the devices from which you want to gather reporting data.
* You need to use PMPC Cloud to deploy and manage your third-party apps, updates, and Custom Apps.
* For a PMPC Client to appear in the [Microsoft](../patch-my-pc-cloud/insights-intune/about-dashboards/updates-page.md#microsoft) tab of the [Updates](../patch-my-pc-cloud/insights-intune/about-dashboards/updates-page.md) dashboard, it needs to be opted into Microsoft Updates.
* If you have TLS encryption enabled on your endpoints, you need to bypass the following:

<table><thead><tr><th width="217" valign="top">Domain</th><th width="249.99993896484375" valign="top">Reason</th><th width="69.00006103515625" valign="top">Port</th><th width="115.33331298828125" valign="top">Protocol</th></tr></thead><tbody><tr><td valign="top">portal.patchmypc.com</td><td valign="top">Client enrollment/Region discovery</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">*.patchmypc.com</td><td valign="top">Client communication</td><td valign="top">443</td><td valign="top">https</td></tr></tbody></table>

* Configure an **allow** rule on your firewall for the following:

<table><thead><tr><th width="216.99993896484375" valign="top">Domain</th><th width="249.99993896484375" valign="top">Reason</th><th width="69.00006103515625" valign="top">Port</th><th width="115.33331298828125" valign="top">Protocol</th></tr></thead><tbody><tr><td valign="top">*.portal.patchmypc.com</td><td valign="top">Client enrollment/Region discovery</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">us.portal.patchmypc.com</td><td valign="top">Client communication</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">eu.portal.patchmypc.com</td><td valign="top">Client communication</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">api.patchmypc.com</td><td valign="top">Client communication</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">*.digicert.com</td><td valign="top">CRL checking</td><td valign="top">80</td><td valign="top">http</td></tr></tbody></table>

{% hint style="danger" %}
**Important**

Wildcard entries in this article do not cover apex hosts.
{% endhint %}

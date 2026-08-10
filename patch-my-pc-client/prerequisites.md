# Patch My PC Client Prerequisites

_Applies to: Patch My PC Client_

The Patch My PC (PMPC) Client has the following Prerequisites:

* You need to be using the PMPC Portal, and it needs to be connected to your Intune tenant.
* Your PMPC company needs to be connected to the same Intune tenant that is used to manage the devices from which you want to gather your reporting data.
* You need to use PMPC Cloud to deploy and manage your third-party apps, updates, and Custom Apps.
* If you have TLS encryption enabled on your endpoints, you need to allow:\
  **\*.patchmypc.com**
* Configure an **allow** rule on your firewall for the following:

<table><thead><tr><th width="208.111083984375" valign="top">Domain</th><th width="197.77777099609375" valign="top">Reason</th><th width="85.66668701171875" valign="top">Port</th><th width="115.33331298828125" valign="top">Protocol</th></tr></thead><tbody><tr><td valign="top">*.digicert.com</td><td valign="top">CRL checking</td><td valign="top">80</td><td valign="top">http</td></tr><tr><td valign="top">*.portal.patchmypc.com</td><td valign="top">Client communication</td><td valign="top">443</td><td valign="top">https</td></tr><tr><td valign="top">api.patchmypc.com</td><td valign="top">Client communication</td><td valign="top">443</td><td valign="top">https</td></tr></tbody></table>

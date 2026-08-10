# Deploy the Patch My PC Client

_Applies to: Patch My PC Client_

To deploy the Patch my PC (PMPC) Client:

1. Navigate to **Settings | Deploy Client**

<figure><img src="../../.gitbook/assets/image (593).png" alt="Navigating to &#x27;Settings | Deploy Client&#x27;" width="563"><figcaption></figcaption></figure>

The **Deploy Client** screen is shown, which is split into two sections:

* **Preview Version Deployment –** Shows details of the preview version of our Client and which Entra ID groups it is targeted to (if relevant).
* **Production Version Deployment -** Shows details of the production version of our Client and which Entra ID groups it is targeted to (if relevant).

<figure><img src="../../.gitbook/assets/image (594).png" alt="&#x27;Deploy Client Deployment&#x27; screen" width="563"><figcaption></figcaption></figure>

2. To deploy the Client (**Preview** or **Production**), click the **Groups** dropdown and select the relevant Entra ID group(s) you want to deploy the Client to.

{% hint style="danger" %}
**Important**

Please ensure that:

* Any devices you plan to install the PMPC Client on meet the [PMPC Client Supported configurations](../supported-configurations.md).
* You use one Entra ID group to target the installation of the Preview version of the Client and a separate group to target the installation of the Production version.
* You do not have the same devices in the Entra ID groups being used to target the installation of the Preview and Production versions of the Client.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (595).png" alt="Selecting the Entra ID Group(s) you want to deploy the client to" width="563"><figcaption></figcaption></figure>

3. Click **Save**

<figure><img src="../../.gitbook/assets/image (596).png" alt="Clicking &#x27;Save&#x27;" width="563"><figcaption></figcaption></figure>

The **Success - Created** notification is shown.

<figure><img src="../../.gitbook/assets/image (603).png" alt="&#x27;Success – Created&#x27; notification" width="563"><figcaption></figcaption></figure>

Once the Win32 app for the Client has been created in Intune, the status updates to **Success** and the Client will be deployed to the targeted devices.

<figure><img src="../../.gitbook/assets/image (592).png" alt="Client deployed successfully" width="563"><figcaption></figcaption></figure>

As the Client is installed on the targeted devices, the number of **Devices Managed** shown in the **Dashboard** will increase.

{% hint style="success" %}
**Tip**

You can also check for the existence of the **C:\ProgramData\Patch My PC\Client** folder on any target devices and review the following log to monitor the installation of the Client:

`C:\Windows\Temp\PatchMyPC_Client_Installer_msi.log`
{% endhint %}

{% hint style="info" %}
**Note**

To deploy the Client to other Entra ID groups, select the relevant groups from the **Groups** dropdown and click **Save**. The **Success – Updated** notification will be displayed and the Client will be deployed to the additional groups.
{% endhint %}

## Switching between Deployment Channels

If you want to switch a device between deployment channels (i.e. from using the Preview version of the Client to the Production version, or vice versa), you should:

1. Remove the device(s) from the relevant Entra ID group or remove the relevant Entra ID group from targeting.
2. [Uninstall the Client](uninstall.md).
3. Once the Client has been uninstalled, add the device(s) to the relevant Entra ID group or add the relevant Entra ID group to target the desired channel.

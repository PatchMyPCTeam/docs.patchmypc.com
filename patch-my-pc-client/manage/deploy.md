# Deploy the Patch My PC Client

_Applies to: Patch My PC Client_

To deploy the Patch my PC (PMPC) Client:

1. Navigate to **Settings | Deploy Client**

![Navigating to 'Settings | Deploy Client'](/_images/image-(593).png)

The **Deploy Client** screen is shown, which is split into two sections:

* **Preview Version Deployment –** Shows details of the preview version of our Client and which Entra ID groups it is targeted to (if relevant).
* **Production Version Deployment -** Shows details of the production version of our Client and which Entra ID groups it is targeted to (if relevant).

!['Deploy Client Deployment' screen](/_images/image-(594).png)

2. To deploy the Client (**Preview** or **Production**), click the **Groups** dropdown and select the relevant Entra ID group(s) you want to deploy the Client to.

> \*\*Important\*\*
>
> Please ensure that:
>
> \* Any devices you plan to install the PMPC Client on meet the \[PMPC Client Supported configurations]\(../supported-configurations.md).
>
> \* You use one Entra ID group to target the installation of the Preview version of the Client and a separate group to target the installation of the Production version.
>
> \* You do not have the same devices in the Entra ID groups being used to target the installation of the Preview and Production versions of the Client.

![Selecting the Entra ID Group(s) you want to deploy the client to](/_images/image-(595).png)

3. Click **Save**

![Clicking 'Save'](/_images/image-(596).png)

The **Success - Created** notification is shown.

!['Success – Created' notification](/_images/image-(603).png)

Once the Win32 app for the Client has been created in Intune, the status updates to **Success** and the Client will be deployed to the targeted devices.

![Client deployed successfully](/_images/image-(592).png)

As the Client is installed on the targeted devices, the number of **Devices Managed** shown in the **Dashboard** will increase.

> \*\*Tip\*\*
>
> You can also check for the existence of the \*\*C:\ProgramData\Patch My PC\Client\*\* folder on any target devices and review the following log to monitor the installation of the Client:
>
> \`C:\Windows\Temp\PatchMyPC\_Client\_Installer\_msi.log\`

> \*\*Note\*\*
>
> To deploy the Client to other Entra ID groups, select the relevant groups from the \*\*Groups\*\* dropdown and click \*\*Save\*\*. The \*\*Success – Updated\*\* notification will be displayed and the Client will be deployed to the additional groups.

## Switching between Deployment Channels

If you want to switch a device between deployment channels (i.e. from using the Preview version of the Client to the Production version, or vice versa), you should:

1. Remove the device(s) from the relevant Entra ID group or remove the relevant Entra ID group from targeting.
2. [Uninstall the Client](uninstall.md).
3. Once the Client has been uninstalled, add the device(s) to the relevant Entra ID group or add the relevant Entra ID group to target the desired channel.
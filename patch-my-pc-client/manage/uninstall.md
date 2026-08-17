# Uninstall the Patch My PC Client

_Applies to: Patch My PC Client_

You can use the following methods to uninstall the Patch My PC (PMPC) Client:

* [Select specific Entra ID groups to uninstall the PMPC client from](uninstall.md#select-specific-entra-id-groups-to-uninstall-the-pmpc-client-from)
* [Create an Uninstall Deployment from the Intune admin center](uninstall.md#create-an-uninstall-deployment-from-the-intune-admin-center)

## Select specific Entra ID groups to uninstall the PMPC client from

To uninstall the Patch My PC (PMPC) Client you can select specific Entra ID groups to uninstall the client from.

{% hint style="danger" %}
**Important**

Deleting a device from Intune that has the PMPC Client installed will **NOT** uninstall the PMPC Client, meaning the device will still show in PMPC Reporting. The only way to uninstall the PMPC Client is to use one of the above methods.

Also, if your trial license has expired and you have installed the PMPC Client during your trial, please see the [If your Trial License has Expired](uninstall.md#if-your-trial-license-has-expired) section below.
{% endhint %}

To uninstall the PMPC Client from specific Entra ID groups:

1. Navigate to **Settings | Deploy Client**
2. Click the relevant **Uninstall Client** button.

<figure><img src="../../.gitbook/assets/image (598).png" alt="Clicking the relevant &#x27;Uninstall Client&#x27; button" width="563"><figcaption></figcaption></figure>

3. Select the relevant group.

<figure><img src="../../.gitbook/assets/image (599).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If a group is greyed out, it means the current Client deployment is targeted to that group, and must be cleared first from the (Install) deployment before it can be selected for Uninstall.
{% endhint %}

4. Add any additional Groups as required.
5. Click **Save**.

<figure><img src="../../.gitbook/assets/image-(2).png" alt="Clicking “Save”" width="563"><figcaption></figcaption></figure>

The **Deploy Client** page is displayed along with the **Success – Updated** notification.

<figure><img src="../../.gitbook/assets/image (600).png" alt="&#x27;Success | Updated&#x27; notification" width="563"><figcaption></figcaption></figure>

The Client will then be uninstalled from all the devices within the selected Entra ID Group(s).

## Create an Uninstall Deployment from the Intune admin center

You can create an uninstall deployment in the Intune admin center that has the command for uninstalling the PMPC Client configured in the **Uninstall Command** field:

```
MSIExec.exe /x PatchMyPC.ClientInstaller.msi /qn
```

<figure><img src="../../.gitbook/assets/image (558).png" alt="Configuring the uninstall command line for the PMPC Client" width="563"><figcaption></figcaption></figure>

## If Your Trial License has Expired

If your PMPC Cloud Trial License has expired, the **Your license has expired...** banner appears at the top of the Cloud Portal, and when you navigate to **Deploy Client** both the **Delete** and **Save** buttons are disabled.

If you have deployed the PMPC Client during your trial, you should click **Uninstall Client** beside the relevant Client deployment channel used to install the Client.

On the **Confirm Uninstall Action** dialog box, click **Uninstall**.

<figure><img src="../../.gitbook/assets/image (4383).png" alt="&#x27;Confirm Uninstall Action&#x27; dialog box" width="395"><figcaption></figcaption></figure>

A new app is created in Intune for the relevant Entra ID groups with an **Uninstall** assignment to uninstall our Client.

---
description: >-
  When working with a Configuration Manager or WSUS implementation, proper
  certificate configuration is crucial.  Microsoft requires all updates to be
  signed.
---

# Certificate Configuration

_Applies to: On-premises Publisher_

## Certificates

When working with a Configuration Manager or WSUS implementation, proper certificate configuration is crucial. One way **Microsoft helps ensure an update is considered secure and from a trusted source** is through the utilization of a code signing certificate. This requirement means all custom updates must be code signed before injection into WSUS. We provide three different ways to configure the certificate.&#x20;

In most organizations, **allowing Configuration Manager to manage the certificate** is acceptable and the easiest option. There may be external requirements that prevent the usage of self-signed certificates. To read our in-depth guide on certificates click the link below.

{% embed url="https://patchmypc.com/wsus-signing-certificate-options-for-third-party-updates-in-configuration-manager" %}

If a self-signed certificate managed by Configuration Manager, is acceptable for your organization complete the steps below.

## Self Signed - Configuration Manager Managed

If you are running SCCM 1806 or newer, you can enable the option for “Configuration Manager manages the certificate” in the Software Update Point configuration. To configure this setting complete the following steps.

Begin by opening the configuration manager console and then

1. Select **Administration**
2. Expand Site Configuration and select **sites**
3. Select your topmost Site (If you have a CAS, select the CAS) - **Right click the site**
4. Select **Configure Site Components**
5. Select **Software Update Point** from the fly-out.

![](<../../.gitbook/assets/image (1896).png>)

This will open up the software update point management component tab. From this window complete the following steps if not already done.

1. Select the **Third Party Updates** Tab
2. Validate **Enable third-party software updates** is checked.&#x20;
3. Validate **Configuration Manager manages the certificate** option is selected.
4. Select **Apply**

![Enable Third  Party Updates and allow Configuration Manager to manage the certificate.](<../../.gitbook/assets/image (1814).png>)

{% hint style="warning" %}
If your [software update point ](https://docs.microsoft.com/en-us/mem/configmgr/sum/get-started/install-a-software-update-point)**site system is remote from the site server**, SSL needs to be [configured on WSUS](https://docs.microsoft.com/en-us/mem/configmgr/sum/get-started/software-update-point-ssl) for the option _**Configuration Manager manages the certificate to work**_. If SSL is not configured in this scenario, you will need to use an alternative method described here [create and deploy the WSUS signing certificate](https://patchmypc.com/how-to-deploy-the-wsus-signing-certificate-for-third-party-software-updates).

**Note**: Switching WSUS to require SSL does not require client authentication certificates on all devices, it only requires a SSL certificate on the WSUS server that **clients trust**.
{% endhint %}

Once enabled, SCCM will automatically generate the signing certificate **during the next software update point sync**. You can force a software update point sync at any time. To force a software update point sync, complete the following steps.&#x20;

1. Browse to **Software Library**
2. Expand  and **Software Updates** > **Right-click All Software Updates**
3. Select **Synchronize Software Updates**
4. Hit **OK** on the pop-up message.

![Synchronize Software Updates to generate a new certificate](<../../.gitbook/assets/image (1859).png>)

If you want to watch, and confirm the certificate is properly created, you can open the **wsyncmgr.log** this log is located in **%ConfigMgr Install Directory%\Logs\wysnmgr.log.** Alternatively, you can click the button displayed below in the Publisher General Tab.&#x20;

![](<../../.gitbook/assets/image (1874).png>)

{% hint style="info" %}
The **Open wsyncmgr.log** will only show up if the Publisher is installed on the site server. This may not be the case if your top-level software update point is not the site server.
{% endhint %}

With the log file open you'll want to watch for the entry stating the certificate was inserted. This indicates the certificate has been generated and is ready to be used.&#x20;

![](<../../.gitbook/assets/image (1924).png>)

You can ascertain if the certificate exists and is ready for use by clicking the **Show Certificate** button in the publisher.

![Here the certificate exists but has not been checked, select Show Certificate](<../../.gitbook/assets/image (1897).png>)

![Here is the information around the generated certificate](<../../.gitbook/assets/image (1780).png>)

![Note how the checkbox is now green. You are ready to start publishing updates!](<../../.gitbook/assets/image (1947).png>)

# Installing Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This article details how to install Patch My PC (PMPC) Publisher.

{% hint style="success" %}
**Tip**

Please review the [Core Requirements for Publisher](../requirements/core-requirements.md) before continuing, as these apply regardless of the platform being used, before beginning installation.
{% endhint %}

To install Patch My PC (PMPC) Publisher:

1. Once you have [downloaded Publisher](download.md), double-click the MSI to launch the installer.
2. On the **Welcome** screen, click **Next**

<figure><img src="../../.gitbook/assets/image (4756).png" alt="&#x27;Welcome&#x27; screen" width="371"><figcaption></figcaption></figure>

3. On the **End-User License Agreement** screen, review the **Terms of Service**, and if you agree with them, select the **I accept...** option, then click **Next**.

<figure><img src="../../.gitbook/assets/image (4757).png" alt="&#x27;End-User License Agreement&#x27; screen" width="371"><figcaption></figcaption></figure>

4. On the **Enable Intune Standalone Mode** screen, check the **Enable Microsoft Intune standalone mode** checkbox only if you are going to use Publisher to publish applications and updates in Intune only, then click **Next**.

{% hint style="info" %}
**Note**

Intune standalone mode removes some Publisher tabs used specifically for publishing applications and updates to ConfigMgr and WSUS. These tabs can be re-enabled retrospectively after installation from the **Advanced** tab in Publisher.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (4759).png" alt="&#x27;Enable Intune Standalone Mode&#x27; screen" width="371"><figcaption></figcaption></figure>

5. On the **Select Installation Folder** screen, choose where to install Publisher, then click **Next**.

{% hint style="info" %}
**Note**

To ease troubleshooting, we recommend accepting the default installation location:

`C:\Program Files\Patch My PC\Patch My PC Publishing Service\`
{% endhint %}

<figure><img src="../../.gitbook/assets/image (4760).png" alt="&#x27;Select Installation Folder&#x27; screen" width="371"><figcaption></figcaption></figure>

6. On the **Ready to Install** screen, click **Install.**

<figure><img src="../../.gitbook/assets/image (4761).png" alt="&#x27;Ready to Install&#x27; screen" width="371"><figcaption></figcaption></figure>

7. Click **Yes** if you receive a UAC prompt.\
   \
   Publisher is then installed.

<figure><img src="../../.gitbook/assets/image (4762).png" alt="Publisher installation begins" width="371"><figcaption></figcaption></figure>

8. On the **Completion** screen, uncheck the **Launch Patch My PC Publishing Service** if you don't want to launch Publisher immediately, then click **Finish**.

<figure><img src="../../.gitbook/assets/image (4763).png" alt="&#x27;Completion&#x27; screen" width="371"><figcaption></figcaption></figure>

## Next Steps

Once Publisher is installed, configure it based on your environment and how you plan to use it using the scenario below that best matches your environment:

* [Manage ConfigMgr Applications only](../configure/quick-start-guides/manage-configmgr-applications-only.md)
* [Manage ConfigMgr Applications and Updates (WSUS)](../configure/quick-start-guides/manage-configmgr-applications-wsus-updates.md)
* [Manage WSUS (Standalone)](../configure/quick-start-guides/manage-wsus-standalone.md)
* [Manage Intune Apps and Updates](../configure/quick-start-guides/manage-intune-apps-updates.md)
* [Manage a Mixed Environment (ConfigMgr, WSUS, and Intune)](../configure/quick-start-guides/manage-mixed-environment.md)

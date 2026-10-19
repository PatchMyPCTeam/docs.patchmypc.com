# Installing Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This article details how to install Patch My PC (PMPC) Publisher.

{% hint style="success" %}
**Tip**

Please review the [Core Requirements for Publisher](../requirements/core-requirements.md) before continuing, as these apply regardless of the platform being used, before beginning installation.
{% endhint %}

To install Patch My PC (PMPC) Publisher:

1. Once you have [downloaded Publisher](download.md), double-click the MSI to launch the installer.
2. On the **Install location** screen, check the checkbox beside the **I agree to the license terms and conditions** option, then click **Next**.

{% hint style="success" %}
**Tip**

Clicking the **I agree to the license terms and conditions** text opens our Terms of Service in a browser so you can review them.
{% endhint %}

{% hint style="info" %}
**Note**

To ease troubleshooting, we recommend accepting the default installation location:

`C:\Program Files\Patch My PC\Patch My PC Publishing Service\`
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1347).png" alt="&#x27;Install location&#x27; screen" width="490"><figcaption></figcaption></figure>

3.  On the **Select your install mode and integration settings** screen, select:

    * **Install Mode:** Choose **Full (Service and UI)\***.
    * **Integration:** Choose the option for your environment. If you use both **Microsoft Configuration Manager** and **WSUS**, choose **Microsoft Configuration Manager**, then enable **WSUS** from [Integrations and Platform](../manage/advanced-tab/integrations-platform.md) in the Publisher’s **Advanced** tab after installation.

    **\*Note:** We recommend selecting **Full** for production installations. **Service Only** and **UI Only** are currently private preview features and are not yet intended for production use.

<figure><img src="../../.gitbook/assets/image (1349).png" alt="&#x27;Select your install mode and integration settings&#x27; screen" width="490"><figcaption></figcaption></figure>

4. Click **Install** and then click **Yes** if you receive a UAC prompt.\
   \
   Publisher is then installed.

<figure><img src="../../.gitbook/assets/image (1350).png" alt="Publisher installing" width="490"><figcaption></figcaption></figure>

5. If the **Launch when ready** checkbox is checked (default), once the installation process completes, Publisher is loaded.

<figure><img src="../../.gitbook/assets/image (1351).png" alt="Publisher" width="563"><figcaption></figcaption></figure>

## Next Steps

Once Publisher is installed, configure it based on your environment and how you plan to use it using the scenario below that best matches your environment:

* [Manage ConfigMgr Applications only](../configure/quick-start-guides/manage-configmgr-applications-only.md)
* [Manage ConfigMgr Applications and Updates (WSUS)](../configure/quick-start-guides/manage-configmgr-applications-wsus-updates.md)
* [Manage WSUS (Standalone)](../configure/quick-start-guides/manage-wsus-standalone.md)
* [Manage Intune Apps and Updates](../configure/quick-start-guides/manage-intune-apps-updates.md)
* [Manage a Mixed Environment (ConfigMgr, WSUS, and Intune)](../configure/quick-start-guides/manage-mixed-environment.md)

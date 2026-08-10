# Installing Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This article details how to install Patch My PC (PMPC) Publisher.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Please review the [Core Requirements for Publisher](../requirements/core-requirements.md) before continuing, as these apply regardless of the platform being used, before beginning installation.</p>
</blockquote>

To install Patch My PC (PMPC) Publisher:

1. Once you have [downloaded Publisher](download.md), double-click the MSI to launch the installer.
2. On the **Welcome** screen, click **Next**

!['Welcome' screen](/_images/image-(4756).png "&#x27;Welcome&#x27; screen")

3. On the **End-User License Agreement** screen, review the **Terms of Service**, and if you agree with them, select the **I accept...** option, then click **Next**.

!['End-User License Agreement' screen](/_images/image-(4757).png "&#x27;End-User License Agreement&#x27; screen")

4. On the **Enable Intune Standalone Mode** screen, check the **Enable Microsoft Intune standalone mode** checkbox only if you are going to use Publisher to publish applications and updates in Intune only, then click **Next**.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Intune standalone mode removes some Publisher tabs used specifically for publishing applications and updates to ConfigMgr and WSUS. These tabs can be re-enabled retrospectively after installation from the **Advanced** tab in Publisher.</p>
</blockquote>

!['Enable Intune Standalone Mode' screen](/_images/image-(4759).png "&#x27;Enable Intune Standalone Mode&#x27; screen")

5. On the **Select Installation Folder** screen, choose where to install Publisher, then click **Next**.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>To ease troubleshooting, we recommend accepting the default installation location:</p>
<p>`C:\Program Files\Patch My PC\Patch My PC Publishing Service\`</p>
</blockquote>

!['Select Installation Folder' screen](/_images/image-(4760).png "&#x27;Select Installation Folder&#x27; screen")

6. On the **Ready to Install** screen, click **Install.**

!['Ready to Install' screen](/_images/image-(4761).png "&#x27;Ready to Install&#x27; screen")

7. Click **Yes** if you receive a UAC prompt.\
   \
   Publisher is then installed.

![Publisher installation begins](/_images/image-(4762).png "Publisher installation begins")

8. On the **Completion** screen, uncheck the **Launch Patch My PC Publishing Service** if you don't want to launch Publisher immediately, then click **Finish**.

!['Completion' screen](/_images/image-(4763).png "&#x27;Completion&#x27; screen")

## Next Steps

Once Publisher is installed, configure it based on your environment and how you plan to use it using the scenario below that best matches your environment:

* [Manage ConfigMgr Applications only](../configure/quick-start-guides/manage-configmgr-applications-only.md)
* [Manage ConfigMgr Applications and Updates (WSUS)](../configure/quick-start-guides/manage-configmgr-applications-wsus-updates.md)
* [Manage WSUS (Standalone)](../configure/quick-start-guides/manage-wsus-standalone.md)
* [Manage Intune Apps and Updates](../configure/quick-start-guides/manage-intune-apps-updates.md)
* [Manage a Mixed Environment (ConfigMgr, WSUS, and Intune)](../configure/quick-start-guides/manage-mixed-environment.md)
# Troubleshoot Installation and Upgrade Issues for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This section provides guidance for troubleshooting issues that may occur during the installation or upgrade of Patch My PC (PMPC) Publisher.

These troubleshooting steps help ensure a successful installation or upgrade of Publisher.

* [Publisher Fails to Upgrade](installation-upgrade.md#publisher-fails-to-upgrade)
* [Error 1714/1612 - The older version of Patch My PC Publishing Service cannot be removed](installation-upgrade.md#error-1714-1612-the-older-version-of-patch-my-pc-publishing-service-cannot-be-removed)

## Publisher Fails to Upgrade

At the end of a [sync](../manage/sync-schedule-tab/), if a new version of Publisher is available, Publisher attempts to install the update by default. When this occurs, the following entry appears in the **PatchMyPC.log** file at the end of the sync.

```
Starting self-update, the command line is: MsiExec.exe /i C:\WINDOWS\TEMP\PatchMyPC-Publishing-Service.msi /qn /log C:\WINDOWS\TEMP\PatchMyPC-Publishing-Service_Upgrade.log
```

![PatchMyPC.log](/_images/image-(4232).png "PatchMyPC.log")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you see errors such as "_An error occurred with the SignalR connection_" logged around the time illustrated above, this is normal while some services stop and start again during the update process.</p>
</blockquote>

If a failure occurs during the self-update process and [Alerts](../manage/alerts-tab/) are configured, a notification is generated. The notification will appear similar to the screenshots shown below

![Example alert](/_images/image-(4233).png "Example alert")

![Example alert detail](/_images/image-(4234).png "Example alert detail")

To understand the root cause of the upgrade failure, inspect the log file indicated in **PatchMyPC.log** produced by the MSI installer:&#x20;

* **C:\WINDOWS\TEMP\PatchMyPC-Publishing-Service\_Upgrade.log**

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Error 1714](installation-upgrade.md#error-1714-1612-the-older-version-of-patch-my-pc-publishing-service-cannot-be-removed) for more details on common causes for upgrade failures.</p>
</blockquote>

## Error 1714/1612 - The older version of Patch My PC Publishing Service cannot be removed

When searching upwards from the bottom of the **PatchMyPC-Publishing-Service\_Upgrade.log** log file for `return value 3`, you might see lines similar to the following:

```
Action start 05:37:07: RemoveExistingProducts.
CustomAction  returned actual error code 1612 (note this may not be 100% accurate if translation happened inside sandbox)
[05:37:07:238]: /_images/Product-Patch-My-PC-Publishing-Service-Error-1714-The-older-version-of-Patch-My-PC-Publishing-Service-cannot-be-removed-Contact-your-technical-support-group-System-Error-1612
Error 1714. The older version of Patch My PC Publishing Service cannot be removed.  Contact your technical support group.  System Error 1612.
```

When you attempt to manually install the update by downloading and running the [latest .msi](https://patchmypc.com/msi), you receive a dialogue similar to the one below:

!['The feature you are trying to use is on a network resource that is unavailable' dialog](/_images/image-(4235).png "&#x27;The feature you are trying to use is on a network resource that is unavailable&#x27; dialog")

The 1612 error code is usually thrown when the original installation media for the currently installed application is no longer available on the system - something has deleted it.&#x20;

Typically, .msi files cache themselves in the **C:\Windows\installer** folder, and the original .msi file is critical for any application update, repair, or uninstall.

The Windows Installer service first looks in the .msi of the currently installed version in **C:\Windows\installer** folder, and also its last known install location - the self-updater is downloaded and launched from the **C:\Windows\temp** folder.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can read more about system error code 1612 in the following knowledge base article: <a href="https://patchmypc.com/kb/system-error-1612-installation-source/">System Error 1612 – The installation source for this product is not available.</a></p>
</blockquote>

If you encounter this issue, you can resolve it by re-caching the missing .msi file:

1. Download the .msi file for the current version you have installed.
2. Recache the .msi file using the following command:

```
msiexec /fvomus "C:\path\to\PatchMyPC-Publishing-Service.msi" /qn
```

3. Attempt the update again, and it should now be successful.

We do not currently publicly host the installers for older versions of Publisher, so we advise you to open a [technical support case](https://patchmypc.com/technical-support/) requesting a copy for the version you need.

After resolving the issue, we strongly recommend you investigate any cleanup scripts or other automations that may be deleting files from the **C:\Windows\installer** folder to prevent the issue from recurring.
# Configure Retention Policy in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

> \*\*Note\*\*
>
> Using the \*\*Retention Policy\*\* tool is optional and is not supported by the MSP App Sets feature.

The **Retention Policy** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to determine how many versions of an app (both Windows and macOS) you want to keep. If deploying a later version of an app causes issues, you can redeploy an older version.

By default, PMPC only retains the latest version of an app in your environment. Configuring a Retention Policy allows you to keep the current version, plus the number of configured versions as set by the Retention Policy.

For example, setting a Retention Policy of 1 for Google Chrome would mean you always have _n-1_ versions of Chrome, the latest and the previous version, until a newer version is deployed.

> \*\*Important\*\*
>
> The previous version (n-1) of an app may temporarily remain visible in Intune even when a Retention Policy is \*\*not\*\* configured.
>
> The portal only deletes the previous version during the \*\*next\*\* \[Sync Schedule]\(../../../../manage/settings/sync-schedule.md), not in the same sync that creates the new version.
>
> This behavior is intentional as it prevents situations where if the new version (n) fails to package, no version of the app remains available.
>
> If Update Rings are configured, the previous version may remain for more than one sync, and will only be deleted after the next \[Sync Schedule and all Update Rings ]\(../../../update-rings/sync-schedule.md)steps are completed.

To configure a PMPC Cloud deployment to use a Retention Policy:

1. Add the [**Retention Policy** tool](../#adding-additional-tools).
2. Click the **Retention Policy** tool.

![Clicking the 'Retention Policy' tool](../../../../../.gitbook/assets/image-\(3647\).png)

3. In the **Versions to Retain** box, either type the required number or use the controls to configure the number of versions of this app you wish to retain in your environment.

> \*\*Note\*\*
>
> The default value of \*\*0\*\* means only the most recent version of the app is retained. You can retain up to ten versions of an app.

![Configuring the 'Versions to Retain' field](../../../../../.gitbook/assets/image-\(3648\).png)

> \*\*Tip\*\*
>
> See \[Check App Version Retention]\(../../../../technical-references/intune-reference/check-app-version-retention-in-intune.md) for details on how to check within Intune that the correct number of versions of an app are being retained as defined in your Retention Policy.

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.

> \*\*Note\*\*
>
> Other important points about App Version Retention:
>
> \* Modifying the \*\*Versions to Retain\*\* setting is supported. The next time the \[Sync Schedule]\(../../../../manage/settings/sync-schedule.md) runs (or you manually \[update an app]\(../../../manage-deployments/updates/)), the changes will be applied to the deployment.
>
> \* Deleting a deployment or disconnecting \[Intune ]\(/broken/pages/RoXhXa1jcXhIcPcKJk05#deleting-an-intune-tenant-connection)will delete the latest and all old unassigned versions of all of your deployments.
>
> \* Modifying an existing deployment with a Retention Policy configured will only affect the current version, not all previous versions. For example, if you edit a deployment and add an extra file, the file is only added to the latest version, not all previous versions.
>
> \* You should avoid deleting versions of apps manually using the Intune admin center. Inadvertently deleting a previous version from Intune will not break the Retention Policy for the deployment. When a newer version is deployed, we will delete the relevant previous version(s) accordingly to keep everything in sync.

# Pause Updates to a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

The _Pause Updates_ feature (which is disabled by default) of Patch My PC (PMPC) Cloud allows you to prevent an app that’s previously been successfully deployed from being updated whenever a new version is released.

> \*\*Important\*\*
>
> Pausing updates for an app only affects our portal. If a new version of an app becomes available and updates are paused, the portal won’t create a new version of that app while updates are paused.
>
> However, any existing versions of apps already in Intune that are assigned will still be evaluated and, if applicable, installed by your devices.

To Pause Updates for an app:

1. Click on the relevant successful deployment you want to pause for updates.

> \*\*Tip\*\*
>
> Click the filter button (!\[]\(/\_images/image-(3215).png>)) and select the \*\*Disabled\*\* option under the \*\*Updates\*\* section, followed by \*\*Apply Filters\*\* to see just those deployments that do not have updates paused.

![Clicking on the relevant successful deployment you want to pause for updates](/_images/image-(2490).png)

2.  Click the **Pause Updates** slider to enable it.<br>

    ![Clicking the "Pause Updates" slider](/_images/image-(2699).png)
3.  Click the **X** to close the deployment properties page.<br>

    ![Clicking "X" to close the deployment properties page.](/_images/image-(2700).png)

    \
    The list of deployments is displayed and **UPDATES PAUSED** shows under the deployment name so you updates are paused for this specific deployment.<br>

    ![](/_images/image-(2701).png)

> \*\*Note\*\*
>
> If \*\*Pause Updates\*\* is enabled for a Deployment, you can still manually sync it at any time to check for and publish a newer version, if one is available. See the \[Sync Now]\(sync-now.md) process for more details.
>
> Also, if your deployment has \[Update Rings]\(../../update-rings/) enabled and you experience a problem with any of the rings, \*\*Pause Updates\*\* prevents both an existing ring from being upgraded to a new version and any additional Update Rings from being created provided the \*\*Immediate\*\* option was set for the rings.
>
> The \*\*Pause Updates\*\* option will be unavailable if your deployment uses \*\*Delayed\*\* rings and some of these rings have yet to update. As a workaround, you can delete the deployment to stop any outstanding updates.
# Resume Updates to a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

If the _Pause Updates_ feature of Patch My PC (PMPC) Cloud has been configured for an app that has since been updated, and you want to bring the app up-to-date to the latest version, you need to disable pause updates.

> \*\*Note\*\*
>
> If an app has more than one version of an update available, resuming updates will ensure it is updated to the latest version.
>
> Also, if you paused a deployment with \[Update Rings]\(../../update-rings/) enabled, when you resume updates for that deployment, the Update Rings are re-enabled and function normally.

To resume updates for an app:

1. Click on the relevant deployment that has been paused.

> \*\*Tip\*\*
>
> Click the filter button (!\[]\(/\_images/image-(3215).png>)) and select the \*\*Enabled\*\* option under the \*\*Updates\*\* section, followed by \*\*Apply Filters\*\* to see just those deployments that have updates paused.

![Clicking on the relevant successful deployment which has been paused for updates](/_images/image-(2702).png)

2.  Click the **Pause Updates** slider to disable it.<br>

    ![Clicking the "Pause Updates" slider](/_images/image-(2703).png)

> \*\*Note\*\*
>
> Notice on the above screenshot that the \*\*Sync Now\*\* button is available, meaning one or more updates are available for this app.

3.  Click the **X** to close the deployment properties page.<br>

    ![Clicking "X" to close the deployment properties page](/_images/image-(2704).png)

    \
    The list of deployments is displayed without **UPDATES PAUSED** under the deployment you just unpaused.<br>

    !["UPDATES PAUSED" no longer under the deployment name.](/_images/image-(2705).png)

Updates for this app are now resumed.

You now need to decide how you want to install any updates for this app:

* **Install the updates now –** If you want to install the updates as soon as possible, follow the [Sync Now](sync-now.md) process.
* **Wait for the nightly sync to run –** If you are happy to wait for the updates to be installed the next time the daily sync runs (at 2 am by default), you do not need to do anything.

> \*\*Note\*\*
>
> You can change the Sync Schedule to a different time, as detailed in the \[Managing the Sync Schedule]\(../../../manage/settings/sync-schedule.md) process.
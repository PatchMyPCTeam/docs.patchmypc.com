# Monitor a Deployment in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

All Patch My PC (PMPC) Cloud deployments include a status.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Because PMPC Cloud performs the deployment, not Microsoft Intune, you can only view the status of these deployments in the PMPC Cloud Portal. The status of PMPC Cloud deployments is not visible from within the Intune admin center.</p>
</blockquote>

To see the status of a deployment:

1. Sign in to the portal at [https://portal.patchmypc.com/](https://portal.patchmypc.com/).
2.  Navigate to the **Deployments** node.<br>

    ![Navigating to the "Deployments" page.](/_images/image-(2155).png "Navigating to the “Deployments” page.")

    \
    The **Deployments** page loads, showing all current deployments. \
    \
    The **Status** column shows the current status of each deployment, which will be one of those shown in the table below.

!["Status" column showing the status of each deployment](/_images/image-(2156).png "“Status” column showing the status of each deployment")

<table><thead><tr><th width="121" valign="top">Status</th><th valign="top">Means the application…</th></tr></thead><tbody><tr><td valign="top">Success</td><td valign="top">The application was successfully created in Intune.</td></tr><tr><td valign="top">In Progress</td><td valign="top"><p>The application is currently being created in Intune. During periods of high activity, processing may take longer than usual. If an issue occurs, the Portal will automatically retry the creation process for up to 24 hours.</p><p> </p><p>During this time, the status will change to <strong>Retrying</strong>. If the application still cannot be created after 24 hours, the status will change to <strong>Failed</strong>.<br><br>Whilst a deployment is <strong>In Progress</strong>, no other actions can be performed on it, including editing or deleting the deployment.</p></td></tr><tr><td valign="top">Retrying</td><td valign="top"><p>The application is still being processed. The initial creation attempt was unsuccessful and may have failed due to a Microsoft Graph issue or a temporary issue within Patch My PC services.</p><p></p><p>No action is required from you as PMPC. Patch My PC will continue retrying the operation for up to 24 hours.</p><p></p><p>If the deployment remains in a <strong>Retrying</strong> state for longer than 24 hours, the status will change to <strong>Failed</strong>.</p></td></tr><tr><td valign="top">Failed</td><td valign="top"><p>The deployment could not be successfully processed and created in Intune.</p><p></p><p>In some cases, the application may already exist in Intune even though the deployment is marked as <strong>Failed</strong>.</p><p></p><p>This can happen when the app is successfully created, but PMPC is unable to complete all required processing steps or confirm the final status.</p><p></p><p>If a deployment remains unsuccessful after all retry attempts, its status will be changed to <strong>Failed</strong>.</p><p> </p><p>Please <a href="https://patchmypc.com/technical-support/">Open a Support Case</a> for assistance.</p></td></tr></tbody></table>
# Use the "Sync Now" feature in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If an app has more than one version of an update available, using **Sync Now** ensures it is updated to the latest version as soon as possible, which could impact your users. So, think carefully before using this.</p>
</blockquote>

If you have [resumed updates](resume-updates.md) for an app in Patch My PC (PMPC) Cloud and want to update it as soon as possible rather than waiting for the nightly sync job to run:

1.  Click on the relevant deployment which has been resumed.<br>

    ![Clicking on the relevant successful deployment for which updates have been resumed](/_images/image-(2706).png "Clicking on the relevant successful deployment for which updates have been resumed")
2.  Click **Sync Now** to install any updates for the app immediately.<br>

    ![Clicking "Sync Now"](/_images/image-(2707).png "Clicking “Sync Now”")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If the **Sync Now** button is greyed out, no updates are available for this app.</p>
</blockquote>

3.  On the **Are you sure you want to update <**_**app\_name**_**> to the latest version** popup, click **OK**.<br>

    ![](/_images/image-(2530).png)

    \
    The **Deployment <**_**app\_name**_**> updated** notification is displayed and the deployment **Status** changes to **In Progress**.<br>

    ![](/_images/image-(2531).png)

    \
    Once the deployment has been completed successfully, the **Status** changes to **Success**.<br>

    !["Status" changing to Success.](/_images/image-(2532).png "“Status” changing to Success.")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you look in the **Events node**, you will see the following event:</p>
<p>**Deployment <**_**app\_name**_**> Updated.**</p>
</blockquote>
# About the "Summary" tab of a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Reviewing the **Summary** tab is optional, but recommended.</p>
</blockquote>

The **Summary** tab of the Patch My PC (PMPC) Cloud deployment wizard provides a summary of the deployment so you can confirm that it is configured correctly before you create it.

!["Summary" tab](/_images/image-(3093).png "&#x22;Summary&#x22; tab")

Review the summary of the deployment shown on the **Summary** page.\
\
If you are happy click **Deploy**.\
\
If you need to change something, click **< Prev** to backtrack through the Deployment Wizard to the relevant setting. Make the change, then step back through the wizard to this page. If everything is now correct, click **Deploy**.

![Clicking "Deploy"](/_images/image-(3094).png "Clicking &#x22;Deploy&#x22;")

<blockquote class="wp-block-quote">
<p>Note</p>
<p>If you have configured this deployment to use [Update Rings](../update-rings/), you will see the **Deployment Summary** screen, containing details on how you have configured the rings.</p>
<p>!["Deployment Summary" shown if this deloyment is using Update Rings](/_images/image-(2993 "\"Deployment Summary\" shown if this deloyment is using Update Rings").png>)</p>
<p>See [Update Rings](../update-rings/) for more information.</p>
</blockquote>

The App Catalog is redisplayed along with the **Success - Created&#x20;**_**\<deployment\_name>**_ notification.

![](/_images/image-(3095).png)

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>When a new version of software is released, it is automatically deployed using the settings of the existing deployment. The old version will be removed from the target user/device and replaced with the newer version.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>By default, the installation logs for an app will be created in the following folder regardless of the installer file type:</p>
<p>`%ProgramData%\PatchMyPCInstallLogs`</p>
<p>The only exception is for EXE files, where the specified value for the **loggingSwitch** variable will be used if it is not null or empty.</p>
</blockquote>
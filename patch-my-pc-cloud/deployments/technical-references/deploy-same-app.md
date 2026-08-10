# Deploy the same App with multiple configurations using Patch My PC Cloud

_Applies to: Patch My PC Cloud_

You can deploy the same app with different configurations using Patch My PC (PMPC) Cloud.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>For this to work, you must use a different **Display Name** for the deployment. If you don't, you will receive the [deployment with the same name already exists](../../troubleshoot/deployments/a-deployment-with-the-same-name-less-than-deployment_name-greater-than-already-exists-error-when-dep.md) error.</p>
</blockquote>

To deploy the same app with a different configuration:

1. Sign in to the portal at [https://portal.patchmypc.com/](https://portal.patchmypc.com/).
2. Locate the required app on the **App Catalog** page.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>Use the **Search** field to help you locate the app.</p>
</blockquote>

!["App Catalog" page](/_images/image-(1443).png "“App Catalog” page")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The green cloud icon beside the version number tells you this software has already been deployed using PMPC Cloud.</p>
</blockquote>

3. Click the app to open its properties, then click **Deploy** to start the Deployment Wizard.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See the [Deploy an App](../deploy-app/) for more details. You can also apply a deployment template to this deployment by clicking **Apply Template** and following the [Use a Template in Deployments](../use-template.md) process.</p>
</blockquote>

![Clicking "Deploy" on the App's properties page](/_images/image-(1189).png "Clicking &#x22;Deploy&#x22; on the App&#x27;s properties page")

4. On the G**eneral Information** tab, in the **Display Name** field, enter a unique name for this deployment, then click **Next**.

!["General Information" page](/_images/image-(3317).png "&#x22;General Information&#x22; page")

5. On the **Configurations** tab, configure the settings to add any required scripts or additional installation parameters, then click **Next**.

!["Configurations" tab](/_images/image-(3318).png "&#x22;Configurations&#x22; tab")

6. On the **Assignments** tab, click **Add Assignment**, then select the assignment type you want to add for this deployment.

![Clicking "Add Assignment", then selecting the assignment type you want to add for this deployment](/_images/image-(3319).png "Clicking &#x22;Add Assignment&#x22;, then selecting the assignment type you want to add for this deployment")

7. On the **Add <**_**assignment\_type**_**> Assignment** page, select the relevant options, then click **Save**.

![](/_images/image-(3320).png)

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you add an available assignment, as shown below, we recommend selecting the same options in the **Add update only app for** section. Doing this will automatically make the current version of the app and any updates (current or future) available.<br></p>
</blockquote>

The **Assignments** page updates to show the newly created deployment.

![New assignment shown on the "Assignments" page](/_images/image-(3321).png "New assignment shown on the “Assignments” page")

8. Configure the settings for deployment, if required.

![Configure any required settings](/_images/image-(3322).png "Configure any required settings")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>We automatically configure these settings based on our experience and best practices, but you can modify certain settings if necessary.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can click **Deploy** on this page if you don’t want to add additional assignments or see the **Overview** page, which allows you to double-check the settings you’ve configured for this deployment.</p>
</blockquote>

9. Add any additional assignments for this deployment by clicking **Add Assignment** and repeating Steps 6 to 8, then click **Next**.

![Adding  any additional assignments for this deployment by clicking "Add Assignment"](/_images/image-(3323).png "Adding  any additional assignments for this deployment by clicking &#x22;Add Assignment&#x22;")

10. Review the deployment summary shown on the **Summary** page.\
    \
    If you are happy, click **Deploy**.

![Clicking "Deploy"](/_images/image-(3324).png "Clicking &#x22;Deploy&#x22;")

If you need to change something, click **< Prev** to backtrack through the Deployment Wizard to the relevant setting. Make the change, then step back through the wizard to this page. If everything is now correct, click **Deploy**.

The **Deployments** page is displayed along with the **Success - Created&#x20;**_**\<deployment\_name>**_ notification.

![](/_images/image-(3326).png)

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>By default, the installation logs for an app will be created in the following folder regardless of the installer file type:</p>
<p>`%ProgramData%\PatchMyPCInstallLogs`</p>
<p>The only exception is for EXE files, where the specified value for the **loggingSwitch** variable will be used if it is not null or empty.</p>
</blockquote>
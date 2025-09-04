# Create an MSP App Set

_Applies to: Patch My PC Cloud_

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This documentation is under construction. Once it is finalized, this banner will be removed.</p>
</blockquote>

Creating an App Set is a two-stage process that involves defining:

1. [Which apps should be included in the App Set](create-an-msp-app-set.md#defining-which-apps-to-include-in-the-app-set)
2. [Where to deploy the App Set.](create-an-msp-app-set.md#defining-where-to-deploy-an-app-set)

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>We do not recommend creating a single App Set that you use to deploy all of the required apps to your customers. Instead, you should consider creating separate App Sets by app function, e.g., core apps (apps that should be installed or available everywhere), utilities that should only be deployed to certain groups or users, etc.</p>
<p>Adopting this approach reduces the impact of working with App Sets on your infrastructure and that of your child companies. Plus, if someone accidentally deletes the wrong App Set, the impact on the targeted users will be reduced, and the time taken to recreate and redeploy the App Set will be reduced.</p>
</blockquote>

### Defining which apps to include in the App Set

To define which apps to include in the App Set:

1. Sign in to the parent MSP Company at [https://portal.patchmypc.com/](https://portal.patchmypc.com/)
2.  Navigate to **App Sets**\


    ![Navigating to “App Sets”](/_images/image-(2546).png "Navigating to “App Sets”")

    \
    The **App Sets** page shows any existing App Sets.\


    ![“App Sets” page showing an existing App Sets](/_images/image-(2548).png "“App Sets” page showing an existing App Sets")
3.  Click **Add App Set**\


    ![Clicking “Add App Set”](/_images/image-(2549).png "Clicking “Add App Set”")
4. On the **Add App Set** screen, enter a unique name for the new App Set in the **App Set Name** field and click **Add**\
   \
   ![Specifying the name for the new App Set](/_images/image (2551).png>)\
   \
   The App Set is created and the _**\<appset\_name>**_ screen opens (where _**\<appset\_name>**_ is the name of the App Set).

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can click **Edit Name** beside the App Set name if you want to rename it.</p>
</blockquote>

![App Set name screen](/_images/image-(2552).png "App Set name screen")

5. To add an application to this App Set, click **Add Application**

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You can add up to 100 apps per App Set, but each app can only be added to an App Set once.</p>
<p>You can also add an [MSP Custom App](../msp-custom-apps/) to an App Set, provided that app has been created and assigned to all customers.</p>
</blockquote>

![Clicking “Add Application” to add an application to this App Set](/_images/image-(2553).png "Clicking “Add Application” to add an application to this App Set")

6. On the **General Information** page, select the relevant app you want to add from the **Select Application** dropdown or start typing its name.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Only apps that have been deployed successfully will appear in the **Select Application** dropdown.</p>
<p>An MSP Custom App will only appear in the **Select Application** dropdown if it has been added and assigned to all customers. If the Custom App has only been assigned to a specific customer or only to the MSP, it will not appear in the dropdown.</p>
</blockquote>

![Selecting the relevant app you want to add from the “Select Application” dropdown](/_images/image-(2554).png "Selecting the relevant app you want to add from the “Select Application” dropdown")

7.  In the **Display Name** field, we suggest you add the name of the App Set as a suffix.\


    For example, if the App Set’s name is **Core Apps** and you are deploying Adobe Acrobat Pro, we recommend changing the **Display Name** from just **Adobe Acrobat Pro** to **Adobe Acrobat Pro – Core Apps**.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The reason for the above recommendations is that by default, when an app in an App Set is deployed, if the app has already been deployed in your company, we automatically add the **\_AppSet<**_**number**_**>** suffix (for example **\_AppSet7**) to the deployment’s name, where **<**_**number**_**>** is the next available sequential number. This is because all deployment names need to be unique.</p>
<p>So in our Acrobat example, the default deployment name would be something like:</p>
<p>**Adobe Acrobat Pro\_AppSet7**</p>
<p>This is potentially confusing as you won’t know which deployment belongs to which App Set. We are working on improving this.</p>
</blockquote>

![Modifying the “Display Name” to include the App Set’s suffix](/_images/image-(2555).png "Modifying the “Display Name” to include the App Set’s suffix")

8. Modify any other settings on the **General Information** page as required, then click **Next**

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>In the current release, this page contains a subset of the options for creating a regular PMPC Cloud Deployment. See [General Information (Deployments)](../../cloud-deployments/deploying-an-app-using-cloud/cloud-general-information-deployment-tab.md) for more details on each option.</p>
</blockquote>

![Clicking “Next” on the “General information” page.](/_images/image-(2556).png "Clicking “Next” on the “General information” page.")

9. On the **Configurations** page, configure the required options, then click **Next**.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>In the current release, this page contains a subset of the options for creating a regular PMPC Cloud Deployment. See [Configurations (Deployments)](../../cloud-deployments/deploying-an-app-using-cloud/cloud-configurations-deployment-tab/) for more details on each option.</p>
</blockquote>

![Configuring any required options on the “Configurations” page](/_images/image-(2557).png "Configuring any required options on the “Configurations” page")

10. On the **Assignment Type** page, select which assignment type(s) you want to apply to this App Set, then click **Save** to save your changes.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>As this is an App Set, only certain assignment types are supported compared to a regular PMPC Cloud Deployment. See [Assignments (Deployments)](../../cloud-deployments/deploying-an-app-using-cloud/cloud-assignments-deployment-tab.md) for more details on each option.</p>
<p>Selecting the **Update Only** type (if available) will create an Update Only app in Intune alongside the Available or Required type selected.</p>
</blockquote>

![Selecting the assignment type for this app and clicking “Save”](/_images/image-(2558).png "Selecting the assignment type for this app and clicking “Save”")

11. Repeat steps 5 to 10 to add any additional apps to the App Set.

### Defining where to deploy an App Set

Once you have added the required apps, next you need to define where to deploy the App Set.

To define where to deploy an App Set:

1.  Click the **Assignments** tab.\


    ![Clicking the “Assignments” tab](/_images/image-(114).png "Clicking the “Assignments” tab")
2. If you don’t want to use Update Rings, go to step 4.
3. Click **Enable Update Rings** and [configure them](../../cloud-deployments/cloud-update-rings/create-update-rings-in-cloud.md) as required.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>In App Sets, we only support <a href="https://docs.patchmypc.com/installation-guides/patch-my-pc-cloud/deployments/update-rings/how-update-rings-are-created#immediate-update-rings">Immediate </a>Update Rings.</p>
<p>You can add multiple companies to an App Set and to the same set of Update Rings.</p>
<p>A child customer also doesn’t need to be present in all rings. For example, if you create four Update Rings for an App Set, but a child customer only requires two rings, you only need to add that child customer to the two relevant rings. On the child customer side, only the rings they are part of will be created in the child company, not all four rings defined in the App Set.</p>
</blockquote>

![Clicking “Enable Update Rings”](/_images/image-(115).png "Clicking “Enable Update Rings”")

4.  Click **Add Assignment**\
    \


    ![Clicking “Add Assignment”](/_images/image-(116).png "Clicking “Add Assignment”")
5. Select the relevant company that has an Intune connection that you want to assign this deployment to and click **Next**

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You can only select a single company at a time (up to a maximum of 100), as every company’s Entra ID setup in terms of resources will be different.</p>
</blockquote>

![Selecting the relevant company to assign this deployment to.](/_images/image-(118).png "Selecting the relevant company to assign this deployment to.")

6. On the **Assignments** tab, select the relevant resources you want to deploy this app to and click **Save**.

![Selecting the relevant resources for this assignment](/_images/image-(119).png "Selecting the relevant resources for this assignment")

7. Repeat steps 4 to 6 to add any additional companies you want to deploy this App Set to.
8. On the **App Set** page, configure any required settings for the assignments.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you are using Update Rings for this App Set, we recommend you create all of the assignments first, which adds all of them to the first Update Ring. Then drag and drop the assignments to the relevant rings.</p>
</blockquote>

![Configuring any required settings for the assignments](/_images/image-(120).png "Configuring any required settings for the assignments")

9.  Click **Deploy** to deploy this App Set.\


    ![Clicking “Deploy” to deploy this App Set](/_images/image-(122).png "Clicking “Deploy” to deploy this App Set")

The **App Sets** page is redisplayed along with the **Success – App Set created** notification. The newly created App Set will show a Status of **In Progress**, followed by **Success** once all the deployments within the App Set have been completed successfully.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The **Status** will show as **Failed** if one or more of the deployments fails.</p>
</blockquote>

![“App Sets” showing the newly created deployment](/_images/image-(123).png "“App Sets” showing the newly created deployment")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You and the admins at the child company can monitor the status of each individual deployment from the **Deployments** node of the targeted company.</p>
<p>![App Set deployment when viewed from the child company](/_images/image (124).png>)</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>You cannot **Edit** or **Delete** a deployment from the **Deployments** node if it belongs to an App Set (these options are unavailable when clicking on the ellipsis (**⋮**) beside the deployment). This is another reason for adding the App Set’s name as a suffix to the app’s **Display Name** so that when you are viewing all of your deployments, you and the admins at your child companies can easily identify which deployment belongs to an App Set.</p>
</blockquote>

Once the App Set has been deployed successfully, it will show a **Status** of **Success** on the **App Sets** page.

![App Set showing with a status of “Success”](/_images/image-(125).png "App Set showing with a status of “Success”")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Once successfully created, any deployments created as part of an App Set will be updated based on the Sync Schedule configured at each child customer. So even if you have a single App Set with deployments to multiple child customers, you can end up with different versions of the same app at different child customers depending on when the [Sync Schedule](../../cloud-administration/manage-the-sync-schedule-in-cloud.md) runs. See [Manage Updates](../../cloud-deployments/manage-updates-in-cloud/) for more information.</p>
</blockquote>
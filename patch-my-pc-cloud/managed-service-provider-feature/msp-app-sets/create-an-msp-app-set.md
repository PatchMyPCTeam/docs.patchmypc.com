# Create an MSP App Set

_Applies to: Patch My PC Cloud_

Creating an App Set in Patch My PC (PMPC) Cloud is a two-stage process that involves:

* [Adding Apps to the App Set](create-an-msp-app-set.md#defining-which-apps-to-include-in-the-app-set)
* [Deploying the App Set](create-an-msp-app-set.md#defining-where-to-deploy-an-app-set)

{% hint style="info" %}
**Note**

We do not recommend creating a single App Set that you use to deploy all of the required apps to your customers. Instead, you should consider creating separate App Sets by app function, e.g., core apps (apps that should be installed or available everywhere), utilities that should only be deployed to certain groups or users, etc.

Adopting this approach reduces the impact of working with App Sets on your infrastructure and that of your child companies. Plus, if someone accidentally deletes the wrong App Set, the impact on the targeted users will be reduced, and the time taken to recreate and redeploy the App Set will be reduced.
{% endhint %}

## Adding Apps to the App Set

{% hint style="danger" %}
**Important**

We currently do not support adding script-based Custom Apps or Binary Free Apps to MSP App Sets.
{% endhint %}

To add apps to an App Set:

1. Sign in to the parent MSP Company at [https://portal.patchmypc.com/](https://portal.patchmypc.com/)
2. Navigate to **App Sets**

<figure><img src="../../../.gitbook/assets/image (3248).png" alt="Navigating to “App Sets”" width="563"><figcaption></figcaption></figure>

The **App Sets** page shows any existing App Sets.

<figure><img src="../../../.gitbook/assets/image (3250).png" alt="“App Sets” page showing an existing App Sets" width="563"><figcaption></figcaption></figure>

3. Click **Add App Set**

<figure><img src="../../../.gitbook/assets/image (3251).png" alt="Clicking “Add App Set”" width="563"><figcaption></figcaption></figure>

4. On the **Add App Set** screen, enter a unique name for the new App Set in the **App Set Name** field and click **Add**

![Specifying the name for the new App Set](<../../../.gitbook/assets/image (3253).png>)

The App Set is created and the _**\<appset\_name>**_ screen opens (where _**\<appset\_name>**_ is the name of the App Set).

{% hint style="success" %}
**Tip**

You can click **Edit Name** beside the App Set name if you want to rename it.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3254).png" alt="App Set name screen" width="563"><figcaption></figcaption></figure>

5. To add an application to this App Set, click **Add Application**

{% hint style="info" %}
**Note**

You can add up to 100 apps per App Set, but each app can only be added to an App Set once.

You can also add an [MSP Custom App](../msp-custom-apps/) to an App Set, provided that app has been created and assigned to all customers.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3255).png" alt="Clicking “Add Application” to add an application to this App Set" width="563"><figcaption></figcaption></figure>

6. On the **General Information** page, select the relevant app you want to add from the **Select Application** dropdown or start typing its name.

{% hint style="info" %}
**Note**

Only apps that have been deployed successfully will appear in the **Select Application** dropdown.

An MSP Custom App will only appear in the **Select Application** dropdown if it has been added and assigned to all customers. If the Custom App has only been assigned to a specific customer or only to the MSP, it will not appear in the dropdown.

Also, if an app has multiple variants with different version numbers, you will see a yellow triangle with an exclamation mark next to the **Version** number. This is a warning to you to double-check that you are deploying the correct version.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3256).png" alt="Selecting the relevant app you want to add from the “Select Application” dropdown" width="506"><figcaption></figcaption></figure>

7.  In the **Display Name** field, we suggest you add the name of the App Set as a suffix.<br>

    For example, if the App Set’s name is **Core Apps** and you are deploying Adobe Acrobat Pro, we recommend changing the **Display Name** from just **Adobe Acrobat Pro** to **Adobe Acrobat Pro – Core Apps**.

{% hint style="info" %}
**Note**

The reason for the above recommendations is that by default, when an app in an App Set is deployed, if the app has already been deployed in your company, we automatically add the **\_AppSet<**_**number**_**>** suffix (for example **\_AppSet7**) to the deployment’s name, where **<**_**number**_**>** is the next available sequential number. This is because all deployment names need to be unique.

So in our Acrobat example, the default deployment name would be something like:

**Adobe Acrobat Pro\_AppSet7**

This is potentially confusing as you won’t know which deployment belongs to which App Set. We are working on improving this.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3257).png" alt="Modifying the “Display Name” to include the App Set’s suffix" width="509"><figcaption></figcaption></figure>

8. Modify any other settings on the **General Information** page as required, then click **Next**

{% hint style="info" %}
**Note**

In the current release, this page contains a subset of the options for creating a regular PMPC Cloud Deployment. See [General Information (Deployments)](../../deployments/deploy-app/general-information-tab.md) for more details on each option.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3258).png" alt="Clicking “Next” on the “General information” page." width="509"><figcaption></figcaption></figure>

9. On the **Configurations** page, configure the required options, then click **Next**.

{% hint style="info" %}
**Note**

In the current release, this page contains a subset of the options for creating a regular PMPC Cloud Deployment. See [Configurations (Deployments)](../../deployments/deploy-app/configurations-tab/) for more details on each option.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3259).png" alt="Configuring any required options on the “Configurations” page" width="507"><figcaption></figcaption></figure>

10. On the **Assignment Type** page, select which assignment type(s) you want to apply to this App Set, then click **Save** to save your changes.

{% hint style="info" %}
**Note**

As this is an App Set, only certain assignment types are supported compared to a regular PMPC Cloud Deployment. See [Assignments (Deployments)](../../deployments/deploy-app/assignments-tab.md) for more details on each option.

Selecting the **Update Only** type (if available) will create an Update Only app in Intune alongside the Available or Required type selected.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3260).png" alt="Selecting the assignment type for this app and clicking “Save”" width="502"><figcaption></figcaption></figure>

11. Repeat steps 5 to 10 to add any additional apps to the App Set.

## Deploying the App Set

Once you have finished adding the required apps to an App Set, you can deploy it.

To define where to deploy an App Set:

1.  Click the **Assignments** tab.<br>

    <figure><img src="../../../.gitbook/assets/image (816).png" alt="Clicking the “Assignments” tab" width="563"><figcaption></figcaption></figure>
2. If you don’t want to use Update Rings, go to step 4.
3. Click **Enable Update Rings** and [configure them](../../deployments/update-rings/create.md) as required.

{% hint style="info" %}
**Note**

In App Sets, we only support [Immediate ](https://docs.patchmypc.com/installation-guides/patch-my-pc-cloud/deployments/update-rings/how-update-rings-are-created#immediate-update-rings)Update Rings.

You can add multiple companies to an App Set and to the same set of Update Rings.

A child customer also doesn’t need to be present in all rings. For example, if you create four Update Rings for an App Set, but a child customer only requires two rings, you only need to add that child customer to the two relevant rings. On the child customer side, only the rings they are part of will be created in the child company, not all four rings defined in the App Set.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (817).png" alt="Clicking “Enable Update Rings”" width="563"><figcaption></figcaption></figure>

4.  Click **Add Assignment**\
    <br>

    <figure><img src="../../../.gitbook/assets/image (818).png" alt="Clicking “Add Assignment”" width="563"><figcaption></figcaption></figure>
5. Select the relevant company that has an Intune connection that you want to assign this deployment to and click **Next**

{% hint style="info" %}
**Note**

You can only select a single company at a time (up to a maximum of 100), as every company’s Entra ID setup in terms of resources will be different.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (820).png" alt="Selecting the relevant company to assign this deployment to." width="466"><figcaption></figcaption></figure>

6. On the **Assignments** tab, select the relevant resources you want to deploy this app to and click **Save**.

<figure><img src="../../../.gitbook/assets/image (821).png" alt="Selecting the relevant resources for this assignment" width="460"><figcaption></figcaption></figure>

7. Repeat steps 4 to 6 to add any additional companies you want to deploy this App Set to.
8. On the **App Set** page, configure any required settings for the assignments.

{% hint style="success" %}
**Tip**

If you are using Update Rings for this App Set, we recommend you create all of the assignments first, which adds all of them to the first Update Ring. Then drag and drop the assignments to the relevant rings.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (822).png" alt="Configuring any required settings for the assignments" width="563"><figcaption></figcaption></figure>

9.  Click **Deploy** to deploy this App Set.<br>

    <figure><img src="../../../.gitbook/assets/image (824).png" alt="Clicking “Deploy” to deploy this App Set" width="563"><figcaption></figcaption></figure>

The **App Sets** page is redisplayed along with the **Success – App Set created** notification. The newly created App Set will show a Status of **In Progress**, followed by **Success** once all the deployments within the App Set have been completed successfully.

{% hint style="info" %}
**Note**

The **Status** will show as **Failed** if one or more of the deployments fails.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (825).png" alt="“App Sets” showing the newly created deployment" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

You and the admins at the child company can monitor the status of each individual deployment from the **Deployments** node of the targeted company.

![App Set deployment when viewed from the child company](<../../../.gitbook/assets/image (826).png>)
{% endhint %}

{% hint style="danger" %}
**Important**

You cannot **Edit** or **Delete** a deployment from the **Deployments** node if it belongs to an App Set (these options are unavailable when clicking on the ellipsis (**⋮**) beside the deployment). This is another reason for adding the App Set’s name as a suffix to the app’s **Display Name** so that when you are viewing all of your deployments, you and the admins at your child companies can easily identify which deployment belongs to an App Set.
{% endhint %}

Once the App Set has been deployed successfully, it will show a **Status** of **Success** on the **App Sets** page.

<figure><img src="../../../.gitbook/assets/image (827).png" alt="App Set showing with a status of “Success”" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Once successfully created, any deployments created as part of an App Set will be updated based on the Sync Schedule configured at each child customer. So even if you have a single App Set with deployments to multiple child customers, you can end up with different versions of the same app at different child customers depending on when the [Sync Schedule](../../manage/settings/sync-schedule.md) runs. See [Manage Updates](../../deployments/manage-deployments/updates/) for more information.
{% endhint %}

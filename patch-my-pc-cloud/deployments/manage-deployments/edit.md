# Edit a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

In Patch My PC (PMPC) Cloud, a successful deployment can be edited (changed) should you wish to change any of its settings (e.g., assignments, command line parameters, etc.).

{% hint style="info" %}
**Note**

Some notes about Deployments:

* Only successful deployments can be edited.
* If you edit a deployment with [App Dependencies](../deploy-app/configurations-tab/additional-tools/dependencies.md) configured and edit just the dependency, the app won’t be republished in Intune from scratch. However, making any other changes could result in the app being republished.
* If the **Apply Template** option is unavailable when editing a deployment, as templates are currently unsupported for use in existing deployments. See [Use a Template in Deployment](../use-template.md) for more information.
* When you edit an existing deployment, if a default template has been configured for the OS platform that this deployment uses, the default template is not applied when you save the deployment.
* If when you edit an existing deployment several variants of the app are available, we prevent you from changing any settings that could lead to issues such as different installer variants of the same app being installed on devices with the currently deployed one already installed.
* Editing a Return Code in an existing deployment does not trigger the recreation of app.
{% endhint %}

There are two ways to edit a deployment:

* [Editing a deployment from the Deployments node](edit.md#editing-a-deployment-from-the-deployments-node)
* [Editing a deployment from the App Catalog](edit.md#editing-a-deployment-from-the-app-catalog)

## Editing a deployment from the Deployments node

To edit an existing deployment from the **Deployments** node:

1. Navigate to the **Deployments** node.
2.  Click the relevant deployment you want to edit.<br>

    <figure><img src="../../../.gitbook/assets/image (2589).png" alt="Clicking the relevant deployment you want to edit."><figcaption></figcaption></figure>
3.  On the deployment's property page click **Edit**.

    <figure><img src="../../../.gitbook/assets/image (2712).png" alt="Clicking &#x22;Edit&#x22; on the deployment&#x27;s property page."><figcaption></figcaption></figure>

    The Deployment Wizard starts.<br>

    <figure><img src="../../../.gitbook/assets/image (2591).png" alt="Deployment Wizard starting."><figcaption></figcaption></figure>
4. Follow the [Deploy an App](../deploy-app/) process.

{% hint style="info" %}
**Note**

Be mindful of any changes you make, as you are editing the existing deployment, not creating a new one.
{% endhint %}

{% hint style="success" %}
**Tip**

You can also edit a deployment from the **Deployments** node by clicking the ellipsis (**⋮**) beside the relevant deployment you want to edit, then click **Edit**.

<img src="../../../.gitbook/assets/image (2592).png" alt="Clicking the ellipsis beside the relevant deployment you want to edit, then clicking Edit." data-size="original">
{% endhint %}

## Editing a deployment from the App Catalog

To edit a deployment from the App Catalog:

1.  Navigate to the **App Catalog** and click on the app whose deployment you wish to edit.<br>

    <figure><img src="../../../.gitbook/assets/image (2586).png" alt="Navigating to the App Catalog and locating the app whose deployment you wish to edit."><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

Any apps already deployed by Intune Apps have the green cloud icon with a tick (![](<../../../.gitbook/assets/image (2585).png>)) next to the version number.
{% endhint %}

2.  Click **Edit Deployment** on the deployment's property page.<br>

    <figure><img src="../../../.gitbook/assets/image (2713).png" alt="Clicking &#x22;Edit Deployment&#x22; on the deployment&#x27;s property page."><figcaption></figcaption></figure>

The behavior of the **Edit Deployment** button depends on whether there is at least one existing, successful deployment:

* If there is only deployment for an app, clicking the **Edit Deployment** button starts the Deployment Wizard.
* If there is more than one deployment for the same app, clicking the **Edit Deployment** button provides a dropdown list of all deployments for this app, from which you can select the relevant deployment to edit. Clicking a deployment starts the Deployment Wizard.

{% hint style="info" %}
**Note**

If there is more than one deployment for the same app but any of them are in **Processing**, **Retrying** or **Failed** state, the **Edit Deployment** button still provides a dropdown list of all deployments for this app, but you can only select those that have successfully completed to edit.
{% endhint %}

The Deployment Wizard starts.

<figure><img src="../../../.gitbook/assets/image (2591).png" alt="Deployment Wizard starting."><figcaption></figcaption></figure>

3. Follow the [Deploy an App](../deploy-app/) process.

{% hint style="info" %}
**Note**

Be mindful of any changes you make, as you are editing the existing deployment, not creating a new one.
{% endhint %}

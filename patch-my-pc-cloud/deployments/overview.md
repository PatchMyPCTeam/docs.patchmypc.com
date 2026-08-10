# Overview of Deployments in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Patch My PC (PMPC) Cloud supports the following methods for deploying apps:

* [Deploying an App we can auto-update from our App Catalog](overview.md#deploying-an-app-we-can-auto-update-from-our-app-catalog)
* [Deploying an App we cannot auto-update from our App Catalog](overview.md#deploying-an-app-we-cannot-auto-update-from-our-app-catalog)
* [Using Custom Apps to deploy a custom EXE or MSI](overview.md#using-custom-apps-to-deploy-a-custom-exe-or-msi)

## Deploying an App we can auto-update from our App Catalog

The PMPC App Catalog contains apps for which there is a publicly accessible download of the installer that we can deploy and update. In the majority of cases, you should use the [Deploy an App](deploy-app/) process to deploy your apps.

## Deploying an App, we cannot auto-update from our App Catalog

Some apps do not publish a publicly accessible download. These are typically apps:

* You need to pay for.
* The installer is behind a paywall that requires an individual login and password.
* The vendor uses a compressed file for its installer.

We refer to such apps as _Binary-free apps_ and you should follow the [Create a Binary Free App](../binary-free-apps/deploy-a-binary-free-app.md) process.

{% hint style="info" %}
**Note**

See our [Products that Require Manual Download to the Local Content Repository](https://patchmypc.com/local-content-repository-for-licensed-applications-that-require-manual-download) for a list of such apps that we’ve built and maintain.
{% endhint %}

## Using Custom Apps to deploy a custom EXE or MSI

If you have your own installer (EXE or MSI) that you want to deploy, then you should follow the [Create a Custom App](../custom-apps/create-a-custom-app/) and [Publish a Custom App](../custom-apps/publish-a-custom-app.md) processes.

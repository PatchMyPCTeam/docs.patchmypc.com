# Managing External Apps in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

{% hint style="danger" %}
**Important**

This feature is currently only available through an invitation-only Private Preview, as both it and the documentation are under development, incomplete, and subject to change.

Please do not share links to these docs with others outside of the Private Preview.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

The **External** child node of the **App Catalog** node in the Patch My PC (PMPC) Cloud Portal lets you create a catalog of external apps that can be managed and deployed using PMPC Cloud.

{% hint style="danger" %}
**Important**

Any apps managed by the External catalog are not curated, vetted, and maintained by PMPC. You are responsible for all due diligence of such apps and their ongoing support. We merely provide the mechanism to use them with PMPC Cloud.
{% endhint %}

## Current Limitations

In the current release, the **External** catalog has the following limitations:

* Only apps in the Public WinGet repository can be managed using the External catalog. Apps in private Winget repositories are unsupported.
* Other catalogs/repositories may be added in the future, based on customer demand.
* WinGet Apps available in the Patch My PC curated catalog cannot be added or deployed. In this scenario, you will be pointed to deploy the app from the Patch My PC Catalog.
* The following app types cannot be added:
  * APPX
  * MSIX
  * Portable
  * PWA
* This feature is not available in Managed Service Provider (MSP) App Sets.
* MSPs will have to add and deploy external apps for each individual company.
* The Migration feature of PMPC Cloud does not support migrating WinGet applications from Microsoft ConfigMgr applications to Intune.
* The Discovery feature of PMPC Cloud does not check WinGet apps. This may change in future iterations based on customer demand.
* All WinGet apps are created with the official Microsoft brown folder with a white arrow. It is possible to change this when deploying the app.

### Using the External Catalog

To be able to manage an app using the **External** catalog, you need to:

* [Enable the External Catalog](enable-external-catalog.md)
* [Add the External App](add-external-app.md)
* [Deploy the External App](deploy-external-app.md)

{% hint style="info" %}
**Note**

You can also [Delete an External App](delete-external-app.md).
{% endhint %}

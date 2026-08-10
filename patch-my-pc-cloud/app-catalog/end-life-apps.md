# End-Of-Life Apps in Patch My PC Cloud

_Applies to: Patch My PC (PMPC) Cloud_

There are times when we need to remove a product from the Patch My PC (PMPC) App Catalog, primarily because the product either:

* Goes End-Of-Life (EOL) and is no longer supported or maintained by the vendor.
* Other compatibility issues related to silent install or versioning.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See <a href="https://patchmypc.com/kb/how-products-are-handled-end/">How Products are Handled at End-Of-Life (EOL) or Become Incompatible</a> for more information about how we handle EOL apps in general, other reasons for removing apps from our App Catalog, and a searchable <a href="https://patchmypc.com/kb/how-products-are-handled-end/#h-list-of-products-removed-due-to-end-of-life-or-compatability-issues">List of Products Removed due to End-of-Life or Compatibility Issues</a>.</p>
</blockquote>

In PMPC Cloud, when an app goes EOL:

* The app no longer appears in App Catalog.
* Any existing deployments of the app will be flagged with the **EOL** indicator in the **Deployments** node.
* If the app has been discovered by PMPC Cloud Discovery and is currently being managed, the app itself will be flagged with the **EOL** indicator on the **Managed** tab of the **Discovery** node.

If an app that is part of an MSP App Set is marked as EOL:

* Any existing deployments of the app will be flagged with the **EOL** indicator in the App Set.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>* If an app includes multiple variants and only certain variants are marked as EOL, the other non-EOL variants continue to function normally and are not marked as EOL.</p>
<p>* Any existing deployments of EOL apps can still be edited, recreated, etc., but you will be unable to create a new deployment of the EOL app. This also applies to EOL apps that are part of an existing App Set. EOL apps will not appear in the **Select Application** dropdown when creating a new App Set.</p>
<p>* If an existing App Set contains a deployment for an EOL app, new assignments can be added to the deployment for new Child Companies managed by the MSP Parent Company.</p>
</blockquote>

## Examples of EOL Apps

The following examples show how EOL will appear in the Cloud Portal:

* [Deployments](end-life-apps.md#deployments)
* [Discovery](end-life-apps.md#discovery)
* [App Set](end-life-apps.md#app-sets)

### Deployments

An existing deployment of an EOL app will be shown as follows.

![EOL deployment](/_images/image-(4262).png "EOL deployment")

### Discovery

A managed app in **Discovery** that is EOL will be shown as follows.

![EOL app in Discovery](/_images/image-(4263).png "EOL app in Discovery")

### App Set

An EOL app deployment that is part of an existing App Set will be shown as follows.

![EOL app in an App Set](/_images/image-(4264).png "EOL app in an App Set")
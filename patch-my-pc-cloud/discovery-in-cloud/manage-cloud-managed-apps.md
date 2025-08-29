# Manage Cloud Managed Apps

_Applies to: Patch My PC Cloud_

Once an app appears on the **Managed** tab of the **Discovery** node, it means there is at least one matching deployment in either Patch My PC (PMPC) Cloud or our on-premises Publisher for that app.

To administer a Managed app:

1. Navigate to the **Discovery** node.
2.  Click the **Managed** tab.\


    <figure><img src="/_images/gitbook/image%20%28397%29.png" alt="Clicking the “Managed” tab."><figcaption></figcaption></figure>

    \
    The list of discovered managed apps is shown.\


    <figure><img src="/_images/gitbook/image%20%282123%29.png" alt="“Managed” tab"><figcaption></figcaption></figure>

The following columns are shown on this page:

| Column          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| App Name        | <p>The name of the app, which is always taken from our App Catalog as there may be a situation where multiple products from an app have been mapped to a single discovered app from Intune. In such cases, we show you the multiple records for each app.<br><br>We also show you which product published the app:<br><br>• PMPC Cloud (<img src="/_images/gitbook/image%20%282124%29.png" alt="">)</p><p>• On-Prem Publisher (<img src="/_images/gitbook/image%20%282125%29.png" alt="">)</p> |
| Vendor          | As shown in Intune. If no vendor name exists in Intune, we show the one from our App Catalog.                                                                                                                                                                                                                                                                                                                                                                                                |
| # Of Installs   | The number of installations of this app in your environment.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Assigned To All | <p>Shows:</p><p>• How the app was deployed</p><p>• Whether there is at least one deployment with a Required or <strong>Update Only</strong> assignment type that is assigned to <strong>All Users</strong> or <strong>All Devices</strong></p><p>• <strong>Unknown</strong> if the app has only been deployed via Publisher.</p>                                                                                                                                                             |

{% hint style="info" %}
**Note**

See the [Discovery Managed Apps Reference](cloud-discovery-managed-apps-reference.md) for more information and examples of how various apps appear on the **Managed** tab depending on how they have been deployed.
{% endhint %}

{% hint style="success" %}
**Tip**

Hovering over either the value in the **Assigned To All** column or **Edit** button for a deployment will show a tooltip providing more information.
{% endhint %}

3. Click the **Edit** button beside the app you want to edit:

* If the app only has one deployment, the **Edit** button includes a pencil (<img src="/_images/gitbook/image%20%28528%29.png" alt="" data-size="line">).
* If the app has more than one deployment, the **Edit** button includes a down arrow (<img src="/_images/gitbook/image%20%28529%29.png" alt="" data-size="original">) beside it, which, when clicked, provides a dropdown list of all of the deployments for the app, from which you can choose the deployment you want to edit.

{% hint style="info" %}
**Note**

If the **Edit** button is unavailable, the deployment was created in Publisher and cannot be managed through the portal.
{% endhint %}

{% hint style="warning" %}
**Important**

We do not recommend deploying the same app through the Publisher and PMPC Cloud to avoid settings conflicts and unwanted app behavior.
{% endhint %}

<figure><img src="/_images/gitbook/image%20%282126%29.png" alt="Different styles of the “Edit” button"><figcaption></figcaption></figure>

The Deployment Wizard starts, allowing you to make any required changes.

<figure><img src="/_images/gitbook/image%20%28531%29.png" alt="Deployment Wizard starting"><figcaption></figcaption></figure>

4. Make any required changes, then click **Save** to save them.

{% hint style="warning" %}
**Important**

Remember, it can take up to 24 hours for the changes you make to be applied to the discovery data, and even then, up to a week for an app to appear on the **Managed** tab unless you [refresh your discovery data](refresh-cloud-discovery-data.md).
{% endhint %}

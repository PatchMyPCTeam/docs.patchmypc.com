# Manage Cloud Managed Apps

_Applies to: Patch My PC Cloud_

Once an app appears on the **Managed** tab of the **Discovery** node, it means there is at least one matching deployment in either Patch My PC (PMPC) Cloud or our on-premises Publisher for that app.

To administer a Managed app:

1. Navigate to the **Discovery** node.
2.  Click the **Managed** tab.\\

    ![Clicking the "Managed" tab.](/_images/image-(397).png)

    \
    The list of discovered managed apps is shown.\\

    !["Managed" tab](/_images/image-(2123).png)

The following columns are shown on this page:

| Column          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| App Name        | <p>The name of the app, which is always taken from our App Catalog as there may be a situation where multiple products from an app have been mapped to a single discovered app from Intune. In such cases, we show you the multiple records for each app.<br><br>We also show you which product published the app:<br><br>• PMPC Cloud (![](/_images/image-(2124).png))</p><p>• On-Prem Publisher (![](/_images/image-(2125).png))</p> |
| Vendor          | As shown in Intune. If no vendor name exists in Intune, we show the one from our App Catalog.                                                                                                                                                                                                                                                                                                                                                                                |
| # Of Installs   | The number of installations of this app in your environment.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Assigned To All | <p>Shows:</p><p>• How the app was deployed</p><p>• Whether there is at least one deployment with a Required or <strong>Update Only</strong> assignment type that is assigned to <strong>All Users</strong> or <strong>All Devices</strong></p><p>• <strong>Unknown</strong> if the app has only been deployed via Publisher.</p>                                                                                                                                             |

> \*\*Note\*\*
>
> See the \[Discovery Managed Apps Reference]\(cloud-discovery-managed-apps-reference.md) for more information and examples of how various apps appear on the \*\*Managed\*\* tab depending on how they have been deployed.

> \*\*Tip\*\*
>
> Hovering over either the value in the \*\*Assigned To All\*\* column or \*\*Edit\*\* button for a deployment will show a tooltip providing more information.

3. Click the **Edit** button beside the app you want to edit:

* If the app only has one deployment, the **Edit** button includes a pencil (![](/_images/image-(528).png)).
* If the app has more than one deployment, the **Edit** button includes a down arrow (![](/_images/image-(529).png)) beside it, which, when clicked, provides a dropdown list of all of the deployments for the app, from which you can choose the deployment you want to edit.

> \*\*Note\*\*
>
> If the \*\*Edit\*\* button is unavailable, the deployment was created in Publisher and cannot be managed through the portal.

> \*\*Important\*\*
>
> We do not recommend deploying the same app through the Publisher and PMPC Cloud to avoid settings conflicts and unwanted app behavior.

![Different styles of the "Edit" button](/_images/image-(2126).png)

The Deployment Wizard starts, allowing you to make any required changes.

![Deployment Wizard starting](/_images/image-(531).png)

4. Make any required changes, then click **Save** to save them.

> \*\*Important\*\*
>
> Remember, it can take up to 24 hours for the changes you make to be applied to the discovery data, and even then, up to a week for an app to appear on the \*\*Managed\*\* tab unless you \[refresh your discovery data]\(refresh-cloud-discovery-data.md).
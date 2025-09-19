# Cloud Discovery Managed Apps Reference

_Applies to: Patch My PC Cloud_

As detailed in [Managing Managed Apps](manage-cloud-managed-apps.md), an app will appear on the **Managed** tab of the **Discovery** node of Patch My PC (PMPC) Cloud if there is at least one matching deployment in either PMPC Cloud or our on-premises Publisher (Publisher) for that app.

This article includes examples of each of the supported scenarios.

> **Tip**
>
> Hovering over either the value in the **Assigned To All** column or **Edit** button for a deployment will show a tooltip providing more information.

### PMPC Cloud-Only Deployment

If the app has only been deployed using PMPC Cloud, the app:

* Has the PMPC Cloud (![](/_images/image-(2124).png%3E)) icon beside its name.
* Has either a red X (![](/_images/image-(379).png)) or green tick (![](/_images/image-(380).png)) in the **Assigned To All** column, depending on whether there is at least one deployment with a **Required** or **Update Only** assignment type to the Intune pre-defined **All Users** or **All Devices** assignments:
  * A red X indicates there isn’t.
  * A green tick indicates there is.
* The **Edit** button is either:
  * A pencil (![](/_images/image-(381).png)) if the app only has one deployment.
  * A down arrow (![](/_images/image-(382).png)) if the app has multiple deployments. When you click the arrow, a dropdown list opens containing all of the deployments for the app from which you can choose the deployment you want to edit.

In the following screenshot:

* Both **Notepad++** and **Zoom Workplace** have only been deployed through PMPC Cloud.
* **Notepad++** has a single deployment with a **Required** assignment type to **All Users**.
* **Zoom Workplace** has multiple deployments, but none have a **Required** assignment type to **All Users** or **All Devices**.

![How an app only deployed through PMPC Cloud appears in the "Managed" tab](/_images/image-(2127 "How an app only deployed through PMPC Cloud appears in the \"Managed\" tab").png)

This can be confirmed by searching for the app in the App Catalog.

![How an app only deployed through PMPC Cloud appears in the App Catalog](/_images/image-(384 "How an app only deployed through PMPC Cloud appears in the App Catalog").png)

### Publisher Only Deployment

If the app has only been deployed using Publisher, as PMPC Cloud did not create the deployment, the app:

* Has the On-Prem Publisher (![](/_images/image-(2125).png%3E)) icon beside its name.
* Has a value of **Unknown** in the **Assigned To All** column.
* The **Edit** button is disabled as you need to edit the deployment in Publisher.

In the following screenshot, the **Google Chrome** app has only been deployed using Publisher.

![How an app only deployed through Publisher appears in the "Managed" tab](/_images/image-(2128 "How an app only deployed through Publisher appears in the \"Managed\" tab").png)

This can be confirmed by searching for the app in the App Catalog.

![How an app only deployed through Publisher appears in the App Catalog](/_images/image-(2129 "How an app only deployed through Publisher appears in the App Catalog").png)

### PMPC Cloud and Publisher Deployment

> **Important**
>
> We do not recommend deploying the same app through the Publisher and PMPC Cloud to avoid settings conflicts and unwanted app behavior.

If the app has been deployed using PMPC Cloud and Publisher, the app:

* Has both the PMPC Cloud (![](/_images/image-(2124).png%3E)) and On-Prem Publisher (![](/_images/image-(2125).png%3E)) icons beside its name.
* Has either a red X (![](/_images/image-(387).png)) or green tick (![](/_images/image-(389).png)) in the **Assigned To All** column, depending on whether there is at least one PMPC Cloud deployment with a **Required** or **Update Only** assignment type to the Intune pre-defined **All Users** or **All Devices** assignments:
  * A red X indicates there isn’t.
  * A green tick indicates there is.
* The **Edit** button is only available to edit the PMPC Cloud deployment and will either be:
  * A pencil (![](/_images/image-(390).png)) if the app only has one deployment.
  * A down arrow (![](/_images/image-(391).png)) if the app has multiple deployments. When you click the arrow, a dropdown list opens containing all of the deployments for the app from which you can choose the deployment you want to edit.

In the following screenshot, **Notepad++** has been deployed through Publisher and PMPC Cloud, with the PMPC Cloud deployment having a **Required** or **Update Only** assignment type to the Intune pre-defined **All Users** or **All Devices** assignments.

![How an app deployed through both PMPC Cloud and Publisher appears in the "Managed" tab](/_images/image-(2130 "How an app deployed through both PMPC Cloud and Publisher appears in the \"Managed\" tab").png)

This can be confirmed by searching for the app in the App Catalog.

![How an app deployed through both PMPC Cloud and Publisher appears in the App Catalog](/_images/image-(2131 "How an app deployed through both PMPC Cloud and Publisher appears in the App Catalog").png)